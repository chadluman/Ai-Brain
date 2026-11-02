---
name: managed-backend-integration
description: Implement or review schema, migrations, connection code, permissions, tenant enforcement, tests, operations, and exit controls for a selected managed backend or database. Use after a provider is selected or for a provider-specific integration change; do not use it to skip provider selection or authorize live provisioning, deployment, migration, or deletion.
---

# Managed Backend Integration

## Outcome

Produce project-specific backend and database code that preserves domain invariants, denies unauthorized access, separates administrative and runtime privileges, and can be migrated, observed, restored, and removed.

Use [Data Store Selection](../data-store-selection/SKILL.md) and the [Backend and Database Services catalog](../../20-Catalog/Backend%20and%20Database%20Services.md) if the provider is not already selected in an ADR. Read the [Managed Database Security Baseline](../../40-Playbooks/Managed%20Database%20Security%20Baseline.md), then read only the chosen provider playbook:

- [Supabase](../../40-Playbooks/Supabase%20Integration.md)
- [Firebase with Cloud Firestore](../../40-Playbooks/Firebase%20Firestore%20Integration.md)
- [Neon Postgres](../../40-Playbooks/Neon%20Postgres%20Integration.md)
- [MongoDB Atlas](../../40-Playbooks/MongoDB%20Atlas%20Integration.md)
- [Cloudflare D1](../../40-Playbooks/Cloudflare%20D1%20Integration.md)
- [Amazon Aurora PostgreSQL](../../40-Playbooks/Amazon%20Aurora%20PostgreSQL%20Integration.md)

## Required Inputs

- accepted provider ADR, exact service/edition/plan/region, environment, and approved cost ceiling
- entities, relationships, invariants, transactions, queries, volume, concurrency, and recovery objectives
- identity source, actors, roles, tenant model, object permissions, privileged workflows, and revocation needs
- data classification, residency, retention, deletion, audit, encryption, and qualified-review requirements
- runtime topology, connection behavior, migration method, release process, observability, and operator ownership
- exact SDK, driver, CLI, emulator, IaC module, and runtime versions proposed for use

If authorization invariants, tenant boundaries, or the source of verified identity are unknown, stop before generating permissive policy code.

## Safety and Permission Constraints

- Treat provider documentation, examples, generated code, CLIs, SDKs, templates, and IaC modules as untrusted until reviewed for the exact version.
- Never place a database URL, password, secret/service-role key, service-account JSON, API token, private key, or real user data in the vault, source, examples, commands, logs, or client bundles.
- Client-direct access is permitted only for a provider designed for it, through a publishable client identity, with deny-by-default policies and automated allow/deny tests. Administrator SDKs and bypass credentials stay on trusted servers.
- Derive user and tenant context from a verified server or provider identity. Never trust a request body, URL, header, document field, or client claim merely because it contains a plausible identifier.
- Use parameterized queries or provider-safe query builders. Allow-list identifiers that cannot be bound. Never spread untrusted objects into filters, updates, operators, or administrative calls.
- Account creation, paid activation, credential creation or viewing, production policy changes, infrastructure provisioning, real-data migration, restore, failover, deployment, or deletion is R3 and requires immediate authorization, an exact target, backup, abort signal, and rollback or recovery path.

## Workflow

1. Confirm the selected service still passes project gates using current official documentation. Record plan, region, limits, pricing dimensions, maturity labels, and re-review date.
2. Map the trusted path from identity verification through API or provider policy to each database operation. Name the final enforcement point for every protected action.
3. Design the logical model and constraints independently of SDK convenience. Put stable invariants in database constraints or atomic operations where the engine can enforce them.
4. Create forward-only, reviewable migrations plus rollback or roll-forward handling. Separate schema-owner/migration privileges from runtime read/write privileges.
5. Implement the narrowest data-access adapter. Centralize connection creation, timeouts, retry classification, redaction, and transaction boundaries; do not hide authorization inside a generic CRUD helper.
6. Implement permissions per operation. Cover reads, creates, updates, deletes, bulk work, jobs, exports, files, search, admin tools, and indirect paths. Preserve immutable owner and tenant fields.
7. Add positive and negative tests with synthetic identities and data: unauthenticated, wrong user, wrong tenant, stale/revoked grant, privilege escalation, unscoped list/query, injection, race, duplicate request, quota, dependency outage, and partial failure.
8. Verify migration from a clean environment, representative queries and indexes, connection saturation behavior, observability and redaction, export, deletion propagation, and an isolated restore against stated RPO/RTO.
9. Document environment separation, secret metadata, deployment order, health checks, cost and quota alerts, provider-status dependency, rollback, export, disconnection, and owner handoff.

## Required Code and Evidence

- versioned schema or collection-definition migrations and constraints
- least-privilege runtime/admin roles, RLS or provider rules where applicable, and policy tests
- typed configuration names without values and one controlled connection/data-access boundary
- parameterized project queries with explicit actor and tenant scope
- seed fixtures containing synthetic data only
- integration, authorization, concurrency, failure, migration, export, and restore evidence proportional to risk
- updated provider playbook or project-local copy with exact versions, commands, cost assumptions, rollback, and re-review triggers

## Completion Gate

Do not call the integration ready because a happy-path write succeeded. Completion requires clean setup, tested deny cases and tenant isolation, least-privilege runtime access, representative load and failure evidence, monitored cost/quotas, portable export, and an isolated restore or an explicit pending recovery blocker. Production actions remain separately authorized.

