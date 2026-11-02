---
status: draft
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R3
tags: [playbook, backend, database, cloudflare, d1, sqlite, security]
sources:
  - https://developers.cloudflare.com/d1/
  - https://developers.cloudflare.com/d1/get-started/
  - https://developers.cloudflare.com/d1/worker-api/prepared-statements/
  - https://developers.cloudflare.com/d1/best-practices/read-replication/
  - https://developers.cloudflare.com/d1/platform/limits/
  - https://developers.cloudflare.com/d1/reference/time-travel/
  - https://developers.cloudflare.com/d1/best-practices/import-export-data/
---

# Cloudflare D1 Integration

## Scope and Fit

This playbook covers Cloudflare D1 accessed by a Cloudflare Worker through a D1 binding. D1 is a managed serverless SQL database with SQLite semantics; it is not a general Postgres/MySQL endpoint and it does not provide application-user authentication, row-level security, or database users for each customer.

Use D1 when the application already fits Workers, each database remains within current limits, SQLite-compatible SQL is sufficient, and the Worker can be the trusted authorization boundary. Avoid it when a single database will exceed the documented size/row/query limits, heavy write concurrency or relational features exceed D1 behavior, or the runtime must be portable without a Cloudflare adapter.

Current documented paid limits include 10 GB per database, 2 MB per row/string/BLOB, 100 bound parameters, and per-invocation query limits; free limits are lower. Recheck [limits](https://developers.cloudflare.com/d1/platform/limits/), [pricing](https://developers.cloudflare.com/d1/platform/pricing/), and maturity labels immediately before selection.

## Trust Boundary

```text
untrusted client -> Worker authentication -> application authorization -> tenant-scoped prepared statement -> D1 binding
operator/CI -> scoped Cloudflare API token -> migrations, export, or restore
```

Only the bound Worker reaches the normal data API. Every Worker route must authenticate the caller and enforce action/resource/tenant policy before querying. The D1 binding is not proof that the caller is authorized.

## Prerequisites and Approval Boundaries

- Apply the [Managed Database Security Baseline](Managed%20Database%20Security%20Baseline.md).
- Accept an ADR covering Worker placement, SQLite compatibility, database partitioning, limits, read consistency, recovery, cost, and exit.
- Security-review the exact Node runtime, Wrangler CLI, Worker framework, test emulator, generated types, and other packages before installation or execution.
- Account/database creation, API tokens, billing, remote migrations, production data import/export, read-replica changes, Time Travel restore, deployment, and deletion are R3.

## Configuration Inventory

| Item | Exposure | Purpose |
|---|---|---|
| `DB` binding | Worker-only binding | Application access to the selected D1 database |
| Database ID/name | Deployment configuration | Binds the correct database per environment |
| Cloudflare API token | CI/operator secret | Narrow control-plane permissions for approved deployment/migration operations |
| Authentication verifier configuration | Worker secret/configuration | Verifies issuer, audience, keys, and token/session policy before data access |

Use separate Worker environments and D1 databases for local/test, staging, and production. Bind by environment; never make runtime selection depend on untrusted request data.

## Schema and Migration Workflow

1. Model tables, constraints, indexes, write contention, query count, and expected database growth against the current D1 limits.
2. Keep numbered SQL migrations in source control. Apply locally first, then to an isolated remote test database.
3. Snapshot/export or record a Time Travel bookmark as appropriate before an authorized production migration. Define abort and recovery behavior.
4. Use prepared statements with bound parameters for application queries. Reserve `exec()` for reviewed one-shot maintenance/migrations without untrusted input.
5. Treat tenant scope as mandatory in keys, unique constraints, indexes, reads, updates, and deletes.
6. If global read replication is enabled, use the Sessions API and propagate its bookmark for sequential consistency. Without Sessions, replicas can lag; do not assume read-your-writes.

## Reference Migration

```sql
create table tenants (
  id text primary key,
  name text not null check (length(name) between 1 and 120)
);

create table projects (
  id text not null,
  tenant_id text not null,
  owner_id text not null,
  name text not null check (length(name) between 1 and 120),
  created_at text not null,
  primary key (tenant_id, id),
  foreign key (tenant_id) references tenants(id) on delete cascade
);

create index projects_tenant_owner_idx
  on projects (tenant_id, owner_id);
```

Use an unambiguous UTC timestamp representation and validate it in application code. Test foreign-key behavior and migration compatibility in D1 rather than assuming every SQLite feature or pragma is exposed identically.

## Reference Worker Repository

The authentication function is intentionally project-specific. It must verify the session/token and return server-trusted subject and tenant context before this repository runs.

```ts
type AuthContext = {
  subject: string;
  tenantId: string;
  permissions: ReadonlySet<string>;
};
type Env = { DB: D1Database };

export async function getProject(
  env: Env,
  auth: AuthContext,
  projectId: string,
) {
  if (
    !auth.subject ||
    !auth.tenantId ||
    !projectId ||
    !auth.permissions.has("project:read")
  ) {
    throw new Error("Missing authorized scope");
  }

  return env.DB
    .prepare(
      `select id, tenant_id, owner_id, name, created_at
         from projects
        where tenant_id = ?1 and id = ?2`,
    )
    .bind(auth.tenantId, projectId)
    .first();
}
```

Use explicit response fields and avoid returning D1 error details, SQL, bindings, or internal metadata to clients. Bound pagination and allow-list sort choices.

## Permissions and Platform Access

D1 does not replace application authorization with SQL grants or RLS. Enforce end-user policy in the Worker and test it as a security boundary. Separately restrict Cloudflare dashboard roles and API tokens to the exact account, database, Worker, and actions needed. Use different identities for routine deploy, schema migration, backup/export, and emergency restore where their privileges differ.

## Verification

- Unauthenticated, invalid, expired, revoked, wrong-audience, wrong-user, and wrong-tenant requests are denied before a D1 call.
- Every select/update/delete includes tenant scope; owner/role checks match the access matrix; immutable scope cannot change.
- Bound values prevent injection; dynamic identifiers and order expressions are fixed allow-lists.
- Migrations succeed on an empty and prior-version database; constraints and indexes are observable.
- Query counts, rows read/written, row size, bound parameters, Worker subrequests, database size, and concurrency remain below current limits under representative load.
- Timeouts, retries, duplicate requests, partial failure, and ambiguous responses preserve invariants.
- When using read replication, a bookmark carried through the logical user session proves required read consistency.
- Time Travel restore is rehearsed in an isolated database where supported, and a SQL export/import path is proven for longer retention and provider exit.

## Recovery, Cost, and Exit

D1 Time Travel is currently always on for production-storage databases and retains up to 30 days on Workers Paid or 7 days on Free. A restore cancels in-flight work and is R3. For longer retention or an independent failure domain, create an approved export process and test import; do not assume Time Travel alone meets the threat model.

Monitor Worker errors/latency, D1 query errors, rows read/written, database/storage size, slow or high-scan queries, replica serving region and primary/replica behavior, Time Travel readiness, API-token activity, quotas, and spend.

For exit, export schema and data to SQL, capture platform bindings and migration history, and test the target engine for SQLite/D1 differences. Inventory Worker runtime APIs, Sessions/bookmarks, Durable Objects/Queues/R2 dependencies, authentication middleware, and deployment configuration.

## Re-Review Triggers

- D1 limits, pricing, storage subsystem, SQL compatibility, migrations, Time Travel, read replication, Sessions API, Wrangler, or Workers runtime changes
- new database partitioning strategy, cross-database workflow, high-write path, remote API access, or privileged automation
- cross-tenant result, query-limit error, write contention, replica-consistency defect, restore failure, export gap, or cost anomaly

