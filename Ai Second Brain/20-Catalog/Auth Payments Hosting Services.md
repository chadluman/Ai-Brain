---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [catalog, auth, payments, hosting, managed-service]
sources:
  - https://clerk.com/docs/nextjs/getting-started/quickstart
  - https://docs.stripe.com/payments/checkout/build-subscriptions
  - https://vercel.com/kb/guide/how-to-add-vercel-environment-variables
---

# Auth, Payments, and Hosting Services

## Scope

This is a curated, project-selection shortlist, like [Backend and Database Services](Backend%20and%20Database%20Services.md). It compares materially different service shapes for the three decisions most web products make first: who signs users in, who takes their money, and where the app runs. It is not a claim that these nine services cover every valid option. Re-run [Identity and Auth Selection](../30-Skills/identity-auth-selection/SKILL.md), [Payments and Ledger Design](../30-Skills/payments-ledger-design/SKILL.md), [Hosting and Runtime Selection](../30-Skills/hosting-runtime-selection/SKILL.md), and [Third-Party Service Evaluation](../30-Skills/third-party-service-evaluation/Third-Party%20Service%20Evaluation.md) when a project's requirements point elsewhere.

No provider or executable dependency is approved by this note. Pricing shapes below were cross-checked on 2026-11-02 against vendor pricing pages as reported in October 2026 comparisons; vendors change prices, meters, and plan terms often, so pricing, quotas, regions, support, product maturity, API behavior, and security features must be rechecked from the vendor's own pricing and documentation pages for the exact plan and region before an ADR is accepted. Do not quote a price from this note to a customer or a budget without that recheck.

## Decide the Service Shape First

| Decision | Shape | What it supplies | What the application still owns |
|---|---|---|---|
| Auth | Hosted identity | Sign-in, sessions, and user management as a service, with SDKs and prebuilt UI | Authorization policy, tenant checks, session validation on every server call, and the migration path for users |
| Auth | Platform-bundled auth | Sign-in bundled with a database or backend platform | The same authorization policy, plus the platform's project lifecycle and limits |
| Payments | Payment processor | Card processing, checkout, and subscription billing; you are the seller | Tax registration and filing (unless a separate tax tool is added), refunds, disputes, and the ledger that turns payments into entitlements |
| Payments | Merchant of record | The provider is the seller, collects and remits tax, and handles disputes, for a higher percentage | Product pricing that absorbs that percentage, customer-relationship control, and the migration path for subscribers |
| Hosting | Framework-native platform | Git-based deploys, preview environments, CDN, and serverless functions tuned for one framework | Environment scoping, secret handling, usage budgets, and the exit path for data and routing |
| Hosting | Edge runtime | Code running close to users on a platform runtime, with no egress charge | Runtime compatibility, adapter support for the chosen framework, and CPU-per-request limits |

Do not choose a hosted auth service expecting it to enforce your authorization rules. Do not choose a payment provider expecting it to decide what a user is entitled to. Do not expose a secret key, service-role key, or webhook secret to a client or a public repository.

## Auth Shortlist

| Service | Shape and counting unit | Strong fit | Decisive limitations and risks | Security boundary | Portability and cost shape |
|---|---|---|---|---|---|
| Clerk | Hosted identity; bills monthly retained users (MRU) — a user who returns 24 or more hours after signing up, so sign-up-and-bounce users do not count | Next.js and React products that want prebuilt sign-in UI, organizations, and a fast path to production | MRU overage is steep at scale; enterprise SSO connections beyond the first included connection are a per-connection monthly charge; development and production instances must be kept separate | Publishable key is client-safe; the secret key is server-only; always validate the session on the server, never trust a client claim | Users can be exported and migrated, but session, organization, and webhook behavior need separate work. Cost grows with retained users, not sign-ups |
| Auth0 | Hosted identity (Okta); bills monthly active users (MAU) in discrete tier buckets, not a flat per-user rate | Products with enterprise SSO, complex rules, or a need for a mature, long-running identity platform | Paid tiers climb in discrete MAU buckets, so a small user-count increase can jump the bill; self-serve pricing ends at high volumes and becomes an enterprise quote; some capabilities are gated by tier | Secret and management credentials are server-only; production and development tenants must be separate; MFA and attack protection belong on the production tier, not the free tier alone | Portable in the sense that it speaks standard OIDC, OAuth 2, and SAML, but rules, actions, and tenant configuration are migration work. Cost grows in tier steps with MAU |
| Supabase Auth | Platform-bundled auth; bills MAU, bundled with a Supabase project | Products already building on Supabase Postgres, where auth, database, storage, and realtime live in one project | Auth follows the Supabase project lifecycle, including free-project pausing; SAML is metered; switching databases later means switching auth too, or running a separate auth service | Client key is only safe with least-privilege grants and tested row-level security on every exposed object; service-role access bypasses those policies | Core user data is portable, but auth configuration, storage, and realtime behavior are not. Cost is bundled with the database and other platform usage, which can hide the auth line item |

## Payments Shortlist

