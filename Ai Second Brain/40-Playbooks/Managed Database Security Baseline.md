---
status: reviewed
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R3
tags: [playbook, backend, database, security]
sources:
  - https://cheatsheetseries.owasp.org/cheatsheets/Database_Security_Cheat_Sheet.html
  - https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html
  - https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html
  - https://www.postgresql.org/docs/current/ddl-rowsecurity.html
---

# Managed Database Security Baseline

## Purpose

Apply this baseline to every managed backend or database before provider-specific setup. It is the shared source of truth for controls repeated across providers; provider playbooks add only product-specific decisions.

## 1. Define the Trusted Access Path

Choose one path per operation and document it:

```text
untrusted client -> authenticated API/backend -> authorized operation -> database
```

or, only for a client-capable BaaS:

```text
untrusted client -> provider identity token -> tested policy/RLS -> exposed data API
```

Administrator SDKs, database credentials, migration roles, secret/service-role keys, backup access, and control-plane tokens are never client credentials. A gateway check can reject early, but the operation that touches protected data still needs resource and tenant authorization.

## 2. Model Data and Permission Invariants

Before schema or rule code, record:

- actors, service identities, tenants, resources, actions, sensitive fields, and privileged exceptions;
- immutable ownership and tenant fields, lifecycle states, valid transitions, uniqueness, referential integrity, and conserved values;
- which invariants the database enforces and which the application enforces;
- authorization behavior for lists, direct-object reads, writes, bulk actions, exports, jobs, files, search, admin tools, and deleted or suspended actors.

Authentication proves an identity. It does not grant resource access. Use [Authorization and Tenancy Design](../30-Skills/authorization-tenancy-design/Authorization%20and%20Tenancy%20Design.md) for the access matrix and negative cases.

## 3. Separate Identities and Privileges

Use distinct identities for control-plane administration, migrations/schema ownership, runtime reads/writes, background jobs, analytics/read-only access, backups, and emergency recovery when their permissions differ.

- Runtime identities must not create roles, create databases, change policies, disable auditing, manage backups, or own application tables unless a documented design requires it.
- Grant access to named schemas, collections, tables, and operations. Avoid wildcards and provider owner/admin roles.
- Revoke broad defaults before adding narrow grants.
- Prefer workload identity or short-lived credentials. Where static credentials remain, store them in the approved secret manager and rehearse rotation.
- Keep local, test, staging, and production in separate projects/accounts or equivalent trust boundaries. Never let lower-environment credentials reach production.

## 4. Enforce Tenant and Object Scope

- Derive actor and tenant identifiers from verified identity or server-side membership data.
- Include the tenant predicate in every key, query, mutation, uniqueness constraint, cache key, job payload, file path, search document, and export path where the resource is tenant-owned.
- Preserve tenant and owner fields on update. Reject client attempts to transfer them unless an explicit, separately authorized workflow exists.
- Use database RLS or provider rules where their identity and policy model fits. Test owner/bypass behavior, overlapping policies, views/functions, server SDK bypasses, and policy freshness.
- Where the database lacks row policies, keep it behind trusted code, narrow the database role, and make scoped repositories or commands difficult to call without tenant context.

## 5. Constrain Inputs and Queries

- Validate payload type, shape, size, allowed fields, and business preconditions at the trusted boundary.
- Use parameter binding for values. Dynamic table, column, sort, operator, or path selection requires a fixed allow-list.
- For document databases, never pass user objects directly as filters or updates; construct the exact filter and allowed `$set`/equivalent fields.
- Limit page size, query complexity, fan-out, transaction duration, batch size, retries, and expensive scans before work begins.
- Use uniqueness, foreign keys, checks, validators, conditional writes, transactions, or compare-and-set behavior for critical invariants. Application pre-checks alone are race-prone.

## 6. Protect Network, Transport, and Secrets

- Prefer private connectivity when requirements and cost justify it. Otherwise restrict source networks where supported and require certificate and hostname verification.
- Keep database/control-plane endpoints out of browser and mobile bundles unless the service explicitly uses a publishable client API.
- Record secret name, owner, purpose, scope, store, rotation, revocation, and consumers—never its value.
- Redact connection strings, tokens, query parameters, personal data, and sensitive document fields from logs, traces, errors, build output, plans, and support artifacts.

## 7. Make Changes Recoverable

- Put schema, indexes, roles, grants, rules, and policy changes under version control and review them together.
- Expand before contract for compatibility-sensitive changes. Define lock/time thresholds, mixed-version behavior, abort criteria, data validation, and rollback or roll-forward.
- Backups must cover every system of record, including file/object data that a database backup omits.
- Test restoration into an isolated destination, then verify schema, permissions, tenant isolation, counts, invariants, representative journeys, and achieved RPO/RTO.
- Treat replicas and synchronization as availability tools, not independent backups.

## 8. Observe Abuse, Failure, and Cost

Monitor authentication failures, denied access, privileged actions, schema/policy changes, connection saturation, slow/error queries, storage, replication or backup health, restore readiness, quota consumption, unusual exports, and spend.

Alerts need an owner, threshold, runbook, and test. Store only the minimum query and identity detail needed for operations; access-control audit data is itself sensitive.

## Required Verification Matrix

| Area | Required evidence |
|---|---|
| Identity | invalid, expired, revoked, wrong-audience, and missing identity denied |
| Authorization | own resource allowed; another user, role, and tenant denied across direct and indirect paths |
| Mutation | immutable tenant/owner fields preserved; invalid state and duplicate/concurrent actions rejected |
| Injection | bound values used; dynamic identifiers/operators allow-listed; document operator injection rejected |
| Privilege | runtime identity cannot migrate, administer, read forbidden objects, or bypass policy |
| Failure | timeout, retry, connection loss, quota, provider outage, and ambiguous commit handled without corrupting invariants |
| Recovery | isolated restore meets or explicitly misses RPO/RTO; permissions and critical journeys verified |
| Exit | representative data and schema exported in a documented portable format and import feasibility checked |

## R3 Stop Points

Immediately before creating a paid resource or credential, changing production network/policy/schema, migrating or exporting real data, restoring, failing over, deleting, or disconnecting a live service, present the exact target, data affected, cost, evidence, backup, abort signal, rollback/recovery, and required authorization. This playbook never supplies that authorization.

