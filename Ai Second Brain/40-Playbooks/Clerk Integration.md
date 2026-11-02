---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [playbook, auth, identity, clerk, nextjs, security]
sources:
  - https://clerk.com/docs/nextjs/getting-started/quickstart
---

# Clerk Integration

## Scope and Fit

This playbook covers Clerk as an identity provider for a Next.js App Router application: sign-in, sign-up, sessions, and server-side identity checks. It does not cover Clerk Organizations, Billing, or a migration from another identity provider unless that migration is separately planned and approved.

Use Clerk when you need hosted sign-in, social and email authentication, session management, and prebuilt account UI without building an identity system. Do not use Clerk as a substitute for application authorization: Clerk proves who a user is, not what that user may do in your application, tenant, or data.

Verify the current [Next.js quickstart](https://clerk.com/docs/nextjs/getting-started/quickstart) before use. That page was last updated 2026-10-30 in the version checked for this playbook, and Clerk's setup guidance changes with Next.js versions. In particular, recheck the middleware/proxy filename, the provider placement, and the async `auth()` rule below against the current quickstart, not against memory or an older tutorial.

## Trust Boundary

```text
untrusted client -> Clerk hosted sign-in / session -> Next.js proxy/middleware (route protection only)
server action / route handler -> await auth() -> verified userId -> application authorization -> tenant-scoped data
```

The proxy/middleware file is not the sole authorization boundary. Re-check authorization in every Server Action and Route Handler that reads or changes data, even when the route is already protected by middleware. A protected route proves a session exists; it does not prove the user may access that record, tenant, or operation.

## Prerequisites and Approval Boundaries

- Accept an ADR covering identity model, sign-in methods, session lifetime, organizations if used, data residency and retention, cost, and exit.
- Security-review the exact `@clerk/nextjs` version, the Clerk CLI version if used, and any Clerk-related dependency before use.
- Creating a Clerk application, changing sign-in methods, changing production keys, enabling organizations or billing, migrating users, and deleting an application or user data are R3.
- Apply [Identity and Authentication Selection](../30-Skills/identity-auth-selection/SKILL.md), [OAuth and OpenID Connect Integration Security](../30-Skills/oauth-oidc-integration-security/SKILL.md), and [Session and Cookie Security](../30-Skills/session-cookie-security/SKILL.md) for the surrounding decisions. This playbook does not replace them.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY` | Public, intentionally in the client bundle | Clerk publishable key for the selected Clerk application and environment |
| `CLERK_SECRET_KEY` | Server secret only, never `NEXT_PUBLIC_` | Clerk secret key for server-side identity checks |

Use separate Clerk applications, or separate development and production instances as Clerk currently provides them, for development, preview, and production. Never reuse development keys in production, and never commit a secret key, a development key file, or a production key to the repository. Keep keys in the approved secret store and in the hosting provider's environment settings, scoped per environment.

## Setup, Following the Current Quickstart

The current quickstart's default path is the Clerk CLI, not hand-written setup:

```bash
npx -y clerk@latest init
```

That command, run signed in or not, detects the framework and package manager, provisions a claimable application when signed out, writes development keys to `.env.local`, and configures the SDK, provider, middleware/proxy file, and auth routes. Signing in later claims the application. Do not install `@clerk/nextjs` or hand-write setup first; fall back to manual setup only if `init` has already run and failed, as the quickstart directs.

After setup, verify with:

```bash
npx -y clerk@latest doctor
```

Then start the app and confirm sign-in, sign-up, and signed-in user controls are visible, and that sign-in and sign-up actually work.

### Filename, provider, and async rules — recheck these every time

- **Filename follows the Next.js version in `package.json`:** `proxy.ts` on Next.js 16+, `middleware.ts` on Next.js 15 and below. The contents are otherwise the same, and the CLI creates the correct file. Do not copy a `middleware.ts` example into a Next.js 16 project without checking this rule.
- **Middleware/proxy by default protects nothing.** All routes are public until you opt in. Protect routes close to where they are used, for example with a route matcher and `auth.protect()` for dashboard and private API routes.
- **`ClerkProvider` goes inside `<body>`, not wrapping `<html>`.** Use prebuilt components such as `SignInButton`, `SignUpButton`, `Show`, and `UserButton` from `@clerk/nextjs`, and wrap request-dependent UI such as `<Show>` in `<Suspense>`.
- **`auth()` from `@clerk/nextjs/server` is async. Always `await auth()`.**
- **Never expose `CLERK_SECRET_KEY` in client code.** Use `@clerk/nextjs`, not `@clerk/clerk-react`, for a Next.js application.

A minimal protected-route shape, to be checked against the current quickstart before use, is:

```ts
import { clerkMiddleware, createRouteMatcher } from "@clerk/nextjs/server";

const isProtectedRoute = createRouteMatcher(["/dashboard(.*)", "/api/private(.*)"]);

export default clerkMiddleware(async (auth, req) => {
  if (isProtectedRoute(req)) await auth.protect();
});

export const config = {
  matcher: [
    "/((?!_next|[^?]*\\.(?:html?|css|js(?!on)|jpe?g|webp|png|gif|svg|ttf|woff2?|ico|csv|docx?|xlsx?|zip|webmanifest)).*)",
    "/(api|trpc)(.*)",
  ],
};
```

Copy the matcher from the current quickstart for the project, rather than assuming the example above is still current.

### Application identity mapping

Clerk gives you a verified `userId` for a session. Your application still needs its own user and tenant records:

- Create or look up the application user from the verified `userId` on the server, after authorization, not from a client-sent user id.
- Store the mapping in your own database, with tenant membership and roles enforced by your own authorization checks, not by Clerk alone.
- On sign-up, account closure, or user deletion, define what happens to application data, tenant membership, and billing state. Do not delete application data solely on an unverified lifecycle signal, and do not assume a Clerk deletion automatically deletes your data, or vice versa. Verify webhook signature handling in the current Clerk docs before relying on lifecycle webhooks.

## Local, Preview, and Production Setup

- **Local:** Use development keys from `.env.local`, created by the CLI or from the Clerk Dashboard for a development instance. Do not use production keys locally.
- **Preview:** Use preview-scoped keys and a preview Clerk instance where the project supports one. Preview users, sessions, and data must not grant production access, and preview sign-in must not use production secrets.
- **Production:** Use production keys, scoped only to production, set in the hosting provider (for example Vercel, via its Marketplace integration where that integration is currently offered — verify the current Marketplace listing before relying on it). Enable production sign-in methods, domains, and redirect URLs explicitly; do not leave a development redirect or test domain as a production fallback.
- **Rotation:** Rotate a compromised or leaked secret key immediately, update every environment that uses it, and verify that old sessions and integrations behave as expected after rotation. A key rotation is a production change, not a configuration tweak.

## Verification

- Sign-up, sign-in, sign-out, password reset, and social sign-in (where enabled) work on local, preview, and production, with the correct keys per environment.
- Protected routes redirect or reject signed-out users, and unprotected routes remain public as intended. No route is protected only by middleware: every data-changing Server Action and Route Handler re-checks authorization.
- Wrong-user and wrong-tenant requests return no data and cannot mutate, even when the session is valid.
- `CLERK_SECRET_KEY` does not appear in client bundles, logs, error messages, or committed files.
- Session expiry, sign-out, and account-switching clear application session state and do not leak the previous user's data.
- A compromised-key rotation has been rehearsed or is documented with exact steps, owners, and verification checks.

## Operations, Cost, and Exit

Monitor sign-in failures, session errors, middleware/proxy errors, and Clerk Dashboard status, alongside application authorization failures. Alert on a spike in failed sign-ins, on production key errors, and on any authorization bypass report, and treat those as security incidents, not as ordinary errors.

Recheck Clerk pricing, plan limits, monthly active user counting, and any Organizations or Billing add-on costs for the selected plan before an ADR is accepted. Do not quote a price from this playbook; prices and plan boundaries change.

For exit, inventory what Clerk owns versus what your application owns: user identities, sessions, social connections, organizations, and any Clerk-hosted data. Plan user export, password and social-login migration, session invalidation, and data deletion in advance, and do not assume passwords are portable. Verify current export capabilities in the Clerk docs before promising a migration path. Revoke keys and delete the application only after the replacement identity system is verified and a rollback is no longer needed.

## Re-Review Triggers

- Next.js major version, Clerk SDK major version, middleware/proxy filename rule, or `auth()` API change
- Sign-in method, domain, redirect, session, Organizations, or Billing change
- Pricing, plan, data residency, retention, or subprocessors change
- Key leak, authorization bypass, session confusion, or cross-tenant result
- Any change to how the application maps Clerk identities to tenants, roles, or entitlements