| Service | Shape and who is the seller | Strong fit | Decisive limitations and risks | Security boundary | Portability and cost shape |
|---|---|---|---|---|---|
| Stripe | Processor; you are the seller | Subscription SaaS with Checkout, Billing subscriptions, and a Customer Portal, where the team can own tax or add a tax tool | You own tax registration and filing unless Stripe Tax or a merchant-of-record layer is added; Billing adds a percentage of billing volume; subscription, invoice, and payment events must be reconciled against your own ledger | Secret key and webhook secret are server-only; verify every webhook signature; use idempotency keys; never unlock an entitlement from a client-side success page | Customers, prices, and subscriptions can be exported, but your ledger is the source of truth for entitlements and must survive a provider change. Cost is a percentage plus a fixed fee per transaction, plus billing and tax add-ons |
| Paddle | Merchant of record; Paddle is the seller | Global B2B SaaS that wants sales tax, VAT, and GST handled by the provider, with one published all-in rate | The all-in percentage is higher than a processor's rate and grows with revenue; Paddle's name appears on the buyer's statement; subscriber migration is a sales-led process, not a self-serve export | API credentials are server-only; webhook verification and your own entitlement ledger still apply; the provider handles tax, not your authorization rules | Subscribers live in Paddle, so a move away needs a migration plan for payment methods and billing cycles. Cost is a percentage plus a fixed fee per checkout transaction, with no separate monthly platform fee |
| Lemon Squeezy | Merchant of record; Lemon Squeezy is the seller | Small digital products and license-key sales that want a storefront and tax handling without a monthly fee | Owned by Stripe since 2024, with the team's focus moved to Stripe Managed Payments and slower product updates for Lemon Squeezy itself; surcharges stack for international cards, PayPal, and subscriptions; the migration path to Managed Payments may not be live for every seller, and no end date for existing stores has been announced — check its current status before committing a new product to it | Same webhook, credential, and ledger discipline as Paddle; license delivery must be driven by verified events, not by a checkout redirect | Same merchant-of-record migration caution as Paddle, plus the added uncertainty of its Stripe Managed Payments transition. Cost is a percentage plus a fixed fee, plus the surcharges above |

## Hosting Shortlist

| Service | Shape and billing unit | Strong fit | Decisive limitations and risks | Security boundary | Portability and cost shape |
|---|---|---|---|---|---|
| Vercel | Framework-native platform for Next.js; bills per developer seat plus metered usage | Next.js SaaS products that want preview deployments for every pull request and native framework behavior | Hobby is for personal, non-commercial use only, so a commercial product needs Pro; Pro is priced per developer seat, which stacks for teams; usage meters cover bandwidth, functions, builds, and image optimization | Environment variables are scoped per environment; secret variables are write-only; a change applies only to the next deployment; `NEXT_PUBLIC_` values are inlined at build time; Turborepo cache settings must include every variable a build reads | A Next.js app is portable in principle, but framework-specific features, edge configuration, and integrations are migration work. Cost is seats plus usage, with a spend control that pauses deployments at a budget |
| Netlify | Git-based platform; bills in credits that cover deploys, bandwidth, and compute | Static and Jamstack sites, and small teams that want a flat Pro price with unlimited members | Credits make the total bill harder to reason about than per-unit meters; a production deploy, bandwidth, and compute all draw from the same pool; the free plan has a hard cap and pauses sites at its limit | Same environment-scoping discipline as Vercel; preview and production variables must be separated; auto-recharge, if left on, removes the hard cap | Static output is portable; functions, forms, identity, and edge configuration are not. Cost is a monthly credit pool plus credit packs, not separate bandwidth and build-minute lines |
| Cloudflare Workers and Pages | Edge runtime; bills requests and CPU time, with no egress charge | Static sites and edge APIs at scale, where bandwidth cost dominates and the app fits an edge runtime | The Workers runtime is not full Node.js, so some libraries need compatibility flags or alternatives; full-stack Next.js needs an adapter such as OpenNext, and Pages is no longer the recommended route for new full-stack projects — check the current Cloudflare framework guide before choosing; CPU time per request is capped | Same environment and secret discipline; Worker bindings, not direct database credentials, are the way to reach platform services; a free-plan overage returns an error until the daily reset | Static assets are highly portable; Worker code, bindings, and storage (KV, D1, R2) are platform-specific. Cost is a low account floor plus metered requests and CPU, with no egress line item |

## Selection Rules

- Compare auth by the counting unit at your expected retained or active user count, not by the free tier alone. A generous free tier that counts a different population is not a cheaper plan.
- Compare payments by who is the seller and who files tax, not by the headline percentage alone. A merchant of record's higher percentage buys tax handling; a processor's lower percentage leaves tax with you.
- Compare hosting by commercial-use status, team seat model, and runtime fit, not by the free tier alone. A free plan that forbids commercial use, pauses at a hard cap, or needs an adapter for your framework is not a production plan.
- In every case, keep your own ledger for payments, your own authorization checks for auth, and your own usage budget and exit plan for hosting. The provider's dashboard is not a substitute for any of them.
