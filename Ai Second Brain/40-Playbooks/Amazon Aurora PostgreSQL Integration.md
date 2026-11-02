---
status: draft
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R3
tags: [playbook, backend, database, aws, aurora, postgres, security]
sources:
  - https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.html
  - https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.Security.html
  - https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/UsingWithRDS.IAMDBAuth.html
  - https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Managing.Backups.html
  - https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/rds-proxy.html
  - https://aws.amazon.com/rds/aurora/pricing/
---

# Amazon Aurora PostgreSQL Integration

## Scope and Fit

This playbook covers Amazon Aurora PostgreSQL-Compatible Edition using provisioned instances or Aurora Serverless v2. It does not cover Aurora MySQL, Aurora DSQL, ordinary RDS PostgreSQL, Babelfish, zero-ETL integrations, or Global Database except when a project separately selects them.

Use Aurora PostgreSQL when PostgreSQL compatibility, AWS VPC/IAM integration, configurable high availability, replicas, backup controls, and mature operations justify the additional infrastructure and cost. Avoid it for a small application that cannot operate AWS networking, identity, monitoring, failover, and recovery safely.

Recheck [Serverless behavior and limitations](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless-v2.html), [security](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.Security.html), [IAM database authentication](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/UsingWithRDS.IAMDBAuth.html), [backups](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Managing.Backups.html), [RDS Proxy](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/rds-proxy.html), engine/region support, and [pricing](https://aws.amazon.com/rds/aurora/pricing/) before selection.

## Trust Boundary

```text
untrusted client -> application authentication + authorization -> workload in private network
workload -> security group + TLS + least-privilege database role (optionally RDS Proxy) -> Aurora
operator/CI -> separate IAM and migration role -> schema/control plane
```

IAM control-plane permission, database login, and end-user authorization are three different layers. A workload that can connect still needs a narrow database role; an authenticated app user still needs resource/tenant authorization.

## Prerequisites and Approval Boundaries

- Apply the [Managed Database Security Baseline](Managed%20Database%20Security%20Baseline.md).
- Accept ADRs for engine major/minor policy, region/AZs, instance or Serverless v2 capacity, replicas, VPC/subnets, public accessibility, security groups, encryption/KMS, authentication, proxy, backup/RPO/RTO, monitoring, cost, and exit.
- Security-review exact database drivers, migration tools, AWS SDK/CLI, IaC modules/providers, container images, and observability agents before use.
- AWS account/resource creation, IAM/KMS/security-group changes, credentials/tokens, cluster/proxy creation, billing, production migration, failover, restore, snapshot copy, scaling, and deletion are R3.

## Network and Identity Baseline

- Place the cluster in the intended VPC and private subnets by default. Set public accessibility off unless a reviewed requirement and compensating controls justify it.
- Allow the database port only from named workload security groups or approved private paths. Avoid broad CIDRs.
- Require TLS and validate the current AWS RDS CA and hostname through the driver.
- Use separate IAM roles for infrastructure administration, deployment, migration, backup/recovery, monitoring, and application runtime.
- Inside PostgreSQL, separate schema owner/migration, runtime, read-only, job, and emergency roles. The master/admin identity is not an application credential.
- Prefer Secrets Manager rotation or IAM database authentication where its constraints fit. IAM database auth tokens last 15 minutes, require TLS, consume database resources, and are not a substitute for database grants.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `DATABASE_URL_RUNTIME` | Server secret or dynamically constructed server config | Runtime role through cluster/proxy endpoint |
| `DATABASE_URL_MIGRATION` | CI/operator secret | Direct migration-owner endpoint |
| `AWS_REGION` | Server configuration | Selects the authorized region for IAM/Secrets operations |
| Secret ARN/name | Server configuration, not secret value | Locates the approved runtime credential in Secrets Manager |
| RDS CA bundle path | Server artifact/configuration | Certificate chain for verified TLS |

Prefer workload IAM credentials over long-lived AWS access keys. Never place database passwords, generated IAM auth tokens, KMS material, or connection strings in source, build arguments, Terraform state outputs, or logs.

## Reference PostgreSQL Roles and Schema

Run as a reviewed migration identity. Create environment-specific login credentials outside the migration and grant them the no-login runtime group role.

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

If RLS is required, design the trusted identity propagation, table ownership, `FORCE ROW LEVEL SECURITY`, pool/proxy behavior, and bypass roles explicitly. Test views, functions, jobs, and backup/restore roles; RLS is not automatically applied to owners or `BYPASSRLS` roles.

## Reference Server Query

After reviewing the exact driver, use one bounded pool per process and tenant-scoped parameterized SQL:

```ts
import { Pool } from "pg";

const pool = new Pool({
  connectionString: process.env.DATABASE_URL_RUNTIME,
  max: 10,
  connectionTimeoutMillis: 5_000,
  idleTimeoutMillis: 30_000,
  ssl: { rejectUnauthorized: true },
});

export async function listProjects(tenantId: string, pageSize = 50) {
  if (!tenantId) throw new Error("Missing authorized tenant");
  const boundedSize = Math.min(Math.max(pageSize, 1), 100);
  const result = await pool.query(
    `select id, tenant_id, owner_id, name, created_at
       from app.projects
      where tenant_id = $1
      order by created_at desc, id desc
      limit $2`,
    [tenantId, boundedSize],
  );
  return result.rows;
}
```

The production TLS configuration must trust the current AWS RDS CA rather than rely only on this abbreviated example. Derive `tenantId` from verified authorization, not a request field.

## Capacity, Connections, and Failure

- For Serverless v2, set minimum and maximum Aurora Capacity Units from measured workload and cost limits. Test scaling and, if enabled and supported, pause/scale-to-zero wake behavior.
- Bound application pools across the full fleet. Use RDS Proxy when connection churn, Lambda/serverless fan-out, or faster failover handling justifies its cost and limitations.
- Configure statement, lock, idle-transaction, request, and job timeouts appropriate to the workload.
- Retry transient connection/failover or serialization errors with jitter and a strict attempt/deadline bound. Retry whole transactions, not partial external effects.
- Keep network calls outside database transactions. Use an outbox/reconciliation design where committed data must drive an external effect.

## Verification

- Network path works only from approved workload/admin sources; public and plaintext/unverified paths fail.
- IAM roles cannot exceed intended control-plane actions; runtime database role cannot migrate, administer, bypass policy, or read other schemas.
- Wrong-user/tenant direct IDs, lists, bulk work, exports, jobs, replicas, and admin paths are denied.
- Parameter binding, input bounds, constraints, isolation, deadlock/serialization retry, and idempotency preserve invariants under concurrency.
- Fleet connection count, proxy behavior, failover, DNS/connection recovery, Serverless scaling, max-capacity overload, and maintenance are tested.
- Logs, Performance Insights/Database Insights as selected, Enhanced Monitoring, CloudWatch alarms, audit needs, and redaction are verified without recording secrets or sensitive query values.
- Automated backup retention and snapshot policy meet requirements. Aurora continuous backups currently support point-in-time restore within a configured 1–35 day retention period; restore to a new isolated cluster and verify roles, parameters, extensions, data, permissions, and journeys.

## Cost and Exit

Model instance or ACU capacity, I/O mode/requests, storage, backup and retained snapshots, replicas, Global Database if any, RDS Proxy, data transfer, KMS, Secrets Manager, logs/metrics, support, and idle non-production resources. Set budgets and alarms before provisioning.

For exit, use native PostgreSQL logical export/replication as qualified for the data size and downtime window. Inventory Aurora extensions/features, parameter groups, IAM auth, Secrets Manager, RDS Proxy, VPC/private DNS, replicas, snapshots, KMS, monitoring, IaC state, and AWS event integrations. Revoke and delete only after the target, rollback retention, and required exports are verified.

## Re-Review Triggers

- engine version/support, region, instance/ACU range, Serverless behavior, pricing/I/O mode, IAM auth, RDS Proxy, backup, CA, KMS, or AWS policy changes
- new replica/global topology, extension, integration, public path, privileged role, cross-account access, or regulated data class
- failover or restore miss, connection storm, capacity ceiling, cross-tenant finding, secret exposure, unexpected spend, or migration/export gap

