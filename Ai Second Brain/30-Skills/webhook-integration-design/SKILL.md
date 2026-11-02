---
name: webhook-integration-design
description: Design or review secure, recoverable inbound or outbound webhook integrations, including authenticity, replay defense, deduplication, ordering, retries, asynchronous processing, reconciliation, and provider-specific failure behavior. Use when an external system pushes HTTP event notifications; do not use for ordinary request-response APIs alone.
---

# Webhook Integration Design

## Outcome

Produce a provider-specific webhook contract and processing path that accepts authentic deliveries quickly, applies effects idempotently, survives duplicates and outages, and can be reconciled or replayed safely.

## Required Inputs

- publisher and subscriber, event types, business effects, and data sensitivity
- official signature, timestamp, retry, timeout, ordering, duplicate, retention, and redelivery behavior
- endpoint ownership, network exposure, payload-size limits, schema/version behavior, and expected load
- source-of-truth API or reconciliation method
- secret ownership, rotation, storage, and environment separation
- recovery objectives and consequences of missed, late, duplicated, or forged events

Do not generalize one provider's delivery guarantees to another. If official delivery behavior is unknown, design defensively and record the uncertainty.

## Safety and Permission Constraints

- Use HTTPS and verify authenticity before trusting or parsing business fields. Preserve the exact raw body and required headers for provider-defined verification.
- Use constant-time comparison through a reviewed cryptographic library; enforce documented timestamp or nonce replay controls.
- Never place secrets in endpoint URLs, logs, fixtures, notes, or the vault. Support overlapping secrets during controlled rotation when the provider permits it.
- Limit body size, content type, accepted methods, event types, and processing time. Treat all payload data as untrusted after signature verification.
- For outbound webhooks, prevent SSRF: validate schemes and resolved destinations, block private and link-local networks unless explicitly required, re-check redirects and DNS behavior, and isolate egress.
- Creating production endpoints, rotating real secrets, redelivering real events, or triggering irreversible effects is R3 and requires immediate authorization plus rollback or reconciliation steps.

## Workflow

1. Capture the provider's exact delivery contract from current official documentation, including what constitutes success and how failures are retried or retained.
2. Define a narrow ingestion boundary: receive the raw request, enforce limits, verify authenticity and freshness, classify the event, and reject unsupported inputs.
3. Assign a stable delivery or event identifier. Persist the verified envelope and deduplication record atomically before acknowledging when the business risk requires durable acceptance.
4. Acknowledge within the provider deadline and move slow or failure-prone work to a bounded background path.
5. Make every downstream state transition and side effect idempotent. Use database uniqueness, state-machine preconditions, idempotency keys, and an outbox where external effects must follow a committed change.
6. Assume duplicates, delay, concurrency, and out-of-order arrival unless the provider explicitly guarantees otherwise. Fetch current authoritative state when event snapshots cannot safely drive the transition.
7. Define retry classification, exponential backoff with jitter, retry limits, quarantine or dead-letter handling, operator replay, and poison-event behavior.
8. Add periodic reconciliation against the source of truth for high-impact state. Alert on age, backlog, verification failures, repeated retries, quarantine, and reconciliation drift.
9. Test valid, invalid, expired, replayed, duplicated, concurrent, out-of-order, oversized, malformed, delayed, and provider-outage cases. Verify effects, not merely HTTP responses.

## Required Output

- provider contract and trust-boundary summary
- authenticated ingestion and secret-rotation design
- deduplication, idempotency, ordering, retry, and reconciliation rules
- queue, retention, quarantine, replay, and observability plan
- payload minimization and data-retention controls
- failure-focused test matrix with expected evidence
- disconnect, rollback, and recovery procedure

## Completion Gate

Do not call the integration complete until signature and replay tests pass, duplicate and concurrent deliveries cannot duplicate effects, missed-event recovery is exercised, and the provider-specific retry and redelivery behavior is documented. Keep the skill draft until a realistic sandbox delivery test succeeds.

## Conditional Reference

Read [Webhook Evidence](references/webhook-evidence.md) before specifying signing, replay, retry, acknowledgement, or recovery behavior.
