---
status: draft
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R3
tags: [playbook, backend, database, neon, postgres, security]
sources:
  - https://neon.com/docs/introduction
  - https://neon.com/docs/connect/connection-pooling
  - https://neon.com/docs/manage/endpoints/
  - https://neon.com/docs/postgres/backup-restore/backups
  - https://neon.com/docs/security/security-overview
  - https://neon.com/pricing
---

# Neon Postgres Integration

## Scope and Fit

This playbook covers Neon's managed Postgres/Lakebase Postgres capability behind trusted application code. Neon's current platform also advertises Auth, Object Storage, Functions, Realtime, AI Gateway, and search features; each is a separate selection and integration decision and is not approved by this playbook.

Use Neon when standard Postgres, database branches, autoscaling/scale-to-zero, and serverless-friendly connections fit an application that already has a trusted backend. Do not connect an untrusted browser or mobile client with a Postgres role. Do not assume a database service supplies end-user identity, object authorization, abuse protection, or an API.

Verify the current [platform scope](https://neon.com/docs/introduction), [pooling behavior](https://neon.com/docs/connect/connection-pooling), [backup options](https://neon.com/docs/postgres/backup-restore/backups), [security features](https://neon.com/docs/security/security-overview), and [pricing](https://neon.com/pricing) for the selected plan, cloud, and region.

## Trust Boundary

```text
untrusted client -> application authentication + authorization -> server data-access module
server -> least-privilege Postgres runtime role -> Neon
migration/backup operator -> separate direct connection and elevated role -> Neon
```

The backend derives user and tenant context from verified identity. The database connection string never enters client code. A database branch copied from production remains production-sensitive even if used for development.

## Prerequisites and Approval Boundaries

- Apply the [Managed Database Security Baseline](Managed%20Database%20Security%20Baseline.md).
- Accept an ADR covering region/cloud, Postgres version, compute range, scale-to-zero, branching, restore history, networking, cost, and exit.
- Security-review the exact driver/ORM, migration tool, Neon CLI/API client, integrations, and IaC module before use.
- Project creation, paid activation, credentials, IP allow/private network changes, production branching, remote migrations, restore/reset, and deletion are R3.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `DATABASE_URL_RUNTIME` | Server secret | Pooled endpoint for ordinary application queries |
| `DATABASE_URL_MIGRATION` | CI/operator secret | Direct endpoint and migration owner for DDL, `pg_dump`, and `pg_restore` |
| `NEON_API_KEY` | Automation secret only if approved | Control-plane automation; never needed by normal application requests |

Require TLS with certificate and hostname verification supported by the selected driver. Use separate projects or branches and separate roles per environment; never reuse production credentials in previews.

## Connection and Branch Rules

- Use the pooled endpoint for serverless functions, web applications, and high connection churn. Neon's pooler uses transaction mode.
- Use a direct connection for schema migrations, `pg_dump`/`pg_restore`, logical replication, long admin sessions, and features that depend on a persistent session.
- Pooled transaction mode does not support session-level `SET`/`RESET`, `LISTEN`/`NOTIFY`, session advisory locks, and several other session-dependent features. Qualify the selected driver and ORM against the current list.
- Configure application reconnect and bounded retry for compute restarts and wake events. Retry only safe/idempotent work or retry the whole database transaction.
- Measure scale-to-zero wake latency against the product SLO. Disable it only with a documented cost tradeoff.
- Protect production branches where the plan supports it. Do not create data-bearing branches for previews unless privacy, retention, deletion, credential rotation, and cleanup are approved.

## Reference Schema and Least-Privilege Role

Run reviewed DDL as the migration owner over a direct connection. Keep passwords and provider-created login roles out of migration files.

```sql
revoke all on schema public from public;

create schema if not exists app;
revoke all on schema app from public;

create role app_runtime
  nologin
  nosuperuser
  nocreatedb
  nocreaterole
  noreplication
  nobypassrls;

create table app.projects (
  id uuid not null default gen_random_uuid(),
  tenant_id uuid not null,
  owner_id text not null,
  name text not null check (char_length(name) between 1 and 120),
  created_at timestamptz not null default now(),
  primary key (tenant_id, id)
);

create index projects_tenant_owner_idx
  on app.projects (tenant_id, owner_id);

grant usage on schema app to app_runtime;
grant select, insert, update, delete on app.projects to app_runtime;

alter default privileges in schema app revoke all on tables from public;
alter default privileges in schema app revoke all on sequences from public;
```

Create or rotate the environment-specific login identity through an approved provider/secret workflow, then grant it membership in `app_runtime`. Do not grant object ownership. Add read-only, job, or admin group roles only when their operations differ.

This example relies on the trusted backend to scope every query. If database RLS is required as defense in depth, design a trustworthy per-request identity propagation mechanism and prove it under transaction pooling; do not rely on a session variable that can leak or disappear between pooled transactions.

## Reference Server Data Access

After the exact `pg` version is reviewed, keep a bounded shared pool and include tenant scope in the SQL itself:

```ts
import { Pool } from "pg";

const pool = new Pool({
  connectionString: process.env.DATABASE_URL_RUNTIME,
  max: 10,
  connectionTimeoutMillis: 5_000,
  idleTimeoutMillis: 30_000,
});

export async function getProject(tenantId: string, projectId: string) {
  if (!tenantId || !projectId) throw new Error("Missing scoped identifier");
  const result = await pool.query(
    `select id, tenant_id, owner_id, name, created_at
       from app.projects
      where tenant_id = $1 and id = $2`,
    [tenantId, projectId],
  );
  return result.rows[0] ?? null;
}
```

`tenantId` must come from a completed authorization decision, not directly from the request. Use explicit columns and fields. Apply statement, request, and transaction timeouts appropriate to the project.

## Verification

- Runtime role can perform only the named DML and cannot create/alter/drop schema, roles, databases, or policies.
- Every repository operation requires verified tenant context; wrong-tenant IDs return no data and cannot mutate.
- Parameters prevent injection; dynamic sort/identifier choices use a fixed allow-list.
- Clean migration, upgrade, rollback/roll-forward, and seed work on isolated branches with synthetic data.
- Pooled and direct modes are used correctly; connection leaks, saturation, queue timeout, compute restart, autoscale, and wake behavior are measured.
- Critical constraints survive concurrent writes and transaction retries.
- Instant restore/history and an independent `pg_dump`/`pg_restore` path are evaluated against RPO/RTO. Restore into an isolated destination and verify roles, permissions, data, and journeys.

## Operations, Cost, and Exit

Monitor compute activity, scale-to-zero, connection and pool waits, query latency/errors, storage/history growth, branch count and age, backup/export health, transfer, quotas, and spend. Alert before the maximum compute range or cost ceiling.

For exit, use a direct connection and native Postgres schema/data export. Inventory extensions, logical replication, branching automation, provider API use, networking, Auth/storage/functions if separately adopted, and features unavailable on the target. Revoke roles/API keys only after the target and rollback copy are verified.

## Re-Review Triggers

- plan, pricing, Postgres major version, cloud/region, pooling, scale-to-zero, history/restore, branching, private networking, or platform ownership changes
- new extension, database branch with sensitive data, replica, control-plane automation, or optional Neon backend product
- wake-latency SLO miss, connection exhaustion, role escalation, cross-tenant result, restore failure, or cost anomaly

