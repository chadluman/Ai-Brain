---
name: cache-consistency-design
description: Design or review browser, CDN, reverse-proxy, application, database, and computed-result caching with explicit keys, freshness, validation, invalidation, tenant safety, stampede control, observability, and fallback. Use when caching could improve latency, availability, or cost; do not cache merely because a platform offers it.
---

# Cache and Consistency Design

## Outcome

Introduce caching only where stale-data tolerance and invalidation are explicit, so performance gains do not leak data, violate authorization, or hide incorrect state.

## Required Inputs

- source of truth, read and write paths, object identity, and update frequency
- users and tenants, authentication, personalization, locale, device, and content negotiation
- acceptable staleness, consistency, latency, availability, and recovery objectives
- traffic shape, object size, cost, dependency capacity, and geographic needs
- every cache layer, owner, eviction behavior, and purge capability

## Safety and Permission Constraints

- Default sensitive, user-specific, authorization-dependent, and mutable financial responses to non-shared caching until a complete key and policy are proven.
- A cache hit must never bypass current authorization. Include all representation-changing and security-relevant dimensions in the key or do not share the response.
- Never store secret values, raw credentials, or prohibited personal data in caches, cache metadata, traces, or debug output.
- Bound memory, object size, key cardinality, lifetime, retries, and origin concurrency. Plan for a cold cache and cache outage.
- Production-wide purge, key migration, TTL change, or enabling shared caching on protected data is R3 and requires immediate authorization and rollback.

## Workflow

1. Measure the uncached bottleneck and define the intended benefit. Prefer query, algorithm, payload, or architecture fixes when caching would mask the cause.
2. Inventory every cache between client and source of truth, including implicit framework, browser, CDN, DNS, service, ORM, and database caches.
3. Classify each response or value by ownership, sensitivity, authorization, mutability, and tolerated staleness.
4. Define canonical keys and variants for tenant, subject or policy scope, resource version, locale, encoding, query, feature flag, schema, and other material dimensions.
5. Choose freshness and validation: immutable versioned content, explicit TTL, conditional validation, write-through, cache-aside, event invalidation, or no cache. State the inconsistency window.
6. Design invalidation and deletion propagation before population. Make late or duplicate invalidation safe and support versioned namespace changes.
7. Prevent stampedes with request coalescing, bounded concurrency, jittered expiry, background refresh, and controlled stale serving only where correctness permits.
8. Define negative-cache and error-cache policy carefully. Do not turn transient authorization, outage, or not-found results into long-lived truth.
9. Observe hit and miss rates, age, evictions, key cardinality, origin load, refresh errors, stale serves, purge latency, data leakage, and cost.
10. Test cross-user and cross-tenant isolation, `Vary` behavior, write races, invalidation loss, stale and expired content, cold start, outage, stampede, deletion, and rollback.

## Current Platform Note (2026)

- Where Redis backs the cache, note that Redis 8 folds the former Redis Stack modules into core. Check whether a capability that previously needed a module is now in core before adding a separate component or dependency.
- Treat cache-population and invalidation consumers as at-least-once: apply invalidations idempotently, using idempotency keys where the consumer supports them, so a redelivered invalidation is safe. This makes the delivery assumption behind step 6 explicit; it does not change the step.

## Required Output

- measured caching objective and source-of-truth map
- cache-layer inventory and data classification
- key, variant, freshness, validation, and invalidation specification
- consistency and stale-serving contract
- stampede, outage, privacy, authorization, and capacity controls
- metrics, alerts, failure tests, purge, and rollback plan

## Completion Gate

Do not call the cache ready until cross-user isolation, invalidation, cold-cache behavior, dependency outage, and stampede tests pass, and the observed benefit exceeds operational and correctness cost.

## Conditional Reference

Read [Cache Evidence](references/cache-evidence.md) when defining HTTP freshness, validators, stale behavior, or overload controls.
