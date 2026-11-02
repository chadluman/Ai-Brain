---
name: api-abuse-resource-controls
description: Design or review API quotas, admission, rate and concurrency limits, cost and resource bounds, automation defenses, sensitive-flow controls, fair-use behavior, client feedback, and abuse operations. Use when an API or business flow can be exhausted or automated harmfully; do not treat a single per-IP rate limit as complete protection.
---

# API Abuse and Resource Controls

## Outcome

Produce layered controls that keep legitimate journeys usable while bounding compute, data, paid side effects, scarce inventory, and harmful automation across identities and distributed traffic.

## Required Inputs

- endpoints and business flows, actors, authentication states, tenants, objects, resources, downstream calls, side effects, and abuse incentives
- legitimate request, burst, batch, pagination, upload, fan-out, query, concurrency, latency, and retry distributions
- CPU, memory, connection, worker, database, storage, bandwidth, email, SMS, payment, identity, AI, search, and third-party cost drivers
- user, tenant, credential, device, IP, network, session, token, object, destination, and behavioral signals with privacy and accessibility constraints
- service tiers, contractual quotas, safety margins, degradation policy, support and appeal, incident response, and cost limits

## Safety and Permission Constraints

- Rate limits do not replace authentication, authorization, invariant checks, fraud controls, capacity planning, or denial-of-service protection. Enforce object and function authorization independently.
- Do not block or profile solely from fragile identifiers such as IP address, user agent, disability-related interaction patterns, or geography. Consider shared networks, IPv6, privacy relays, travel, assistive technology, and false-positive harm.
- Avoid revealing sensitive capacity, identity, fraud, or detection details in response headers and errors. Client hints are advisory and can be stale, spoofed, cached, or used for reconnaissance.
- Never make paid or scarce downstream calls before cheap validation and admission. Use budgets and idempotency around email, SMS, payments, identity checks, AI, media, and other billable effects.
- Load tests, traffic blocks, production throttling, account restrictions, provider quota changes, or automated enforcement are R3 and require authorization, blast-radius and fairness review, stop conditions, rollback, and support readiness.

## Workflow

1. Map resources and abuse cases per endpoint and end-to-end business flow. Include reads, writes, searches, exports, authentication, recovery, signup, promotions, reservations, messaging, checkout, refunds, uploads, webhooks, batch and graph operations.
2. Measure normal demand and the marginal resource or cost amplification of parameters, nesting, fan-out, pagination, retries, cache misses, files, recipients, destinations, and downstream providers.
3. Place cheap hard bounds at parsing and validation: body and header size, field count, string length, nesting, batch size, page size, query complexity, upload type and size, output size, timeout, and total work.
4. Define multi-dimensional budgets by authenticated principal and tenant first, then supplement with credential, session, device, network, object, destination, and global signals. Bind counters to the operation and scarce resource they protect.
5. Choose algorithms and storage from required burst tolerance, fairness, distribution, consistency, failure mode, and cost. Treat token bucket, leaky bucket, fixed or sliding windows, concurrency semaphores, queues, and reservations as tools with different semantics.
6. Protect sensitive business flows with state and inventory controls: eligibility, cooldown, idempotency, uniqueness, per-object and per-destination caps, reservation expiry, proof or friction proportional to risk, manual review, and recovery.
7. Enforce admission before expensive work and at downstream boundaries. Cap concurrency and queue depth, assign retry ownership, shed low-priority work, preserve critical paths, and avoid retry storms when clients receive rejection.
8. Return standards-based errors where useful. RFC 6585 defines `429` and optional `Retry-After`; current IETF RateLimit fields are still a draft. Version any adopted header contract and do not promise quota that capacity or policy may revoke.
9. Monitor allowed, delayed, rejected, challenged, abandoned, retried, appealed, and successful outcomes by flow and cohort. Track resource saturation, cost, distributed evasion, false positives, support load, and displacement to other paths.
10. Test shared networks, IPv6 rotation, multiple accounts and credentials, concurrency, bursts, slow requests, batches, expensive parameters, object and destination distribution, counter-store outage, clock skew, fail-open and fail-closed behavior, retries, accessibility, and recovery after restriction.

## Required Output

- endpoint and business-flow abuse map with resource and cost amplification
- hard input, output, time, batch, complexity, concurrency, queue, and downstream budgets
- identity and dimension strategy, algorithms, counter state, consistency, privacy, and failure policy
- sensitive-flow state, idempotency, inventory, challenge, review, appeal, and recovery controls
- client error and header contract with draft or standard status recorded
- staged test evidence, thresholds, dashboards, alerts, operator controls, rollback, and tuning plan

## Completion Gate

Do not call the controls ready until distributed and authenticated abuse cases remain within declared resource and cost bounds, authorization still protects every object and function, paid effects occur only after admission, counter failure is safe, legitimate bursts and shared users remain usable, false-positive recovery works, and load or adversarial tests pass at controlled scope.

## Conditional Reference

Read [API Abuse and Resource Evidence](references/api-abuse-resource-evidence.md) when defining threat coverage, HTTP feedback, resource bounds, or draft RateLimit header behavior.
