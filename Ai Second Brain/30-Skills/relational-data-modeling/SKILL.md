---
name: relational-data-modeling
description: Design or review a relational database schema from domain identity, invariants, relationships, lifecycle, query patterns, tenancy, history, and migration needs. Use when creating or changing tables, keys, constraints, indexes, audit history, soft deletion, or relational ownership boundaries.
---

# Relational Data Modeling

## Outcome

Create a relational model that represents domain facts clearly, enforces durable invariants in the database where appropriate, supports required access paths, and can evolve without ambiguous ownership or silent corruption.

## Required Inputs

- domain concepts, terminology, lifecycle, ownership, identity, and business invariants
- create, read, update, delete, history, reporting, search, and bulk-access patterns
- relationship cardinality, optionality, ordering, uniqueness, tenancy, and authorization boundaries
- expected volume, growth, retention, archival, deletion, restore, and migration needs
- concurrency, transaction, latency, availability, replication, and consistency requirements
- selected database engine and exact version, or candidate engines if selection is pending

## Safety and Permission Constraints

- Do not encode security, money, inventory, entitlements, uniqueness, or referential invariants only in application code when the database can enforce them atomically.
- Do not use a mutable display value, email address, external provider identifier, or unscoped sequence as a universal identity without documenting lifecycle and collision behavior.
- Treat nullable, defaulted, generated, cascaded, soft-deleted, historical, and derived values as explicit semantic decisions. Convenience defaults can manufacture false facts.
- Avoid storing credentials, access tokens, or unnecessary personal data. Classify sensitive columns and align retention, encryption, access, backup, export, and deletion controls.
- Database extensions, migration tools, ORMs, generators, and schema packages are executable assets requiring exact-version review.
- Production schema changes, backfills, destructive cascades, data merges, and retention deletion are R3 actions requiring immediate authorization, backups, reconciliation, and rollback or forward-repair plans.

## Workflow

1. Write the domain facts and invariants in plain language before tables. Identify aggregates, owners, identities, state transitions, and facts that require history.
2. Model entities, value objects, reference data, associative relationships, and events. Resolve many-to-many relationships and distinguish absence, unknown, not applicable, and empty.
3. Choose stable primary keys and scoped natural or business keys. Define tenant participation in every relevant key and relationship.
4. Select the narrowest semantically correct types, units, precision, time-zone behavior, collation, and encoding. Avoid lossy money, timestamp, identifier, and measurement representations.
5. Encode row and relationship invariants with `NOT NULL`, `CHECK`, `UNIQUE`, primary, foreign, exclusion, or engine-equivalent constraints. State what cannot be enforced declaratively and where it is protected.
6. Define update and delete semantics for every relationship. Use cascade only when dependent lifecycle ownership is unambiguous and bounded.
7. Normalize to remove update anomalies, then denormalize only for a measured read or operational need with an owner and reconciliation strategy.
8. Derive indexes from representative predicates, joins, ordering, uniqueness, and access-control filters. Check write cost, size, selectivity, left-prefix behavior, and redundant indexes with actual plans.
9. Design concurrency and transaction boundaries for cross-row invariants, counters, reservations, ledgers, state transitions, and idempotency.
10. Define history, audit, temporal behavior, soft deletion, retention, archival, tenant export, erasure, backup, and restore semantics.
11. Create an expand, migrate, verify, and contract plan for each breaking change. Test old and new application versions, rollback or forward repair, and restored data.
12. Validate with representative and adversarial fixtures, constraint violations, concurrent writes, query plans, scale estimates, migrations, backup restore, and data-quality queries.

## Required Output

- domain glossary, entity and relationship model, and invariant catalog
- keys, types, nullability, defaults, constraints, and lifecycle semantics
- representative queries and evidence-backed index plan
- transaction and concurrency boundaries
- tenancy, authorization, sensitive-data, history, retention, and deletion model
- migration, backfill, compatibility, reconciliation, restore, and rollback plan
- test fixtures, query plans, and observed integrity evidence

## Completion Gate

Do not call the schema ready until critical invariants fail closed in realistic tests, representative queries have acceptable plans, concurrent operations preserve the model, and an isolated migration plus restore has reconciled expected counts and domain facts.

## Conditional Reference

Read [Relational Data Modeling Evidence](references/relational-data-modeling-evidence.md) before selecting constraint or index patterns. Use [Data Store Selection](../data-store-selection/SKILL.md), [Transaction and Concurrency Design](../transaction-concurrency-design/SKILL.md), and [Data Migration Design](../data-migration-design/SKILL.md) at their respective boundaries.
