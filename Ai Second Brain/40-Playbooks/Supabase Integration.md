---
status: draft
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R3
tags: [playbook, backend, database, supabase, postgres, security]
sources:
  - https://supabase.com/docs/guides/database/overview
  - https://supabase.com/docs/guides/database/secure-data
  - https://supabase.com/docs/guides/database/postgres/row-level-security
  - https://supabase.com/docs/guides/database/connecting-to-postgres
  - https://supabase.com/docs/guides/local-development
  - https://supabase.com/docs/guides/platform/backups
  - https://supabase.com/pricing
---

# Supabase Integration

## Scope and Fit

This playbook covers hosted Supabase Postgres, Data API, and Auth integration. Treat Storage, Realtime, Edge Functions, and third-party extensions as additional services with their own data, permission, backup, and cost review.

Use Supabase when relational data and transactions fit, integrated Auth/API reduce delivery work, and the team can design and test Postgres grants plus row-level security (RLS). Do not use client-direct access when the policy cannot be expressed and tested safely; place those operations behind trusted server code or select a different architecture.

Current product facts and volatile limits are in the [official database overview](https://supabase.com/docs/guides/database/overview), [connection guide](https://supabase.com/docs/guides/database/connecting-to-postgres), [backup guide](https://supabase.com/docs/guides/platform/backups), and [pricing](https://supabase.com/pricing). Recheck the selected plan and region before a decision.

## Trust Boundary

```text
browser/mobile -> publishable key + user token -> Supabase Data API -> grants + RLS -> Postgres
trusted server/admin job -> secret key or direct database role -> explicitly privileged operation
```

A publishable key identifies the project; it is not an authorization policy. Every table or view in an exposed schema requires deliberate grants and tested RLS. Secret and legacy service-role keys bypass RLS when used without a user token and must never enter untrusted clients.

## Prerequisites and Approval Boundaries

- Apply the [Managed Database Security Baseline](Managed%20Database%20Security%20Baseline.md).
- Accept an ADR covering plan, region, Postgres version, BaaS features, recovery, cost, and exit.
- Security-review exact Supabase CLI, client SDK, container runtime, migration tool, and other dependencies before installation.
- Creating a hosted project, enabling billing/add-ons, generating or viewing real credentials, linking a local CLI to a project, applying remote migrations, changing production RLS/grants, restoring, or deleting is R3.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `SUPABASE_URL` | Public only where the client architecture requires it | Project API URL |
| `SUPABASE_PUBLISHABLE_KEY` | Publishable; still restrict usage and monitor abuse | Client Data API identity; relies on grants and RLS |
| `SUPABASE_SECRET_KEY` | Server secret | Administrative access that can bypass RLS |
| `DATABASE_URL_RUNTIME` | Server secret | Runtime Postgres role through the selected direct or pooled endpoint |
| `DATABASE_URL_MIGRATION` | Operator/CI secret | Direct connection for migrations, dump, restore, and admin operations |

Projects may expose legacy `anon` and `service_role` keys. Preserve the same boundary: `anon` is publishable and policy-constrained; `service_role` is secret and bypass-capable. Keep each environment in a separate project and secret scope.

## Build Workflow

1. Model tables, constraints, transaction boundaries, access matrix, and whether each operation is client-direct or server-only.
2. Establish a reviewed local stack or isolated test project with synthetic data. The official local workflow currently requires the Supabase CLI and a Docker-compatible container runtime.
3. Put schema, functions, indexes, grants, RLS, and policy tests in migrations. Do not rely on dashboard-only edits.
4. Revoke broad client grants, grant only required operations, enable RLS on every exposed table, and add one policy per operation where that improves review clarity.
5. Use a publishable key plus the signed-in user's token for user-scoped access. Use a secret/service role only in narrow server-only admin modules with separate tests and logs.
6. Select the connection mode by runtime: Data API for clients, transaction pooler for high-churn serverless/edge connections, and direct connection for migrations, dumps, restores, or session-dependent work. Verify the current official connection matrix.
7. Test allowed and denied RLS paths locally and against an isolated hosted environment before any production policy change.
8. Configure and test database recovery. Supabase database backups contain database data, not the objects stored through the Storage API; protect and restore those objects separately.

## Reference Migration: Single-Owner Records

Adapt names and invariants to the project. This is intentionally owner-only; do not stretch it into team tenancy. Use [Authorization and Tenancy Design](../30-Skills/authorization-tenancy-design/Authorization%20and%20Tenancy%20Design.md) for membership and role rules.

```sql
create table public.projects (
  id uuid primary key default gen_random_uuid(),
  owner_id uuid not null references auth.users(id) on delete cascade,
  name text not null check (char_length(name) between 1 and 120),
  created_at timestamptz not null default now()
);

create index projects_owner_id_idx on public.projects (owner_id);

alter table public.projects enable row level security;
revoke all on table public.projects from anon, authenticated;
grant select, insert, update, delete on table public.projects to authenticated;

create policy projects_select_own
on public.projects for select to authenticated
using ((select auth.uid()) = owner_id);

create policy projects_insert_own
on public.projects for insert to authenticated
with check ((select auth.uid()) = owner_id);

create policy projects_update_own
on public.projects for update to authenticated
using ((select auth.uid()) = owner_id)
with check ((select auth.uid()) = owner_id);

create policy projects_delete_own
on public.projects for delete to authenticated
using ((select auth.uid()) = owner_id);
```

Review views, `security definer` functions, table owners, roles with `BYPASSRLS`, and default privileges separately; they can bypass or widen the table policy. Preserve ownership fields during updates and test every operation.

## Reference Client Boundary

After the exact SDK version is reviewed, keep initialization small and inject only publishable configuration into client code:

```ts
import { createClient } from "@supabase/supabase-js";

export function createPublicSupabaseClient(url: string, publishableKey: string) {
  if (!url || !publishableKey) throw new Error("Missing Supabase public configuration");
  return createClient(url, publishableKey);
}
```

Do not create a convenience function that can select a secret key based on caller input. Server administrative clients belong in a different module with no client import path.

## Verification

- Assert anonymous users receive no access unless a named public use case exists.
- Assert Alice can create/read/update/delete Alice's row and cannot set or change `owner_id` to another user.
- Assert Bob cannot list, read by guessed UUID, update, or delete Alice's row.
- Test every exposed table, view, RPC/function, Storage policy, Realtime subscription, and server-only bypass path.
- Test migrations from an empty database and from the prior production-equivalent schema.
- Exercise connection saturation, dropped connections, transaction retries, slow queries, plan quotas, and project pause/wake behavior where applicable.
- Restore a backup to an isolated destination, reapply any omitted credentials/configuration, and verify data, permissions, Auth linkage, Storage objects, and critical journeys.

## Operations, Cost, and Exit

Monitor denied requests, auth anomalies, database connections, pool waits, slow queries, storage, egress, backup/PITR state, logs, function usage, and plan spend. Set alerts before hard limits or an approved cost ceiling.

For exit, prove a schema and data export with native Postgres tools over a direct connection. Inventory non-Postgres coupling separately: Auth users and sessions, Storage objects and policies, Realtime behavior, functions, extensions, webhooks, and application assumptions. Revoke keys and database roles only after the replacement is verified and rollback retention is accepted.

## Re-Review Triggers

- plan, pricing, quotas, key model, region, Postgres major version, backup behavior, or connection architecture changes
- new exposed table/view/function, Auth provider, Storage bucket, Realtime channel, extension, replica, or server bypass path
- failed RLS test, cross-tenant incident, connection exhaustion, restore failure, or cost anomaly

