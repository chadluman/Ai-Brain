---
status: reviewed
owner: vault-owner
created: 2026-10-21
last_verified: 2026-11-02
review_by: 2027-01-21
risk: R0
tags: [playbooks, map]
sources: []
---

# Playbooks Map

Playbooks connect focused skills into an ordered delivery path. They route to one source of truth rather than repeating detailed guidance.

| Playbook | Use it for | State |
|---|---|---|
| [Web Application Delivery](Web%20Application%20Delivery.md) | Moving a web product from evidence and architecture through a thin vertical slice, release, operation, and handoff | Draft pending a complete representative project exercise |
| [Intentional Interface Design](Intentional%20Interface%20Design.md) | Turning a product brief into an original, state-complete, accessible, and verifiably functional interface | Draft pending a representative design-to-implementation exercise |
| [Managed Database Security Baseline](Managed%20Database%20Security%20Baseline.md) | Applying shared trust-boundary, least-privilege, tenant-isolation, query, migration, recovery, and verification controls | Reviewed guidance; production application remains project-specific and R3 |
| [Supabase Integration](Supabase%20Integration.md) | Integrating hosted Postgres, Data API, Auth, grants, and RLS with tested client/server boundaries | Draft pending isolated RLS, migration, and restore exercise |
| [Firebase Firestore Integration](Firebase%20Firestore%20Integration.md) | Integrating Firebase Auth and Cloud Firestore with document modeling, Security Rules, emulator tests, and recovery | Draft pending isolated rules, quota, and restore exercise |
| [Neon Postgres Integration](Neon%20Postgres%20Integration.md) | Integrating managed Postgres with pooled/direct roles, branching, scaling, and recovery | Draft pending isolated connection, migration, and restore exercise |
| [MongoDB Atlas Integration](MongoDB%20Atlas%20Integration.md) | Integrating a managed document database with schema validation, indexes, network controls, roles, and backup | Draft pending isolated validation, failover, and restore exercise |
| [Cloudflare D1 Integration](Cloudflare%20D1%20Integration.md) | Integrating Worker-bound SQLite-compatible storage with tenant-scoped queries, limits, consistency, and Time Travel | Draft pending isolated Worker, limit, and restore exercise |
| [Amazon Aurora PostgreSQL Integration](Amazon%20Aurora%20PostgreSQL%20Integration.md) | Integrating Aurora PostgreSQL with VPC/IAM controls, roles, pooling, capacity, failover, and recovery | Draft pending isolated infrastructure, failover, and restore exercise |
| [Clerk Integration](Clerk%20Integration.md) | Integrating Clerk identity for Next.js, with proxy/middleware protection, server-side identity checks, and per-environment keys | Draft pending isolated sign-in, authorization, and key-rotation exercise |
| [Stripe Integration](Stripe%20Integration.md) | Integrating Stripe Checkout subscriptions, Customer Portal, webhook provisioning, and ledger entitlements | Draft pending isolated checkout, webhook, and reconciliation exercise |
| [Vercel Integration](Vercel%20Integration.md) | Deploying Next.js to Vercel with Production, Preview, and Development environments, scoped variables, integrations, and rollback | Draft pending isolated deployment, variable-scoping, and rollback exercise |
| [OBS WebSocket Integration](OBS%20WebSocket%20Integration.md) | Controlling a local OBS Studio instance via obs-websocket from a desktop app or local bridge, with localhost-only security and reconnect handling | Draft pending isolated connection, scene-control, and reconnect exercise |
| [Twitch EventSub Integration](Twitch%20EventSub%20Integration.md) | Receiving Twitch platform events via EventSub webhooks or WebSocket, with HMAC verification, deduplication, and idempotent handlers | Draft pending isolated subscription, verification, and dedupe exercise |
| [Streamer.bot Integration](Streamer.bot%20Integration.md) | Bridging to Streamer.bot's local automation via its WebSocket API, triggering reviewed actions without duplicating alerts | Draft pending isolated connection, action-trigger, and reconnect exercise |
| [Sentry Integration](Sentry%20Integration.md) | Tracking client, server, and edge errors in Next.js with Sentry, with scrubbing, source maps, release tracking, and alerts | Draft pending isolated error, scrubbing, and alert exercise |
| [Upstash Integration](Upstash%20Integration.md) | Using Upstash Redis for cache, sessions, and rate limiting, and QStash for serverless queues and scheduling, on a Vercel and Next.js stack | Draft pending isolated cache, rate-limit, and job exercise |
| [Resend Integration](Resend%20Integration.md) | Sending transactional email with Resend and React Email templates from server-side handlers, with domain authentication and bounce handling | Draft pending isolated send, bounce, and domain exercise |
| [File Upload and Storage Integration](File%20Upload%20and%20Storage%20Integration.md) | Handling user uploads with UploadThing, public assets with Cloudflare R2, and transforms with Cloudinary, with deletion and retention rules | Draft pending isolated upload, deletion, and public-delivery exercise |
| [Inngest Integration](Inngest%20Integration.md) | Running durable, multi-step workflows with Inngest on Vercel, with step-level retries and idempotent steps, for webhooks and scheduled jobs | Draft pending isolated workflow, retry, and reconciliation exercise |
| [PostHog Integration](PostHog%20Integration.md) | Consolidating product analytics, feature flags, experiments, surveys, and session replay with PostHog, with event taxonomy and replay masking | Draft pending isolated event, flag, experiment, and masking exercise |

These provider playbooks are reviewed documentation, not provider or dependency approval. Before project use, re-verify current official sources and complete exact-version review for every executable asset. Provisioning, credentials, billing, production changes, real-data operations, restore, and deletion remain R3.
