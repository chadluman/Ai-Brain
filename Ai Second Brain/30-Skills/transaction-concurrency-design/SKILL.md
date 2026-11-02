---
name: transaction-concurrency-design
description: Design or review transactions, isolation, optimistic or pessimistic concurrency, locks, retries, uniqueness, invariants, deadlocks, and cross-system consistency. Use when simultaneous commands can corrupt state, duplicate value, oversell inventory, or violate workflow rules.
---

# Transaction and Concurrency Design

## Outcome

Preserve explicit business invariants under real concurrent execution, retries, crashes, and partial failure using the narrowest correct database and application controls.

## Required Inputs

- commands, entities, invariants, state transitions, and ownership boundaries
- read and write sets, contention keys, workload, latency, availability, and scale
- datastore and exact version, isolation defaults, constraint, transaction, and lock behavior
- external effects, queues, caches, replicas, jobs, clocks, and retry sources
- failure consequences, audit, reconciliation, repair, and operator needs

## Safety and Permission Constraints

- Do not assume a transaction name, ORM method, or default isolation preserves application invariants. Verify exact engine and version semantics.
- Prefer database constraints and atomic operations for invariants the database owns. Application checks without protected writes are race-prone.
- Keep network calls and slow user work outside database transactions unless a proven protocol requires otherwise; long transactions amplify locks and failure.
- Bound retries, locks, wait time, transaction length, and batch size. Retrying without idempotency can duplicate external or local effects.
- Production isolation changes, locking migrations, bulk corrections, or repair of financial, authorization, or user-owned state is R3 and requires authorization, backup, reconciliation, and rollback.

## Workflow

1. State each invariant in domain terms and identify the smallest authoritative boundary capable of enforcing it.
2. Draw concurrent histories for competing commands, duplicates, reordering, stale reads, retries, crash points, and external callbacks. Find the interleavings that break the invariant.
3. Verify the deployed engine's isolation, snapshot, constraint, lock, deadlock, replica, and serialization-failure behavior from current documentation and a focused test.
4. Start with declarative uniqueness, foreign key, check, exclusion, or conditional constraints where they express the rule. Validate existing data before enforcement.
5. Choose atomic update, compare-and-swap or version column, row lock, advisory lock, serializable transaction, or single-writer queue based on contention, scope, and failure cost.
6. Define transaction boundaries and a total lock order. Keep them short, touch rows deterministically, set appropriate timeouts, and surface conflicts rather than silently overwriting.
7. Retry only complete retry-safe transactions on documented transient or serialization failures, with jitter and a deadline. Regenerate reads inside each retry.
8. Separate external effects with an outbox, inbox, saga, or reconciliation process. Never claim atomicity across systems without a protocol that actually provides it.
9. Monitor conflicts, serialization failures, deadlocks, wait time, transaction age, constraint failures, duplicate operations, reconciliation gaps, and repair actions.
10. Test barrier-synchronized races, high contention, process crash before and after commit, duplicate messages, stale replicas, failover, lock timeout, deadlock, and retry exhaustion.

## Required Output

- invariant and authoritative-boundary register
- concurrent histories and identified failure interleavings
- engine-version isolation, constraint, lock, and retry evidence
- selected concurrency control per command with rationale
- transaction, lock-order, timeout, retry, and idempotency policy
- cross-system effect, reconciliation, monitoring, and repair plan
- deterministic race and failure test results

## Completion Gate

Do not call concurrency correct until adversarial interleavings preserve every material invariant, retries cannot duplicate effects, deadlocks and conflicts have bounded handling, and cross-system gaps are observable and repairable.

## Conditional Reference

Read [Transaction and Concurrency Evidence](references/transaction-concurrency-evidence.md) when choosing isolation, locks, constraints, or retry behavior.
