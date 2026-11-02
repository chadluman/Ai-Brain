---
name: mobile-offline-sync
description: Design or review durable offline reads, offline writes, synchronization, conflict handling, local persistence, and background retry behavior for iOS, Android, or cross-platform mobile apps. Use when a mobile journey must survive intermittent connectivity, process death, duplicate delivery, or multi-device edits.
---

# Mobile Offline Sync

## Outcome

Define an offline and synchronization model that preserves user intent and data invariants when connectivity, process lifetime, delivery order, and device state are unreliable.

## Required Inputs

- target platforms, minimum OS versions, framework, supported devices, and account model
- journeys that must work offline and the acceptable age, completeness, and latency of local data
- entities, relationships, invariants, write criticality, and multi-device or multi-user edit patterns
- server capabilities for change tracking, idempotency, versions, tombstones, clocks, and partial synchronization
- data sensitivity, storage duration, encryption, backup, logout, revocation, deletion, and device-loss requirements
- expected data volume, attachment sizes, battery constraints, metered-network behavior, and background limits

## Safety and Permission Constraints

- Never treat connectivity or background execution as guaranteed. A queued operation must remain understandable and recoverable after cancellation, process death, reboot, and long delay.
- Do not use last-write-wins by default for money, inventory, permissions, identity, legal records, or other invariant-bearing data. Define server-authoritative validation and conflict behavior.
- Minimize sensitive local data. Classify whether it may enter OS backups, logs, notifications, screenshots, caches, or shared storage.
- Do not store reusable secrets in an ordinary application database. Route credential storage through reviewed platform facilities and the project's threat model.
- Sync engines, database packages, cloud SDKs, and background-work libraries are executable assets requiring exact-version review before adoption.
- Production data migration, destructive conflict repair, remote deletion, and account-wide resynchronization are R3 actions requiring immediate authorization and rollback evidence.

## Workflow

1. Classify each journey as online-required, offline-readable, offline-creatable, or fully offline-editable. State what the user sees when data is stale or incomplete.
2. Define one observable local source of truth for UI reads. Separate local persistence, synchronization orchestration, and remote transport responsibilities.
3. Model the operation journal or change set with stable operation IDs, entity IDs, base versions, causal metadata when needed, retry state, and user-visible status.
4. Specify write policy per operation: online-only, queued, optimistic, or locally committed. Define validation, compensation, cancellation, and irreversible boundaries.
5. Define merge behavior per field or aggregate. Include concurrent update, delete-versus-update, identity remap, attachment, permission change, clock skew, and schema-version cases.
6. Make remote mutations idempotent and retryable. Use bounded backoff and jitter, distinguish transient from permanent failure, and prevent concurrent drainers from violating order or invariants.
7. Design incremental synchronization with cursors, change tokens, tombstones, pagination, checkpointing, full-resync fallback, and detection of missed or invalidated history.
8. Select platform background mechanisms only after checking current constraints. Foreground resume and explicit user refresh must remain valid recovery paths.
9. Define local schema migration, logout, account switch, revocation, retention, cache eviction, backup exclusion, and secure deletion behavior.
10. Test offline cold start, mid-request loss, process death, reboot, duplicate and reordered responses, expired credentials, quota exhaustion, conflicting devices, deleted accounts, clock skew, corrupt local state, and server rollback.
11. Record synchronization invariants, ownership, telemetry, support actions, repair tooling, and the exit path from the selected storage or sync provider.

## Required Output

- journey-by-journey offline capability and freshness policy
- local and remote data-flow model with the authoritative owner of each invariant
- operation journal, idempotency, retry, ordering, and background-execution design
- conflict matrix with deterministic automatic and user-mediated outcomes
- local storage, migration, backup, logout, revocation, and deletion controls
- failure and multi-device test matrix with observed evidence
- reconciliation, repair, observability, support, and provider-exit plan

## Completion Gate

Do not call the design ready until representative devices have passed process-death, connectivity-loss, duplicate, reordering, conflict, migration, and full-resync tests without silent data loss or invariant violation. Platform background scheduling alone is not completion evidence.

## Conditional Reference

Read [Mobile Offline Sync Evidence](references/mobile-offline-sync-evidence.md) before selecting a synchronization or background-work pattern. Use [Transaction and Concurrency Design](../transaction-concurrency-design/SKILL.md) when writes protect cross-record or financial invariants.
