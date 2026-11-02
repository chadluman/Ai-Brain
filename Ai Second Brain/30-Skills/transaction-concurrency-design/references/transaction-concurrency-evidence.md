# Transaction and Concurrency Evidence

Verified: 2026-10-21

## Product and Academic Sources

- [PostgreSQL current transaction isolation](https://www.postgresql.org/docs/current/transaction-iso.html) documents the exact anomalies and retry requirements of current `Read Committed`, `Repeatable Read`, and `Serializable` behavior.
- [PostgreSQL current explicit locking](https://www.postgresql.org/docs/current/explicit-locking.html) documents table, row, page, deadlock, and advisory-lock behavior. Lock names do not always indicate granularity, so use the compatibility rules and exact operation documentation.
- [PostgreSQL current `SET TRANSACTION`](https://www.postgresql.org/docs/current/sql-set-transaction.html) documents isolation, read-only, deferrable, and snapshot characteristics and notes that PostgreSQL maps `READ UNCOMMITTED` to `READ COMMITTED`.
- [MIT 6.102 Concurrency](https://web.mit.edu/6.102/www/sp26/classes/14-concurrency/) defines race conditions through specifications and invariants whose correctness depends on event timing.

## Decision Boundaries

- PostgreSQL documentation is authoritative only for the deployed PostgreSQL major version and configuration. Other engines can use the same isolation name with different behavior.
- Serializable execution can abort transactions; applications must safely retry the whole unit of work. It does not make external side effects atomic.
- Explicit locks can protect a known contention point but increase blocking and deadlock risk. Establish deterministic order and time bounds.
- Tests that run concurrent operations without coordinating their critical interleaving can pass without exercising the race. Use barriers, repeated stress, and invariant checks.
