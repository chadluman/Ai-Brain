# Mobile Offline Sync Evidence

Verified: 2026-10-21

## Platform Evidence

- [Android offline-first data layer](https://developer.android.com/topic/architecture/data-layer/offline-first) describes a local and network data source, local-first reads, queued writes, synchronization choices, and conflict considerations. It treats a local data source as canonical for application reads, not automatically authoritative for server invariants.
- [Android persistent task scheduling](https://developer.android.com/develop/background-work/background-tasks/persistent) recommends WorkManager for work that must persist after the app leaves the visible state, and documents constraints, retry policies, and persistence across restarts and reboots. It is not a general guarantee of immediate execution.
- [Apple Background Tasks](https://developer.apple.com/documentation/BackgroundTasks) documents system-scheduled background refresh and processing. The system controls launch timing and resource availability, so foreground recovery paths remain necessary.
- [Apple CloudKit](https://developer.apple.com/documentation/cloudkit) states that the base CloudKit framework provides only minimal offline caching and complements rather than replaces an app's local data objects.
- [Apple: Deciding whether CloudKit is right for your app](https://developer.apple.com/documentation/cloudkit/deciding-whether-cloudkit-is-right-for-your-app) distinguishes managed local-replica synchronization, `CKSyncEngine`, and lower-level CloudKit control. The choice depends on the required control, schema, account, and ecosystem boundary.
- [Apple: Syncing a Core Data store with CloudKit](https://developer.apple.com/documentation/coredata/syncing-a-core-data-store-with-cloudkit) documents asynchronous local-replica synchronization and propagation behavior for that specific Apple stack.

## Design Interpretation

- "Offline-first" is a product contract, not a library choice. Define which actions work offline, which merely read cached data, and which must wait for authoritative validation.
- A local source of truth can make UI behavior consistent while the server remains authoritative for security, permissions, uniqueness, balances, inventory, or shared business invariants.
- Background schedulers are delivery opportunities. Jobs need durable checkpoints, idempotency, bounded retries, cancellation handling, and a foreground recovery path.
- Synchronization needs explicit conflict semantics. Timestamp-only last-write-wins is vulnerable to clock skew and can silently erase intent.
- Managed synchronization can reduce code but can also constrain identity, platforms, data model, diagnostics, migration, and provider exit. Record those boundaries in an ADR.

## Re-Review Triggers

- target OS, background policy, storage framework, sync SDK, or cloud-provider change
- new multi-device editing, collaboration, regulated data, or financial invariant
- evidence of lost, duplicated, reordered, stuck, or irreconcilable operations
- schema or identity migration, provider exit, or major account-lifecycle change
