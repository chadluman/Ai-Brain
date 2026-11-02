# Multi-Region Resilience Evidence

Verified: 2026-10-22

## Current Sources

- [NIST SP 800-34 Rev. 1 Update 1](https://csrc.nist.gov/pubs/sp/800/34/r1/upd1/final) is an older but still final federal contingency-planning guide. Its business-impact, recovery-objective, testing, maintenance, and plan-coordination concepts are durable; provider products and current cloud topology require newer evidence.
- [AWS Well-Architected disaster recovery](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/plan-for-disaster-recovery-dr.html) distinguishes availability from disaster recovery and requires business-defined RTO and RPO, tested strategies, configuration-drift control, and automation. AWS cautions that multi-region complexity is usually unnecessary unless requirements justify it.
- [Google Cloud multi-regional deployment archetype](https://docs.cloud.google.com/architecture/deployment-archetypes/multiregional) was last reviewed 2026-09-09 and compares synchronous and asynchronous replication, routing, availability, latency, cost, and complexity. It is Google-specific, not a portability guarantee.
- [Azure regions and availability zones guidance](https://learn.microsoft.com/en-us/azure/well-architected/design-guides/regions-availability-zones) compares single-zone, multi-zone, active-passive, and active-active choices and emphasizes residency, cost, and complexity. Its mission-critical recommendations assume the corresponding Azure operating model.
- [PostgreSQL high availability and load balancing](https://www.postgresql.org/docs/current/high-availability.html) documents current database replication and standby concepts. Managed services can differ in failover, lag, fencing, backup, version, and operator controls.

## Decision Implications

- Provider guidance reflects different service models and risk assumptions. Derive topology from project objectives and test evidence rather than copying a “mission critical” diagram.
- Zone resilience, regional high availability, and disaster recovery protect against different failures. A second live region does not replace point-in-time recovery from corruption or deletion.
- Active-active stateless compute is easier than multi-writer authoritative data. Classify each subsystem instead of labeling the whole application active-active.
- Failover includes capacity, routing, identity, keys, configuration, observability, queues, caches, and dependencies, not only database replication.
- A failover test that never processes real workflow equivalents, creates writes, drains work, reconciles, and fails back does not prove the stated recovery objective.
