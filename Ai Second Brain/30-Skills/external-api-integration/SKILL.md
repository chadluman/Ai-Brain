---
name: external-api-integration
description: Design or review an outbound integration with a third-party or partner API, including credentials, contracts, timeouts, retries, rate limits, idempotency, pagination, reconciliation, observability, sandboxing, and provider exit. Use after a provider is selected and before production connection.
---

# External API Integration

## Outcome

Build a bounded adapter that preserves domain truth and user experience when the external API is slow, unavailable, inconsistent, duplicated, rate-limited, changed, or removed.

## Required Inputs

- business operation, authoritative system, data classes, provider, API and schema versions
- authentication, scopes, endpoints, regions, network destinations, and secret ownership
- latency, availability, volume, burst, quota, pagination, ordering, freshness, and cost limits
- sync or async behavior, user-visible states, reversibility, reconciliation, and support needs
- sandbox fidelity, SDK or direct HTTP choice, changelog, deprecation, export, and exit constraints

## Safety and Permission Constraints

- Review the provider and every SDK, CLI, generated client, schema tool, sample, and executable dependency at the exact version before use.
- Use a dedicated least-privilege identity per environment. Never place keys or bearer tokens in URLs, client code, logs, analytics, error messages, or this vault.
- Treat all provider responses, errors, redirects, files, URLs, and webhook callbacks as untrusted. Validate size, schema, identifiers, media type, and business invariants.
- Do not blindly retry unsafe or non-idempotent operations. Establish provider semantics and a project idempotency or reconciliation strategy first.
- Account creation, credential grant, private-data transfer, paid calls, production traffic, write or delete operations, or provider disconnection is R3 and requires immediate authorization and rollback.

## Workflow

1. Write the domain operation and source of truth before the HTTP call. Define what provider acceptance, completion, failure, cancellation, reversal, and unknown outcome mean locally.
2. Pin the API, schema, and SDK versions. Record official docs, status, limits, pricing, change policy, data handling, support, and test-environment differences.
3. Design a narrow adapter with typed request and response validation, explicit error mapping, correlation identifiers, bounded payloads, and no provider objects leaking across the domain boundary.
4. Set connect, response, and total deadlines from the user and job budget. Cancel abandoned work and bound concurrency, queue depth, response size, redirects, and pagination.
5. Classify failures as permanent, authentication, authorization, validation, conflict, throttling, transient, dependency, or unknown. Retry only eligible cases with exponential backoff, jitter, attempt and elapsed-time limits, and server guidance such as `Retry-After`.
6. Make local commands idempotent with stable operation keys and durable attempt state where the provider supports or requires it. For ambiguous outcomes, query status or reconcile instead of repeating a charge or mutation.
7. Treat quotas as shared capacity. Centralize accounting where needed, shed optional work, reserve critical capacity, and monitor provider-specific limit headers without assuming draft or proprietary fields are guarantees.
8. Decouple long or failure-prone work with a queue or workflow. Expose pending, delayed, failed, and manual-review states honestly to users and support.
9. Reconcile local and provider records by stable identifiers, state, amount, timestamps, deletes, and business invariants. Design replay, backfill, correction, and duplicate handling.
10. Test sandbox and controlled failure: timeout before and after provider commit, 429, 5xx, invalid JSON, schema drift, pagination loop, stale token, revoked scope, clock skew, provider outage, duplicate response, and partial batch.

## Delivery Guarantees for Provider Events

When the provider also pushes events, or when polling must stand in for pushes, design for at-least-once delivery: expect duplicates, expect out-of-order arrival, and never treat a single delivery as proof of exactly-once effect.
- Verify signatures on the raw, unparsed body before trusting any event field, using the provider's documented scheme; parse only after verification passes.
- Deduplicate on the provider's event identifier, persisted durably before the effect is applied, so a redelivery cannot repeat a consequential action.
- Enumerate replay paths in the design: provider redelivery, manual operator replay, reconciliation-driven backfill, and dead-letter reprocessing. Each path must pass through the same deduplication and idempotency checks as a first delivery.
- Use [Webhook Integration Design](../webhook-integration-design/SKILL.md) for the inbound webhook contract; this skill owns the outbound adapter and the reconciliation that proves the provider's view matches the local one.

## Required Output

- domain and provider state mapping with source of truth
- version, endpoint, identity, scope, data, network, and dependency inventory
- adapter contract, validation, timeout, concurrency, pagination, and error policy
- retry, idempotency, unknown-outcome, reconciliation, and manual-recovery design
- quota, cost, security, privacy, telemetry, and support controls
- sandbox and failure test evidence
- deprecation monitoring, fallback, export, rollback, and exit plan

## Completion Gate

Do not call the integration ready until ambiguous outcomes cannot silently duplicate consequential work, timeouts and quotas are bounded, reconciliation proves domain invariants, credentials are least privilege, and provider loss has a tested user and operator path.

## Conditional Reference

Read [External API Evidence](references/external-api-evidence.md) when defining HTTP semantics, problem responses, rate-limit handling, or REST security.
