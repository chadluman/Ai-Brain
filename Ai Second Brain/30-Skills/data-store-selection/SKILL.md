---
name: data-store-selection
description: Select primary and specialized data stores from workload, consistency, recovery, privacy, portability, and operating requirements. Use for a new data architecture or material storage change; do not add multiple databases before one store is proven insufficient.
---

# Data Store Selection

## Outcome

Choose the smallest durable data architecture that protects domain invariants, supports required access patterns, can be restored, and has a credible migration path.

Read [storage evidence](references/storage-evidence.md) before treating a database category or product as a default. When a managed backend or database is in scope, compare the current qualified shortlist in the [Backend and Database Services catalog](../../20-Catalog/Backend%20and%20Database%20Services.md); use [Managed Backend Integration](../managed-backend-integration/SKILL.md) only after selection.

## Inputs

Define entities and relationships, invariants, transaction boundaries, query and write patterns, concurrency, volume and growth, latency and throughput, availability, regions, offline or edge needs, search and analytics, files and media, data sensitivity, residency, retention and deletion, recovery point and time objectives, team skills, budget, and export requirements. Also distinguish a BaaS from a managed database: identify who supplies the API, end-user identity, authorization enforcement, background execution, and file storage.

## Workflow

1. Model the data and invariants independently of a vendor. Mark system-of-record data, derived views, caches, search indexes, analytics copies, files, and event history.
2. Select one primary store when possible. Add a specialized store only when a measured access, isolation, durability, or scale requirement cannot be met safely by the primary store.
3. Decide whether untrusted clients ever access a provider data API directly. Permit that only when the product is designed for it and deny-by-default rules or RLS can be tested; otherwise require a trusted backend boundary.
4. Compare credible candidates on transaction and consistency behavior, concurrency, query model, indexing, schema evolution, backup and point-in-time recovery, replication, failure modes, supported versions, security, observability, operating burden, cost, export, and license. Compare the exact plan, region, and maturity status rather than the product name alone.
5. Prove critical queries, writes, constraints, authorization boundaries, conflict handling, migrations, connection behavior, realistic data size, and cost drivers with a focused POC when claims remain uncertain.
6. Define ownership and synchronization for every derived store. Include lag, replay, rebuild, deletion propagation, and reconciliation.
7. Design forward and rollback migrations. Account for mixed application versions, long-running changes, locks, partial deployment, and data validation.
8. Define encrypted transport and storage as required, least privilege, secret rotation, tenant isolation, audit, retention, deletion, and safe lower-environment data.
9. Implement backup and restoration as a tested recovery process. A successful backup job without a verified restore is not recovery evidence.
10. Record the decision and exit path in an ADR with data-export format, downtime assumptions, provider-coupled features, and vendor-lock-in consequences.

## Current Default (2026)

Start from PostgreSQL as the default primary store when its model fits: use JSONB for flexible or semi-structured fields inside the relational model, and pgvector for modest vector workloads, before adding a second store. A dedicated vector store is justified by measured vector scale or retrieval requirements — the 2026 research cited 100M+ vectors as a rough threshold for that step. Treat that figure as a rule of thumb, not a measured boundary, and prove the decision with the project's own workload. See [Retrieval and Grounding Design](../retrieval-grounding-design/SKILL.md) for the retrieval side.

When a document store is a candidate, check its licence as part of step 4: MongoDB is distributed under the SSPL, which is not an OSI-approved open-source licence. Record the licence finding in the comparison and have it reviewed under [Open Source License Review](../open-source-license-review/SKILL.md) before relying on it.

## Guardrails

- A cache, search index, analytics warehouse, or event stream is not the source of truth unless its durability and correction model intentionally support that role.
- Financial balances, credits, inventory commitments, and similar conserved values require auditable ledger or transaction principles and reconciliation.
- Managed service claims do not remove responsibility for configuration, access, retention, backup scope, restore tests, regional failure, quotas, and cost.
- Do not copy production personal or secret data into development, tests, examples, logs, or the vault.
- Provisioning, migrating real data, destructive schema changes, deletion, and restore over existing data are R3 actions.

## Completion

Deliver the logical model and invariants, workload evidence, selected primary and justified specialized stores, service-shape and trusted-access-path decision, consistency and transaction behavior, migration plan, backup and tested restore plan, privacy and retention controls, cost model, ADR, exit path, and re-evaluation triggers.
