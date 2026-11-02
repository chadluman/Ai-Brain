# Storage Evidence

Verified 2026-10-21. Product behavior varies by version, configuration, topology, and managed provider; verify the exact deployment under consideration.

## Relational Examples

- [PostgreSQL MVCC](https://www.postgresql.org/docs/current/mvcc-intro.html) documents snapshot-based concurrency and transaction isolation. The current documentation also explains explicit locks and serializable behavior; applications must still handle conflicts and serialization failures correctly.
- [PostgreSQL Backup and Restore](https://www.postgresql.org/docs/current/backup.html) distinguishes SQL dumps, file-system backups, and continuous archiving. Select and test a method against actual recovery objectives.
- [SQLite appropriate uses](https://www.sqlite.org/whentouse.html) distinguishes local application storage from client/server databases. It highlights simplicity and local operation while noting constraints for many direct network clients, write-intensive multi-server systems, and high write concurrency.

These are useful contrasting primary sources, not a universal two-product shortlist.

## Candidate Evidence Checklist

For every database, cache, search service, object store, warehouse, or queue verify from current official sources:

- supported exact version, license, end-of-life policy, and security channel
- consistency, transactions, concurrency, limits, durability, and failure semantics
- backup scope, point-in-time behavior, restore process, replication, and regional recovery
- authentication, authorization, encryption, audit, residency, retention, and deletion
- import, export, migration, portability, quotas, pricing dimensions, and egress
- client and driver dependencies, compatibility, connection behavior, and observability

Benchmark the project's workload and failure cases. Vendor throughput numbers and small synthetic tests are not evidence for a different schema, access pattern, or topology.
