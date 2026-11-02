---
name: tenant-lifecycle-operations
description: Design or review organization and tenant creation, verification, provisioning, invitations, membership, ownership, domain claims, suspension, transfer, merge, split, export, offboarding, and deletion. Use for multi-tenant SaaS lifecycle operations after tenant authorization boundaries are defined.
---

# Tenant Lifecycle Operations

## Outcome

Produce an explicit tenant state machine in which identity, ownership, resources, entitlements, integrations, data, access, billing, support, export, retention, and deletion change together safely without cross-tenant leakage or orphaned authority.

Use [Authorization and Tenancy Design](../authorization-tenancy-design/SKILL.md) for request enforcement, [Identity and Authentication Selection](../identity-auth-selection/SKILL.md) for users and federation, [Privileged Access Operations](../privileged-access-operations/SKILL.md) for staff intervention, and [Data Retention and Deletion Operations](../data-retention-deletion-operations/SKILL.md) for disposal. This skill owns tenant state transitions.

## Required Inputs

- tenant types, legal and billing owners, administrators, members, guests, services, support, resellers, parent-child relationships, and cross-tenant collaboration
- tenant isolation model, region, keys, storage, schema or database, files, queues, caches, search, analytics, logs, backups, configuration, domains, integrations, and identifiers
- self-service, sales-assisted, SCIM, SSO, invitation, verified-domain, transfer, merger, acquisition, split, sandbox, trial, suspension, cancellation, and deletion journeys
- plans, entitlements, quotas, invoices, credits, contracts, data residency, retention, legal holds, export, portability, and support obligations
- provisioning and deletion duration, retries, partial failure, reconciliation, manual repair, audit, notification, appeal, and rollback expectations

## Safety and Permission Constraints

- A tenant identifier supplied by a client is only a selector. Bind the tenant to authenticated membership and authorize every action at the trusted resource boundary.
- Domain possession, email suffix, SSO claim, billing contact, and SCIM record are evidence for specific claims, not automatic proof of tenant ownership or unrestricted administration.
- Provisioning and offboarding are distributed workflows. Never mark them complete from one successful API call; reconcile every resource, access path, integration, copy, and external provider.
- Prevent self-approval and single-actor hostile transfers for high-value tenants. Define notice, delay, dual control, dispute, and recovery proportional to harm.
- Creating, suspending, merging, transferring, exporting, restoring, or deleting real tenants; changing production domain claims, federation, billing, or residency; and accessing tenant data are R3 and require immediate authorization, ownership verification, and rollback or recovery.

## Workflow

1. Define tenant identity independently from user accounts and mutable names. Assign stable internal ID, display name, legal or contract identity where needed, region, lifecycle state, ownership, and authoritative sources.
2. Build a state machine for requested, verifying, provisioning, active, restricted, suspended, offboarding, retention-hold, deletion-pending, deleted, and recovery or failed states. Define allowed transitions, actor, proof, side effects, timeouts, retries, and reversal.
3. Provision idempotently from a durable workflow. Create policy, storage, keys where required, quotas, entitlements, billing link, default roles, audit context, indexes, queues, integrations, and observability; reconcile desired versus actual state after partial failure.
4. Design invitations, membership, group sync, service identities, and ownership change. Bind invitations to tenant, intended recipient or domain, role, expiry, single use, and revocation; prevent stale identity-provider data from preserving access after removal.
5. Verify and govern domain claims. Prove current control using a safe method, prevent one domain from silently attaching to multiple incompatible tenants, handle subdomains and aliases, reverify changes, and provide a dispute and recovery process.
6. Make entitlements, quotas, usage, billing state, and product access explicit and idempotent. Payment failure or trial end must not cause unsafe immediate deletion or leave paid external effects running without ownership.
7. Separate restriction, suspension, and deletion. Define allowed reads, writes, exports, support, security response, webhook behavior, background work, integrations, notifications, and restoration for each state.
8. Treat merge, split, transfer, and region move as migrations. Map identity collisions, memberships, domains, data, keys, invoices, entitlements, integrations, identifiers, audit history, retention, and external references; reconcile and preserve rollback before cleanup.
9. Offboard through verified authority, notice, export, integration disconnect, credential and session revocation, queued-work handling, retention or legal hold, primary and derived deletion, backup expiry, vendor confirmation, and minimal deletion evidence.
10. Test concurrent signup, duplicate requests, abandoned provisioning, invitation replay, domain takeover, stale SCIM or group data, owner loss, billing race, suspension bypass, cross-tenant jobs and caches, merge collision, export isolation, restore, deletion retry, retained backup, and support impersonation.

## Required Output

- tenant identity and state machine with actors, proof, transitions, effects, timeouts, retries, reversal, and notifications
- resource, isolation, region, key, entitlement, billing, domain, membership, integration, and ownership inventory
- idempotent provisioning, reconciliation, restriction, suspension, transfer, merge, split, export, offboarding, retention, and deletion workflows
- SCIM or federation boundary, staff authority, dispute, recovery, audit, monitoring, cost, and provider-exit plan
- cross-tenant, partial-failure, concurrency, migration, restore, and deletion test evidence

## Completion Gate

Do not call tenant lifecycle ready until every state constrains every entry point, desired and actual resources reconcile, invitations and domain claims cannot grant unintended authority, owner loss and transfer have safe recovery, suspension cannot be bypassed by jobs or integrations, offboarding revokes access and bounds cost, exports contain only the tenant, and deletion or retained-hold state is evidenced across all copies.

## Conditional Reference

Read [Tenant Lifecycle Evidence](references/tenant-lifecycle-evidence.md) when designing tenant isolation, SCIM provisioning, lifecycle security events, verified membership, onboarding, suspension, or offboarding.
