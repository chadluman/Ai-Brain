---
name: service-resilience-design
description: Design or review timeouts, deadlines, cancellation, retries, idempotency, overload protection, bulkheads, degradation, dependency failure, and recovery for networked services. Use when a web backend, worker, API client, queue consumer, or distributed workflow must tolerate partial failure without amplifying it.
---

# Service Resilience Design

## Outcome

Make dependency and overload failures bounded, observable, and recoverable so the system preserves critical user outcomes without turning retries, queues, or failover into a larger outage.

## Required Inputs

- critical journeys, service graph, dependencies, ownership, and user-visible failure budgets
- request and job semantics, side effects, idempotency, transaction boundaries, and delivery guarantees
- latency distributions, concurrency, capacity, queue depth, resource pools, and overload behavior
- dependency SLAs, rate limits, timeout contracts, retry signals, maintenance windows, and failure modes
- availability, durability, recovery, data-loss, regional, cost, and compliance requirements

## Safety and Permission Constraints

- Never retry merely because a call failed or timed out. A timeout does not prove that a side effect did not occur.
- Automatic retries require safe method semantics or an application idempotency and reconciliation contract. Bound attempts, elapsed time, concurrency, and total retry load.
- Do not stack retries independently at every layer. Assign one retry owner per dependency boundary and preserve the caller's deadline.
- Failover and circuit breaking can shift or hide load. Verify destination capacity, stale-state risk, recovery behavior, and operator controls.
- Do not log payloads, credentials, personal data, or high-cardinality identifiers as resilience telemetry by default.
- Chaos, load, failover, traffic shedding, and disaster tests against shared or production systems are R3 and require immediate authorization, blast-radius controls, stop conditions, and rollback.

## Workflow

1. Map the critical call and work graph with synchronous depth, queues, data stores, third parties, resource pools, and failure domains.
2. Classify each operation by idempotency, side effects, reversibility, deadline, criticality, and whether partial success can be reconciled.
3. Allocate an end-to-end latency and deadline budget. Configure connection, request, idle, queue, and transaction timeouts from measured distributions, including setup work.
4. Propagate deadlines and cancellation. Stop downstream work when the result is no longer useful, while protecting required commit or compensation steps.
5. Define retryable conditions narrowly. Use bounded exponential backoff with jitter, honor valid server pushback, cap total elapsed time, and prevent retries from exceeding a shared budget.
6. Add stable idempotency keys or equivalent deduplication for retryable side effects. Store outcomes long enough for the retry horizon and reconcile ambiguous completion.
7. Protect resources with bounded queues, concurrency limits, admission control, connection pools, bulkheads, load shedding, and fast rejection before exhaustion.
8. Define graceful degradation and stale or partial response rules per journey. Do not present incomplete data as authoritative or relax authorization during failure.
9. Design circuit states, probes, recovery ramps, failover, and fallback so recovery traffic does not stampede a weak dependency.
10. Instrument original calls separately from attempts. Measure timeout source, retry count, retry success, rejected load, queue delay, saturation, cancellation, fallback, and user outcome.
11. Test slow, failed, flapping, overloaded, corrupt, partial, and recovered dependencies at realistic concurrency. Include retry storms, queue growth, cold recovery, deploy overlap, and loss of observability.
12. Document operator controls, kill switches, runbooks, ownership, capacity assumptions, dependency contacts, and post-incident learning triggers.

## Required Output

- dependency and failure-domain map
- deadline, timeout, cancellation, and retry ownership matrix
- idempotency, ambiguous-outcome, and reconciliation design
- admission, queue, pool, overload, bulkhead, circuit, and degradation policy
- failure-injection and recovery evidence with load and user outcomes
- telemetry, alerts, operator controls, runbooks, and residual risks

## Completion Gate

Do not call the design resilient until controlled tests show that dependency slowness, failure, overload, retry, failover, and recovery remain within defined resource and user-impact bounds, with no duplicate irreversible effect or unbounded queue or retry growth.

## Conditional Reference

Read [Service Resilience Evidence](references/service-resilience-evidence.md) before choosing retry or timeout defaults. Use [Background Job and Queue Design](../background-job-queue-design/SKILL.md), [External API Integration](../external-api-integration/SKILL.md), and [Capacity and Cost Planning](../capacity-cost-planning/SKILL.md) for their respective boundaries.
