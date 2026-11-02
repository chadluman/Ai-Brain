---
name: data-retention-deletion-operations
description: Design or review data retention schedules, legal or preservation holds, logical deletion, derived-data cleanup, vendor deletion, backup expiry, media sanitization, restore safeguards, and evidence of disposal. Use when privacy or product policy must become reliable deletion behavior across all copies.
---

# Data Retention and Deletion Operations

## Outcome

Produce an enforceable data-lifecycle system in which every data class has a justified retention clock, holds prevent improper destruction, deletion propagates to all known copies, restores do not resurrect expired data, physical media is sanitized appropriately, and evidence proves process without retaining the deleted content.

Use [Privacy and Data Governance](../privacy-data-governance/SKILL.md) for purpose and qualified legal decisions, [Backup and Disaster Recovery](../backup-disaster-recovery/SKILL.md) for recovery, [Audit Log Design](../audit-log-design/SKILL.md) for evidence, and [Data Migration Design](../data-migration-design/SKILL.md) for store changes. This skill owns operational retention and deletion.

## Required Inputs

- data classes, purposes, subjects, tenants, sensitivity, authoritative owners, identifiers, relationships, regions, and applicable qualified retention or hold decisions
- primary stores, replicas, caches, indexes, search, analytics, logs, traces, files, object versions, event streams, exports, models, derived data, devices, vendors, and support systems
- creation, last-use, account-close, contract-end, consent-withdrawal, case-close, incident, and other retention-clock triggers
- backup topology, snapshots, point-in-time logs, immutable storage, archives, restore flow, media and device lifecycle, and provider deletion capabilities
- user request, tenant offboarding, batch expiry, incident deletion, correction, hold, appeal, audit, monitoring, failure, cost, and operator constraints

## Safety and Permission Constraints

- Retention periods and legal holds require qualified authority for the applicable jurisdiction and contract. Do not invent a period or delete data because a generic source suggests one.
- Deletion is destructive R3 work in production. Require exact scope, authority, current backup and hold state, dry-run or preview, abort conditions, reconciliation, and accountable approval immediately before execution.
- Do not delete or alter data subject to an active preservation, legal, safety, fraud, financial, or incident hold. Restrict held data from unrelated use and record who placed, reviewed, and released the hold.
- Logical deletion, encryption-key destruction, anonymization, backup expiry, and media sanitization are different controls. State which one applies and what remains recoverable or linkable.
- Never keep deleted content inside evidence, logs, queues, error reports, tickets, or tombstones. Evidence should use safe identifiers, policy version, counts, timestamps, outcomes, and authorized exceptions.

## Workflow

1. Build a data-copy graph from creation through every store, derivative, export, model, vendor, device, log, backup, archive, and deletion path. Assign owner and authoritative identifier to each copy.
2. Create a versioned retention schedule by data class and purpose with trigger, duration or review rule, authority, exceptions, hold interaction, disposal method, evidence, owner, and re-evaluation date. Remove “keep indefinitely” defaults without explicit justification.
3. Define lifecycle states such as active, inactive, expiry-pending, held, deletion-requested, deleting, deleted, failed, and restored-pending-reconciliation. Specify allowed reads, writes, derivations, exports, and reversals in each state.
4. Centralize or consistently distribute expiry decisions using trusted time and immutable policy version. Make deletion jobs idempotent, bounded, restartable, rate-controlled, tenant-aware, and observable; prevent concurrent writers from recreating expired records.
5. Order deletion around references and derivations: revoke access, stop new processing, remove or anonymize primary data as authorized, propagate tombstones or commands, clear caches and indexes, update aggregates or models, request vendor deletion, and reconcile every target.
6. Handle backups through scheduled expiry and restore controls rather than silently modifying immutable sets when infeasible. Document maximum residual window, restrict use, and reapply tombstones and current retention immediately after restore before serving users.
7. Implement holds with scoped subject, data classes, reason, authority, start, review, expiry or release, and audit. Holds pause destruction but do not grant broader access or new use.
8. Choose sanitization for retired physical or virtual media from data sensitivity, medium, reuse, provider assurance, encryption and key custody. Verify method and disposition separately from application-record deletion.
9. Reconcile by eligible, deleted, held, failed, missing, vendor-pending, backup-pending, and unexpectedly recreated records. Alert on backlog age, repeated failure, new unregistered stores, hold expiry, restore resurrection, and policy drift.
10. Test ordinary expiry, user or tenant deletion, partial failure, duplicate request, active hold, hold release, identifier collision, concurrent write, vendor outage, backup restore, event replay, cache and search residue, analytics derivative, media retirement, false deletion, and authorized recovery where policy permits.

## Required Output

- data-copy graph and versioned retention schedule with qualified-authority boundary
- lifecycle state machine, hold design, deletion orchestration, vendor and derived-data propagation, and retry behavior
- backup expiry and post-restore anti-resurrection controls plus media sanitization decision
- safe evidence schema, reconciliation, dashboards, alerts, exception, incident, rollback or recovery, and policy-change migration plan
- realistic expiry, hold, deletion, failure, restore, residue, and tenant-isolation test evidence

## Completion Gate

Do not call retention and deletion operational until every registered data class and copy has a justified rule and owner, holds block destruction without broadening use, deletion is idempotent and reconciles across derived and vendor systems, backup residual windows are disclosed and tested, restore reapplies deletions before access, media disposal is verified where applicable, and evidence does not preserve the deleted content.

## Conditional Reference

Read [Data Retention and Deletion Evidence](references/data-retention-deletion-evidence.md) when distinguishing policy from implementation, logical deletion from sanitization, or designing backup and evidence behavior.
