---
name: teach-web-data-engineering
description: Teach data engineering for web applications through modeling, storage choice, constraints, transactions, caching, search, migrations, retention, and recovery. Use for database lessons, data-heavy full-stack projects, schema reviews, or reliability exercises.
---

# Teach Web Data Engineering

## Outcome

Help the learner translate domain invariants and access patterns into durable, testable data behavior, including safe change and recovery.

Follow the shared [lesson contract](../teach-senior-web-development/references/lesson-contract.md).

## Route Supporting Knowledge

- [Data Store Selection](../data-store-selection/SKILL.md) when choosing primary or specialized storage.
- [Relational Data Modeling](../relational-data-modeling/SKILL.md) for identities, relationships, constraints, indexes, history, and schema evolution.
- [Transaction and Concurrency Design](../transaction-concurrency-design/SKILL.md) for races, isolation, locks, retries, and external effects.
- [Cache and Consistency Design](../cache-consistency-design/SKILL.md) and [Search Architecture Selection](../search-architecture-selection/SKILL.md) when reads require those specialized paths.
- [Data Migration Design](../data-migration-design/SKILL.md) for backfills, cutovers, reconciliation, and rollback.
- [Backup and Disaster Recovery](../backup-disaster-recovery/SKILL.md), [Privacy and Data Governance](../privacy-data-governance/SKILL.md), and [Data Retention and Deletion Operations](../data-retention-deletion-operations/SKILL.md) for lifecycle and recovery.

## Teaching Priorities

Start with facts, invariants, ownership, sensitivity, lifecycle, and access patterns before tables or vendor features. Make constraints and failure semantics observable with example data and negative tests. Teach query plans and indexes from representative reads and writes rather than rules of thumb.

Use exercises involving duplicate input, missing references, concurrent updates, stale caches, partial migrations, deletion, and restore. Keep seed data synthetic and small enough to understand, then explain which conclusions require representative scale.

For senior-level practice, require a data-flow sketch, explicit consistency choices, migration compatibility window, reconciliation method, backup or export path, and a strategy for leaving a provider.

## Boundaries

- Do not select a store from habit, popularity, or a toy benchmark.
- Do not confuse application validation with database integrity or a successful backup job with a verified restore.
- Schema changes, destructive migrations, production queries, real personal data, and provider provisioning retain their normal review and authorization requirements.
- Label synthetic-data and small-scale results; do not generalize performance claims without representative measurements.

## Completion

The learner can explain the model and invariants, demonstrate positive and negative behavior, reason about concurrency and consistency, show a safe change or recovery path, and name the workload or policy evidence still required for production.
