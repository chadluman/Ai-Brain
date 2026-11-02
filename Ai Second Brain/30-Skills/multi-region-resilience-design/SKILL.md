---
name: multi-region-resilience-design
description: Design or review single-region, multi-zone, active-passive, and active-active multi-region systems for availability, disaster recovery, latency, capacity, residency, and sovereignty. Use only when region-level requirements are explicit; prefer simpler topology when it meets the objectives.
---

# Multi-Region Resilience Design

## Outcome

Produce the smallest regional topology that meets journey-specific availability, RTO, RPO, latency, capacity, residency, and recovery goals while making consistency, failover authority, split-brain, cost, and operating complexity explicit.

Use [Hosting and Runtime Selection](../hosting-runtime-selection/SKILL.md) for execution platforms, [Service Resilience Design](../service-resilience-design/SKILL.md) for dependency failure, [Backup and Disaster Recovery](../backup-disaster-recovery/SKILL.md) for restoration, and [Data Migration Design](../data-migration-design/SKILL.md) for movement and cutover. This skill owns regional topology and failover.

## Required Inputs

- critical user journeys, regions and geographies, traffic origins, latency targets, SLOs, maximum outage, RTO, RPO, degradation, and manual recovery tolerance
- data ownership, consistency and concurrency invariants, residency, sovereignty, transfer, encryption, retention, deletion, and legal or contractual constraints
- provider regions and zones, service availability, quotas, capacity reservations, control planes, routing, DNS, certificates, identity, secrets, observability, and support
- stateful stores, replication, caches, queues, object storage, search, scheduled work, external effects, third-party endpoints, and global identifiers
- deployment, schema migration, configuration, incident command, cost, staffing, testing, rollback, and provider-exit capacity

## Safety and Permission Constraints

- Do not equate multi-region with high availability. Shared control planes, identity, DNS, dependencies, bad deploys, corrupt data, operator error, and global configuration can fail every region.
- Strong cross-region consistency has latency and availability costs; asynchronous replication has data-loss and conflict costs. State the tradeoff per invariant rather than using one global label.
- Never route or replicate data outside approved regions. Map logs, telemetry, backups, support access, keys, queues, CDN caches, and failover copies, not only the primary database.
- Automatic failover is a write-authority change. Define fencing, quorum, stale-region isolation, reconciliation, and failback before enabling it.
- Provisioning paid regional resources, changing production routing or replication, failing over, restoring real data, moving data across borders, or destroying a region is R3 and requires immediate authorization and a tested recovery plan.

## Workflow

1. Define regional failure scenarios and journey-specific objectives. Distinguish zone loss, region loss, provider control-plane failure, network partition, capacity shortage, dependency outage, data corruption, bad release, and identity or DNS failure.
2. Test whether one region with multiple zones plus backup and restore meets the objectives. Add regions only for demonstrated region-outage, latency, capacity, residency, isolation, or business-continuity needs.
3. Compare backup-and-restore, pilot light, warm standby, active-passive, partitioned or home-region, and active-active patterns on RTO, RPO, correctness, capacity, routing, cost, complexity, and operator burden.
4. Assign each datum and invariant a home, replication direction, consistency model, conflict rule, identity namespace, and write authority. Keep globally unique IDs and prevent concurrent split-brain writes where reconciliation cannot preserve correctness.
5. Make each regional stack independently operable where the objective requires it: compute, data, queues, caches, secrets, keys, certificates, configuration, observability, and runbooks. Identify global dependencies and design their degraded behavior.
6. Define traffic steering and health from end-to-end user journeys rather than process liveness. Account for DNS and client caching, connection draining, sessions, uploads, in-flight work, sticky routing, and rollback.
7. Coordinate application, schema, event, and configuration versions across regions. Use backward-compatible changes and prove mixed-version operation, replication lag, failover during deployment, and rollback.
8. Plan capacity for failover load, regional quotas, cold caches, reconnect storms, queue backlog, recovery jobs, data transfer, and provider capacity pressure. Allocate cost and set spend alarms before an incident.
9. Define failover authority, evidence, communications, fencing, recovery checkpoints, data-loss decision, user-facing degradation, reconciliation, failback, and after-action review. Automation must have bounded triggers and an operator stop path.
10. Exercise zone and region loss, partial network, stale replica, replication stop, corrupted data, dependency failure, bad deploy, capacity exhaustion, control-plane loss, failover, sustained operation, failback, and regional retirement using safe environments.

## Required Output

- failure model and journey-specific SLO, RTO, RPO, latency, capacity, residency, and degradation requirements
- topology comparison and ADR for single region, zones, passive, partitioned, or active-active regions
- data home, replication, consistency, conflict, write-authority, fencing, routing, global dependency, and mixed-version design
- failover and failback authority, runbook, observability, capacity, cost, communication, reconciliation, rollback, and exit plan
- isolated exercise evidence with measured recovery and known residual risks

## Completion Gate

Do not call the design resilient until the selected topology demonstrably beats the simpler alternative on required objectives, every stateful component has a consistency and recovery contract, approved residency holds during failover, surviving capacity is proven, stale regions are fenced, global dependencies are tested, operators can fail over and fail back within objectives, and reconciliation accounts for all accepted data loss or conflict.

## Conditional Reference

Read [Multi-Region Resilience Evidence](references/multi-region-resilience-evidence.md) when comparing regional patterns, translating provider guidance, or defining RTO, RPO, active-passive, active-active, and residency boundaries.
