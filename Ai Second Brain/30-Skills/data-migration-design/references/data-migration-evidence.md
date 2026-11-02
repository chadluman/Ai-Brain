# Data Migration Evidence

Verified: 2026-10-21

## Primary and Industry Sources

- [Google SRE: Data Integrity](https://sre.google/sre-book/data-integrity/) treats schema changes, zero-downtime migrations, evolving integrations, corruption detection, and recovery as user-visible data-integrity work. Its concrete practices must be adapted to the actual datastore and organization.
- [PostgreSQL current logical replication](https://www.postgresql.org/docs/current/logical-replication.html) documents publication and subscription, initial snapshot copy, subsequent change replication, identity requirements, and security considerations for current PostgreSQL.
- [PostgreSQL current SQL dump](https://www.postgresql.org/docs/current/backup-dump.html) documents logical dumps, restore behavior, cluster-wide objects, error handling, transaction tradeoffs, and post-restore analysis.
- [PostgreSQL current `ALTER TABLE`](https://www.postgresql.org/docs/current/sql-altertable.html) documents operation-specific locking and lower-impact constraint-validation patterns. Exact effects depend on the deployed major version, schema, and workload.

## Decision Boundaries

- PostgreSQL documentation is direct product evidence, not a portable recipe for other engines. Verify exact target-version locking, replication, DDL, backup, and restore semantics.
- Logical replication moves selected data changes but does not automatically migrate every schema object, role, extension, sequence state, large object, or application invariant.
- Dual writes create a distributed-consistency problem. Prefer a single authoritative write plus an outbox or change stream when it satisfies latency and availability needs.
- A successful command, empty error log, or matching row count is not sufficient reconciliation evidence.
- Rollback may become more dangerous than roll-forward once new-format writes or external side effects occur. Define the decision point in advance.
