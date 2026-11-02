---
name: backup-disaster-recovery
description: Design and verify backup, restoration, continuity, and disaster-recovery plans for application data and critical configuration. Use when defining RPO/RTO, reviewing managed backup claims, planning ransomware resilience, or testing recovery; never restore over real data without explicit authorization.
---

# Backup and Disaster Recovery

## Outcome

Create a prioritized, tested recovery capability that can restore required business service and trustworthy data after deletion, corruption, compromise, provider failure, or regional disaster.

Read [recovery evidence](references/recovery-evidence.md) before choosing backup or contingency controls.

## Inputs

Inventory critical journeys, systems of record, files and media, identity and secrets, infrastructure and application configuration, external services, data classifications, legal retention and deletion, business impact, dependencies, failure threats, available personnel, and budget.

## Workflow

1. Run a business-impact analysis. Set recovery point and recovery time objectives per capability, including maximum tolerable outage and acceptable data loss.
2. Map every required recovery asset and dependency: data, schemas, object versions, configuration, infrastructure definitions, encryption keys, identity, domains, certificates, build artifacts, runbooks, contacts, and provider access.
3. Define backup frequency, consistency, scope, encryption, integrity, retention, geographic and account separation, immutability or offline protection, monitoring, and deletion behavior from the threat model.
4. Ensure production compromise or operator error cannot silently alter every recovery copy. Protect backup administration and keys with separate least privilege and tested emergency access.
5. Define ordered restoration and validation. Include clean infrastructure, identity, data, dependent services, application versions, caches and indexes, traffic, reconciliation, and user communication.
6. Test restores into an isolated environment on a schedule. Measure achieved RPO and RTO, validate application-level invariants and representative journeys, then remove test data safely.
7. Exercise scenarios such as accidental deletion, bad migration, corruption, credential compromise, ransomware, provider or region loss, and unavailable personnel. Record gaps and owners.
8. Define failover, failback, conflict reconciliation, degraded operation, manual workarounds, and the authority to declare and end a disaster.
9. Re-test after material schema, provider, encryption, identity, topology, or retention changes.

## Safety and Permission Boundaries

- A configured or successful backup job is not evidence that the service can be restored within objectives.
- Replication and synchronization can copy corruption or deletion; they are not automatically independent backups.
- Never store backup credentials, encryption keys, recovery codes, or real data in the vault.
- Production restore, failover, failback, deletion, retention changes, or recovery-key use is R3 and requires explicit authorization immediately before action.
- Recovery testing must preserve privacy, tenant isolation, legal holds, and deletion obligations.

## Completion

Deliver the business-impact priorities, dependency and asset inventory, RPO/RTO, backup design, access and key controls, ordered runbook, isolated restore-test evidence with achieved timings, reconciliation and validation, failover and failback, communications, costs, gaps, owners, and next exercise date.
