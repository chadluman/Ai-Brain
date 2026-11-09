---
name: data-migration-design
description: Plan and review schema changes, backfills, store or provider migrations, dual writes, replication, reconciliation, cutovers, and rollback while preserving data integrity and availability. Use when changing persistent data shape, ownership, engine, region, or source of truth.
---

# Data Migration Design

## Outcome

Produce a reversible, observable migration that preserves defined invariants, authorization, history, privacy, and availability, with reconciliation proving what moved rather than relying on job success.

## Required Inputs

- source and target schemas, stores, versions, owners, regions, and trust boundaries
- data volume, growth, relationships, invariants, sensitivity, retention, and legal holds
- read and write paths, clients, integrations, caches, indexes, jobs, and reporting dependencies
- downtime, consistency, RPO, RTO, performance, cost, and completion requirements
- backup, restore, export, deletion, observability, and operator capacity

## Safety and Permission Constraints

- Treat migrations as data-changing R3 work in production. Require immediate authorization, current restore evidence, exact target, dry-run results, abort conditions, and accountable command.
- Never use record count alone as integrity evidence. Reconcile keys, values, relationships, aggregates, constraints, permissions, deletes, and sampled or complete checksums appropriate to risk.
- Backups are not rollback until a restore fits the required time and data-loss window. Schema, code, queues, external effects, and new writes may make restore insufficient.
- Minimize copied personal data and temporary artifacts; encrypt, restrict, expire, audit, and delete them according to policy.
- Avoid irreversible destructive cleanup until the target has operated through the agreed observation period and rollback is deliberately retired.

## Workflow

1. Define invariants and the authoritative source at every phase. Inventory readers, writers, derived stores, caches, indexes, exports, jobs, and external consumers.
2. Profile source quality and size using safe read-only methods. Quantify invalid, duplicate, missing, orphaned, stale, and policy-incompatible records.
3. Choose offline cutover, expand-and-contract, backfill plus change capture, replication, or another pattern from downtime, write rate, consistency, and tool evidence.
4. Make schema changes backward compatible first. Deploy tolerant readers, then writers, then backfill in resumable bounded batches with checkpoints and idempotency.
5. Define transformations as versioned deterministic rules. Preserve stable identifiers and provenance; quarantine ambiguous records instead of silently coercing them.
6. Reconcile continuously with counts by partition, key coverage, constraints, hashes or aggregates, authorization attributes, delete markers, and business invariants.
7. Observe lag, errors, locks, latency, load, storage, queue depth, and cost. Throttle or stop before user-facing or recovery capacity is consumed.
8. Cut reads and writes separately when possible, with canary cohorts or shadow comparison. Freeze or coordinate writes when correctness cannot tolerate convergence delay.
9. Keep a tested rollback or roll-forward path, including application versions and queued events. Record the point beyond which rollback changes to compensating migration.
10. After an observation window, reconcile again, retire old writers, revoke credentials, archive required evidence, delete temporary copies, and explicitly approve source retirement.

## PostgreSQL Expand-and-Contract

For PostgreSQL schema changes, use expand-and-contract: add the new shape first, dual-write or backfill, move readers, then remove the old shape in a later release. Keep each statement short-lived and non-blocking:

- Set a `lock_timeout` on migration sessions so a blocked DDL statement fails fast instead of queueing behind long transactions and blocking new work.
- Build new indexes with `CREATE INDEX CONCURRENTLY` so index creation does not take a write-blocking lock on the table.
- Add new constraints as `NOT VALID`, backfill or validate existing rows separately, then `VALIDATE CONSTRAINT` — validating does not block writes the way adding a validated constraint does.
- Backfill in bounded batches of roughly 1,000–5,000 rows per transaction, with checkpoints and resumability, so a backfill does not hold long transactions, bloat the write-ahead log, or starve live traffic; throttle or pause when latency or replication lag rises.

## Required Output

- source-target map, invariants, ownership, and dependency inventory
- migration pattern, state machine, compatibility sequence, and data transformations
- batch, checkpoint, retry, replication, and throttling design
- reconciliation queries or rules and acceptance thresholds
- backup and restore evidence, rollback or roll-forward plan, and abort criteria
- cutover timeline, monitoring, communications, approvals, and cleanup gates
- final integrity and deletion evidence

## Completion Gate

Do not call a migration complete until defined invariants reconcile, all intended readers and writers use the target, lag and error queues are resolved, rollback retirement is approved, and temporary data plus obsolete access are removed according to policy.

## Conditional Reference

Read [Data Migration Evidence](references/data-migration-evidence.md) when choosing online or offline patterns, backup and restore behavior, replication, or reconciliation depth.
