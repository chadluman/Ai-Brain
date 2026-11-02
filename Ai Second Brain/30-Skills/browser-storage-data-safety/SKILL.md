---
name: browser-storage-data-safety
description: Design or review cookies, Web Storage, IndexedDB, Cache Storage, origin-private files, and other browser persistence for web applications. Use when client data must survive navigation, reload, offline use, or multiple tabs; do not treat browser storage as authoritative, secret, durable, or unlimited.
---

# Browser Storage Data Safety

## Outcome

Create a minimal, versioned browser-storage design that preserves required user work while tolerating eviction, corruption, concurrency, account changes, application upgrades, privacy controls, and deletion.

Use [Frontend State Design](../frontend-state-design/SKILL.md) to choose state ownership, [PWA and Offline Design](../pwa-offline-design/SKILL.md) for offline workflows, and [Session and Cookie Security](../session-cookie-security/SKILL.md) for authenticated browser sessions. This skill owns persistent client data mechanics and lifecycle safety.

## Required Inputs

- data items, authoritative source, sensitivity, user and tenant binding, value of persistence, retention, deletion, export, and offline needs
- target browsers, webviews, private modes, multi-tab and device behavior, origin and subdomain design, embedded contexts, and storage partitioning assumptions
- expected size and growth, transaction and concurrency needs, schema evolution, sync, backup, corruption, quota, eviction, recovery, and observability requirements

## Safety and Permission Constraints

- Browser persistence is accessible to application code at its origin, can be exposed by script compromise, and can be cleared, denied, partitioned, evicted, corrupted, or unavailable. It is not a system of record or a secret vault.
- Do not persist passwords, private keys, refresh or long-lived bearer tokens, authorization decisions, unrestricted personal data, or data whose deletion and account separation cannot be enforced.
- Client-side encryption does not solve key exposure when the same compromised origin can decrypt. Document the threat it addresses and keep server authorization authoritative.
- New local persistence and schema writes are R2. Migrating, deleting, exporting, or reconciling real user data, or changing production session behavior, is R3 and requires immediate authorization, backups or compensating recovery, bounded rollout, and observable results.

## Workflow

1. Inventory every cookie and storage location, key namespace, schema, producer, reader, owner, origin, user or tenant binding, data class, retention rule, and authoritative recovery source.
2. Eliminate persistence without clear user value. Select cookies for intentional server exchange, Web Storage only for small simple state without locking needs, IndexedDB for transactional structured data, Cache Storage for request-response resources, and other APIs only after support and lifecycle evidence.
3. Define origin, site, partition, frame, profile, private-mode, shared-device, tab, worker, and account boundaries. Never infer tenant or authorization from a client key.
4. Define quota assumptions, growth limits, compaction, persistence requests, storage-pressure behavior, eviction detection, corruption handling, and a usable degraded state. Preserve unsynced user work explicitly or disclose when it can be lost.
5. Design versioned schemas and monotonic, restartable migrations. Keep compatibility with the rollback horizon, quarantine malformed records, make partial upgrade recoverable, and never silently discard user-authored data.
6. Define transaction scope, multi-tab coordination, stale writers, conflicts, locks or leases where supported, crash points, and atomicity. Do not assume Web Storage has cross-context locking.
7. Bind data to the correct signed-in account and tenant. On logout, account switch, revocation, deletion, or shared-device handoff, clear or isolate state and invalidate sensitive cached responses and active workers as required.
8. Minimize telemetry about stored content. Measure only schema version, capacity class, failures, migration outcome, and recovery signals needed for operation, without recording payloads or stable tracking identifiers.
9. Test denied and unavailable storage, quota exhaustion, eviction, corruption, partial migration, downgrade, reload, crash, concurrent tabs, private mode, embedded contexts, logout, account switch, deletion, restore, offline edits, and reconnect reconciliation.

## Required Output

- storage inventory and data classification with authority, owner, origin, account or tenant, lifetime, size, and deletion rule
- API selection and schema, transaction, concurrency, quota, eviction, migration, rollback, and recovery design
- session, privacy, account-change, logout, deletion, offline, synchronization, observability, and test evidence
- unsupported environments, residual data-loss risks, owners, and re-review triggers

## Completion Gate

Do not call storage ready until the application remains correct when storage is missing, full, stale, corrupt, concurrently modified, cleared, or rolled back; sensitive state cannot cross accounts or tenants; migrations preserve recoverable user work; deletion covers every applicable store; and the server still enforces authority.

## Conditional Reference

Read [Browser Storage Evidence](references/browser-storage-evidence.md) before choosing a storage API, persistence assumption, migration mechanism, or site-data clearing behavior.
