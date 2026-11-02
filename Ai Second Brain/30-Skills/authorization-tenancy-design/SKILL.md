---
name: authorization-tenancy-design
description: Design or review application authorization, object access, tenant isolation, policy enforcement, revocation, and authorization tests after identity is known. Use for roles, permissions, ABAC, ReBAC, admin or support access, and multi-tenant data boundaries; do not use as the primary authentication or identity-provider selection guide.
---

# Authorization and Tenancy Design

## Outcome

Produce a deny-by-default authorization model that states who may perform each action on which resource, under what context, and across which tenant boundary, with enforceable tests and auditable failure behavior.

## Required Inputs

- actors, service identities, resources, actions, and sensitive fields
- tenant, organization, ownership, delegation, and sharing relationships
- lifecycle events such as invitation, suspension, revocation, deletion, and ownership transfer
- privileged administration, support, impersonation, emergency access, and approval rules
- latency, availability, policy-freshness, audit, privacy, and compliance constraints
- every entry point that can reach protected work, including APIs, jobs, exports, search, files, and internal tools

If the resource invariants or tenant boundaries are unknown, stop before selecting an authorization product.

## Safety and Permission Constraints

- Treat authentication as identity evidence, not permission.
- Deny by default and authorize every protected operation at the trusted server or resource boundary.
- Never rely on hidden UI controls, opaque identifiers, client claims, or a gateway check as the only enforcement.
- Bind subject, action, resource, tenant, and relevant context explicitly. Fail closed when required policy or attributes are missing, invalid, stale, or unavailable.
- Do not log secrets, tokens, or unnecessary sensitive attributes. Make audit records tamper-resistant and access-controlled.
- Treat production policy changes, cross-tenant access, impersonation, emergency access, or real-data permission migration as R3 actions requiring immediate user authorization and a tested rollback.
- Review any policy engine, SDK, sidecar, or hosted authorization service as an executable third-party asset before adoption.

## Workflow

1. Write resource and action invariants in product language, including negative rules and separation-of-duty constraints.
2. Create an access matrix for ordinary users, owners, staff, services, and exceptional roles. Include object state and tenant scope.
3. Choose the smallest fitting model:
   - use direct ownership or simple role checks when the domain is small and stable;
   - use attributes for contextual rules and relationship rules for resource graphs;
   - combine models only when the invariants require it, not because a product supports them.
4. Define policy decision and enforcement locations. Keep the final enforcement close to the protected operation and cover alternate paths such as bulk actions, exports, jobs, and direct-object routes.
5. Define trusted sources, validation, freshness, caching, propagation, revocation deadlines, and outage behavior for every security-relevant attribute and policy.
6. Enforce tenant predicates in data access as well as business logic. Prevent unscoped queries, cross-tenant cache keys, file-path leakage, search leakage, and background-job context loss.
7. Design privileged access with explicit purpose, short duration, strong authentication, user-visible or independently reviewed audit where appropriate, and a kill switch.
8. Test permitted and denied cases, horizontal and vertical escalation, cross-tenant identifiers, stale grants, revoked sessions, bulk and indirect paths, policy-engine failure, and race conditions.
9. Record the decision in an ADR when the model, engine, or tenancy boundary materially affects architecture or migration.

## Required Output

- authorization invariants and access matrix
- selected model with rejected alternatives and evidence
- tenant-boundary and enforcement design
- policy and attribute sources, freshness limits, and failure behavior
- privileged-access and audit design
- negative test matrix and verification evidence
- migration, rollback, and unresolved-risk notes

## Completion Gate

Do not call the design complete until every protected operation has an enforcement point, denied cases and tenant isolation have been tested, and revocation and dependency-failure behavior are observable. Keep the skill draft until it succeeds on a realistic threat-flow review.

## Conditional Reference

Read [Authorization Evidence](references/authorization-evidence.md) when choosing an access-control model, enforcement topology, or test baseline.
