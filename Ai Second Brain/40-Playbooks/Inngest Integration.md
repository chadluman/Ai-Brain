---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [playbook, backend, workflows, jobs, webhooks, durability]
sources: []
---

# Inngest Integration

## Scope and Fit

This playbook covers Inngest for durable, multi-step workflows on a Vercel and Next.js stack: Stripe webhook handling, payout and overlay jobs, and scheduled cleanups that must survive deploys and function timeouts. Inngest functions checkpoint at each step, retry only the failed step, and support long sleeps.

Use Inngest when a workflow has multiple steps, must survive a deploy or timeout, or needs step-level retries. Use QStash (Upstash playbook) instead for simple fire-and-forget or scheduled jobs, and do not run both for the same workflow.

Do not use Inngest for code that must run outside the app, and do not use it for simple jobs where QStash is cheaper.

## Trust Boundary

```text
event source (Stripe webhook, cron, app event) -> Inngest -> durable function (steps) -> Neon, Stripe, email, overlays
untrusted client -> application authentication + authorization -> server only
```

Inngest functions run in the app's own server environment, so they inherit the app's secrets and database access. A workflow that touches money, entitlements, or user data is as sensitive as the endpoint that triggers it.

## Prerequisites and Approval Boundaries

- Apply the vault's background-job-queue-design skill, webhook-integration-design skill, and subscription-entitlement-design skill (grant only on verified paid events, idempotent and ordered events, scheduled reconciliation).
- Accept an ADR covering which workflows are durable, step boundaries, retry policy, and cost (see below).
- Security-review the exact SDK version, event schemas, and signing-key handling before use.
- Creating production workflows, changing step boundaries or retry policy, and enabling workflows that move money or grant entitlements are R3.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `INNGEST_EVENT_KEY` | Server secret | Sending events to Inngest |
| `INNGEST_SIGNING_KEY` | Server secret | Verifying Inngest requests to the app |
| `INNGEST_SERVE_PATH` | Server config | Usually `/api/inngest` |

Define functions with the Inngest SDK and `step.*` calls, serve them at the API route, and use the local dev server during development. Triggers are events or crons.

## Integration Rules

- Make every step idempotent. A step that is retried must not double-charge, double-grant, or double-send. This is the same rule as the vault's entitlement skill, applied to workflow steps.
- Keep steps small and named. A five-step function counts as six executions in the research run's secondary account, so step-count billing multiplies cost — design steps deliberately, not casually.
- Never provision from a checkout-completion event alone. Provision only on verified paid events, with the entitlement skill's reconciliation, as the Stripe playbook already requires.
- Use `step.sleep` for delays instead of a cron that polls. Polling for a future date is a job that runs forever for no reason.
- Handle Stripe webhooks through a durable function: verify the webhook signature first, then hand the verified event to Inngest, so a deploy or timeout during processing does not lose a payment event.
- Version workflows explicitly. A workflow that changes shape mid-flight (for example, a step added between a job starting and finishing) must either complete on the old shape or be re-run safely on the new one — never half on each.

## Cost Shape

Conflict, not verified, in the 2026-11-02 research run: secondary sources say Pro $75 per month and $99 per month, with a free tier of 50,000 executions. Check inngest.com/pricing before budgeting, and model cost by step count, not by function count.

## Verification

Before production use, verify in an isolated project: a workflow completes across a simulated deploy (function code changed mid-flight is handled safely); a failing step retries only that step, without re-running earlier steps' side effects; a Stripe webhook event is verified, then processed durably, then reconciled against the entitlement record; and a duplicate event does not double-grant.

## Rollback and Recovery

If a workflow misbehaves, pause that workflow's triggers, not the whole app. In-flight jobs that already granted something must be reconciled against the entitlement record before any re-run, so a recovery does not double-grant. Rotate signing keys if ever exposed.
