---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [playbook, hosting, deployment, vercel, nextjs, security]
sources:
  - https://vercel.com/kb/guide/how-to-add-vercel-environment-variables
  - https://vercel.com/academy/ai-summary-app-with-nextjs/deploy-the-app
---

# Vercel Integration

## Scope and Fit

This playbook covers deploying a Next.js application to Vercel from a Git repository, with Production, Preview, and Development environments, environment-variable scoping, Marketplace integrations, and rollback. It does not cover Vercel's AI, analytics, firewall, or other add-on products unless those are separately selected and approved.

Use Vercel when Git-based deployments, automatic Preview deployments for branches, and native Next.js support fit the product, and when the team can operate within Vercel's deployment, environment, and usage model. Do not assume Vercel supplies application authorization, database backups, or a substitute for your own backup, monitoring, and cost controls.

Verify the current Vercel environment-variable guide and deployment guidance before use. The environment-variable guide checked for this playbook was last updated 2026-10-21, and Vercel's Config/Secret model, custom environments, and CLI behavior have changed recently. Recheck those sections, not just the quickstart, before a production setup.

## Trust Boundary

```text
developer -> Git push -> Vercel build (build-time variables inlined where applicable) -> immutable deployment
Production deployment <- Production-scoped variables only
Preview deployment <- Preview-scoped variables only, never production secrets
Development <- Development-scoped variables, pulled locally or injected in memory
```

A deployment is an immutable artifact. Its configuration is fixed at build time and does not shift afterward. That is what makes instant rollback safe, and it is why an environment-variable change requires a new deployment.

## Prerequisites and Approval Boundaries

- Accept an ADR covering framework and runtime, root directory and monorepo layout if any, production branch, custom domains, environment strategy, Marketplace integrations, cost and usage limits, and exit.
- Security-review the exact Vercel CLI version if used, any Vercel integration, and any build plugin before use.
- Creating a project, changing production domains, changing production environment variables, enabling a Marketplace integration, changing team policies, and deleting a project or deployment are R3.
- Apply [Hosting and Runtime Selection](../30-Skills/hosting-runtime-selection/SKILL.md), [CI/CD and Release Design](../30-Skills/ci-cd-release-design/SKILL.md), and [Secrets and Configuration Management](../30-Skills/secrets-config-management/SKILL.md) for the surrounding decisions.

## Environments and Deployments

- **Production:** A push to the production branch, usually `main`, or `vercel --prod`. The production deployment serves the production domain.
- **Preview:** A push to any non-production branch, or `vercel` without `--prod`. Every branch gets a Preview deployment with a unique URL, for testing before merge. Preview deployments must not read production secrets or production data unless that is explicitly approved and isolated.
- **Development:** Local development through `vercel dev`, or by pulling Development variables with `vercel env pull` for use with a framework dev server such as `next dev`.

Vercel auto-detects a Next.js project in the common case: framework preset Next.js, build command `next build`, and output directory `.next`. Verify those defaults for the project, and set the root directory explicitly for a monorepo or for an app that does not live at the repository root. Do not leave a monorepo root, build command, or install command at an unverified default.

### Rollback

Rollback points traffic at an older, immutable deployment whose values are exactly what they were when it shipped. Use the dashboard Redeploy/Rollback control for a production rollback, and verify the rolled-back deployment's environment, domain, and data behavior before announcing recovery. A rollback does not roll back database migrations, external service state, or Stripe/Clerk state; those need their own rollback plans.

## Configuration Inventory and Environment Variables

Environment variables can be added in the dashboard, with the Vercel CLI, or through the REST API. All three methods write to the same underlying store, so dashboard and CLI changes must be treated as the same system, not as two separate configurations.

| Variable pattern | Exposure | Purpose |
|---|---|---|
| `NEXT_PUBLIC_*` | Public, inlined into the client bundle at build time | Public configuration the browser needs, such as a publishable key or a public site URL |
| Server-only variables, no `NEXT_PUBLIC_` prefix | Server only, read at runtime from the deployment | Database URLs, secret keys, webhook secrets, and other credentials |
| `VERCEL_ENV` | System, set by Vercel | Deployment environment name. Returns `preview` for every custom environment, so it cannot distinguish custom environments |
| `VERCEL_TARGET_ENV` | System, set by Vercel | Use this for environment branching where custom environments exist, as it returns `production`, `preview`, `development`, or the custom environment's actual name |
| `VERCEL_URL` | System, set by Vercel | Deployment URL, useful for Preview-specific behavior. Do not use it as a security boundary |

### Rules that cause most environment-variable bugs

