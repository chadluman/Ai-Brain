---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [playbook, backend, redis, queue, caching, rate-limiting]
sources:
  - https://upstash.com/llms-full.txt
---

# Upstash Integration

## Scope and Fit

This playbook covers Upstash Redis for cache, sessions, rate limiting, leaderboards, and pub-sub-lite, and Upstash QStash (and Workflow) for serverless queues, scheduling, and durable steps, on a Vercel and Next.js stack. Both are Edge-friendly over HTTP, so they fit serverless functions without a persistent TCP connection.

Use Upstash Redis when the app needs fast, shared, short-lived state or rate limiting across serverless invocations. Use QStash when the app needs a fire-and-forget job, a delayed job, or a scheduled job without running a worker. Use Inngest (separate playbook) instead when a workflow needs durable multi-step execution with step-level retries.

Do not use Redis as the durable primary database, and do not use QStash for long-running compute.

## Trust Boundary

```text
server / edge -> Upstash Redis (HTTP, token) -> cache, sessions, rate limits
server -> QStash publish (token) -> QStash -> app endpoint (signed) -> job handler
untrusted client -> application authentication + authorization -> server only
```

Redis tokens and QStash tokens are server secrets. QStash delivery to an app endpoint must be verified, or anyone who guesses the endpoint can trigger jobs.

## Prerequisites and Approval Boundaries

- Apply the vault's background-job-queue-design skill for job design, and its api-abuse-resource-controls skill for rate-limit design.
- Accept an ADR covering what lives in Redis versus Neon (durable data stays in Neon), rate-limit policy per endpoint, job retry and dead-letter policy, and cost (see below).
- Security-review the exact client libraries, token handling, and QStash signature verification before use.
- Creating databases, rotating tokens, enabling production rate limits, and creating production scheduled jobs are R3.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `UPSTASH_REDIS_REST_URL` | Server secret | Redis HTTP endpoint |
| `UPSTASH_REDIS_REST_TOKEN` | Server secret | Redis authentication |
| `QSTASH_URL` | Server config | QStash publish endpoint |
| `QSTASH_TOKEN` | Server secret | QStash publish authentication |
| `QSTASH_CURRENT_SIGNING_KEY` / `QSTASH_NEXT_SIGNING_KEY` | Server secret | Verification of QStash deliveries to app endpoints |

Use the `@upstash/redis` HTTP client and `@upstash/ratelimit` for sliding-window or token-bucket limits. For QStash, publish to a QStash URL with delay, retries, and a dead-letter queue, and verify the signing key on every delivery.

## Integration Rules

- Keep durable app data in Neon. Redis holds cache, sessions, rate-limit counters, and leaderboards — data the app can rebuild or lose without data loss.
- Set a time-to-live on every Redis key. A key without a TTL is a slow leak.
- Rate-limit by authenticated user or tenant where possible, and by IP only as a fallback. A shared IP limit punishes every user behind one NAT.
- Make every QStash job handler idempotent. QStash retries mean a job can be delivered more than once, and a non-idempotent handler turns a retry into a duplicate charge, alert, or email.
- Use QStash Workflow (durable steps on QStash) only for short durable steps. For long, multi-step workflows with step-level retries, use Inngest instead — and do not run both for the same workflow.
- Set a per-database budget where Upstash supports it, and alert on command volume. The research run's secondary account notes that budgets are per-database only, with no account-wide budget, so a runaway endpoint can still surprise.
- Accept the latency trade: HTTP Redis latency is higher than colocated TCP Redis in secondary accounts (1–5ms versus sub-millisecond). Do not use Upstash Redis for a hot loop that needs sub-millisecond latency.

## Cost Shape

Secondary, from a vendor markdown mirror in the 2026-11-02 research run, not vendor-verified there: Redis free 500,000 commands per month, 250MB, 10GB bandwidth; pay-as-you-go $0.20 per 100,000 commands; fixed plans from $10 per month. QStash free 1,000 messages or steps per day; pay-as-you-go $1 per 100,000. Delivery-attempt billing was described differently across older and newer mirrors — verify. Check upstash.com/pricing and upstash.com/pricing/qstash before budgeting.

## Verification

Before production use, verify in an isolated project: a cache read and write with TTL expiry; a rate limit that actually blocks after the threshold and recovers after the window; a QStash job delivered once and, on forced failure, retried and then dead-lettered without duplicate side effects; and a forged QStash delivery without a valid signature rejected.

## Rollback and Recovery

If Redis is unavailable, the app must degrade (serve from Neon, or fail a non-critical feature openly) rather than crash. If QStash delivery breaks, pause job publishing for the affected jobs and surface the backlog, rather than publishing an unbounded queue that fires all at once on recovery. Rotate tokens if ever exposed.