- **A variable change applies to the next deployment, not to the live deployment.** After adding or changing a variable, redeploy. The running deployment keeps its old values.
- **`NEXT_PUBLIC_` variables are inlined at build time.** Dynamic lookups such as `process.env[name]` are never inlined, and an empty value reads as `undefined`. Set the value before the build runs, and redeploy. For a value that must change without a rebuild, serve it from a runtime API instead of a build-time variable.
- **Preview deployments read only Preview-scoped variables.** Confirm the Preview target is selected, and do not debug a Preview failure by copying a production secret into Preview.
- **Config versus Secret, as of the guide checked for this playbook:** Config values remain readable to members with access. Secret values are write-only after saving: they stay available to deployments, but no member can view or retrieve them afterward. Use Secret for passwords, API keys, and tokens. You cannot edit the key of a Secret after saving, and you cannot convert a Secret to Config in place; to store the same key as Config, delete the Secret and create a new Config variable. To rotate a Secret, edit it and provide a new value. Secrets can now target Development as well as Production and Preview.
- **Branch-specific Preview variables inherit the general Preview set.** Define only the values you want to override for that branch, rather than duplicating the whole set. Managing branch-specific Preview variables from the CLI requires Vercel CLI 21.0.1 or higher, as of the guide checked for this playbook.
- **Custom environments are a plan feature.** As of the guide checked for this playbook, Pro includes one custom environment per project and Enterprise includes 12, with more available in packs of five. Do not promise a staging or QA custom environment on a plan that does not include it.
- **Turborepo cache trap, relevant to monorepos:** If `env` or `globalEnv` keys are missing from `turbo.json`, Turborepo leaves those values out of its task hash, so a cached build can be reused across environments. Declare `env` per task or `globalEnv` globally, and set `TURBO_FORCE=true` when you need to skip the cache.

### CLI shapes, to be checked against the current Vercel CLI docs before use

```bash
vercel            # Preview deployment for the current branch
vercel --prod     # Production deployment
vercel link       # Link the local directory to a Vercel project
vercel env pull   # Development variables to .env.local; also adds .env.local to .gitignore
vercel env pull --environment=preview
vercel env pull --environment=preview --git-branch=feature-branch
vercel pull --environment=staging  # Custom environment: caches variables and project settings
vercel dev        # Development variables downloaded into memory, no file written
vercel env run -e preview --git-branch feature-branch -- npm run dev
```

Note that `vercel pull` and `vercel env pull` are different commands: `vercel env pull` writes a file for a framework dev server, while `vercel pull` caches variables and project settings for `vercel build` or `vercel dev`. Do not use one when you meant the other.

## Marketplace Integrations

Integrations such as Neon, Supabase, and Upstash add their own variables to project settings, with the integration name shown next to each one. Clerk, where offered through the Vercel Marketplace, follows the same pattern: the integration provisions the service and adds its variables, but the service's own Dashboard, keys, and production instance still need to be verified and scoped per environment.

Before enabling an integration, verify the current Marketplace listing, what variables it adds, what data it can access, what it costs on the selected plan, and how to disconnect and revoke it. An integration is an executable, data-accessing dependency, not a one-click convenience, and it requires exact-version and permission review. Disconnecting an integration does not automatically delete the service's data or revoke its keys; plan that step explicitly.

## Local, Preview, and Production Setup

- **Local:** Link the project once with `vercel link`, then use `vercel dev` or `vercel env pull` for Development variables. Do not commit `.env.local`, and do not copy production variables into a local file.
- **Preview:** Use Preview-scoped variables and preview instances of every dependent service (database, identity, billing test mode). Preview deployments are for testing; they must not send real email, charge real payments, or write to production data unless that is explicitly approved and isolated.
- **Production:** Use Production-scoped variables and production instances only. Set the production branch, custom domain, and redirect rules explicitly, and verify the production deployment's environment, build output, and function logs before announcing launch.
- **Domains and DNS:** Configure the production domain, apex and subdomain behavior, and DNS records as a separate, verified step. A domain change, DNS cutover, or certificate issue is a production change, not a deployment detail.

## Verification

- Production, Preview, and Development deployments each read only their own scoped variables, and a variable change takes effect only after a redeploy.
- `NEXT_PUBLIC_` values are present in the browser bundle where intended, and server-only secrets do not appear in client bundles, build logs, or committed files.
- Preview deployments do not use production secrets, production databases, or live billing keys.
- A rollback to a previous deployment restores the expected environment, domain, and behavior, and database or external-service state has its own rollback plan.
- Marketplace integrations add only their documented variables, and disconnecting an integration has a documented key-revocation and data step.
- Build, function, bandwidth, and usage behavior are monitored against the plan, and a usage spike alerts before it becomes a cost incident.

## Operations, Cost, and Exit

Monitor deployment success and failure, build times, function errors and timeouts, usage, and spend, alongside application errors. Alert on production deployment failure, on a usage or spend anomaly, and on any preview deployment that unexpectedly uses production configuration.

Recheck Vercel pricing, plan limits, build and function quotas, and any add-on costs for the selected plan before an ADR is accepted. Do not quote a limit or price from this playbook; Vercel's plan boundaries change, and they depend on the plan and usage.

For exit, inventory the project, domains, DNS, environment variables, Marketplace integrations, deployments, and any Vercel-owned data or configuration. The application code lives in Git and is portable, but domains, DNS, environment configuration, and integration data need explicit migration steps. Delete a project only after the replacement hosting, domains, and data are verified, and after integration keys are revoked.

## Re-Review Triggers

- Vercel plan, pricing, quota, Config/Secret model, custom environment, or CLI change
- Production branch, domain, DNS, or Marketplace integration change
- Environment-variable scoping, secret rotation, or preview/production isolation failure
- Build-cache, Turborepo, or monorepo layout change
- Usage, spend, deployment failure, or rollback anomaly
