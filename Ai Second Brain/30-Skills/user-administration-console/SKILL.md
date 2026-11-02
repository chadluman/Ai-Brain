---
name: user-administration-console
description: Design or review staff and tenant-admin consoles for finding users, inspecting account and membership state, changing roles or access, handling restrictions, and running safe bulk operations. Use for privileged user-management interfaces; use account-management-experience for end-user self-service settings.
---

# User Administration Console

## Outcome

Produce a task-centered administrative console that helps an authorized operator find the correct subject, understand current authority and state, perform only an allowed operation, preview its blast radius, recover from partial failure, and leave reviewable evidence.

This skill owns the administrative interaction and command surface. Route policy to [Authorization and Tenancy Design](../authorization-tenancy-design/SKILL.md), privileged-session controls to [Privileged Access Operations](../privileged-access-operations/SKILL.md), account states to [User Account Lifecycle](../user-account-lifecycle/SKILL.md), tenant membership and ownership to [Tenant Lifecycle Operations](../tenant-lifecycle-operations/SKILL.md), and evidence semantics to [Audit Log Design](../audit-log-design/SKILL.md).

## Required Inputs

- operator types, eligible roles, tenants, environments, approval rules, separation of duties, escalation paths, and support or impersonation policy
- managed populations, stable identifiers, account and membership states, identity sources, authoritative systems, sensitive fields, and legal or policy restrictions
- individual and bulk actions, reversibility, side effects, propagation deadlines, asynchronous jobs, notifications, audit events, and recovery paths
- expected record volume, query patterns, filters, sorting, pagination, exports, rate limits, concurrency, and provider dependencies
- accessibility, localization, privacy, data residency, retention, observability, and incident requirements

If the system cannot state whether an action targets a global account, one tenant membership, one identity binding, one entitlement, or one provider record, stop before designing the command surface.

## Safety and Permission Constraints

- The console is not a trusted boundary. Authorize every lookup, field, action, export, and bulk item on the server using the current operator, target, tenant, environment, resource state, and policy.
- Make operator identity, elevated state, environment, tenant, selected subjects, and requested scope continuously visible. Do not rely on color alone or a URL parameter to prevent wrong-environment or cross-tenant action.
- Default to the least personal data and least privilege needed for the task. Mask sensitive fields, separate routine support from security administration, and make exceptional access or impersonation visibly bounded and revocable.
- Use operation-specific input contracts and allow-list writable fields. A hidden or omitted role, verification, owner, tenant, enforcement, or billing field must never become writable through generic object binding.
- Search results, counts, checkboxes, cached roles, and loaded pages are not proof of current authority. Revalidate the exact target set and policy at execution; surface exclusions and state changes instead of silently broadening scope.
- Changing roles, identities, access, restrictions, sessions, tenant membership, ownership, billing, exports, or real user records is R3. Require immediate authorization or an approved operating policy, exact targets, reason and evidence, impact preview, monitoring, and reversal or compensation.

## Workflow

1. Inventory operator jobs and privileged actions. For each action define target entity, tenant and environment, required role and assurance, sensitivity, reversibility, approval, reason, notification, audit, propagation, and recovery.
2. Separate read, support, security, tenant administration, billing, moderation, and platform administration where their authority differs. Build task-based navigation and landing views rather than one universal super-admin surface.
3. Design directory and search behavior around stable identifiers and recognizable context. Define exact and fuzzy fields, normalization, enumeration controls, filters, sorting, pagination or cursor semantics, URL state, saved-view ownership, zero-result recovery, freshness, and result-count meaning.
4. Choose the simplest collection interaction. Prefer a semantic table or list for reading and comparison; use an ARIA grid only when application-like cell navigation or editing is genuinely required and its complete keyboard contract will be implemented and tested.
5. Make selection scope explicit. Distinguish this row, selected rows on this page, all loaded rows, and all results matching a named filter. Show the selected count and filter snapshot, support clearing, and never reinterpret a previous selection after filters or data change.
6. Design a subject detail view that distinguishes global account, identities, authenticators, contact points, tenant memberships, roles, entitlements, enforcement, sessions, ownership, billing, and provider state. Label authority, last update, pending work, conflicts, and data provenance.
7. Model each mutation as a named command, not a generic edit. Present allowed fields and target scope, obtain purpose and reason where required, show current and proposed state, perform step-up or approval at commit, enforce idempotency and concurrency preconditions, and return an authoritative result.
8. Match safeguards to consequence. Prefer undo or compensating action when safe; use review pages or focused dialogs for bounded decisions; require stronger proof, dual control, delay, or a separate workflow for irreversible, mass, cross-tenant, security, identity, ownership, export, or deletion actions.
9. Execute bulk work as a bounded job when necessary. Freeze or identify the requested set, preflight permissions and invariants, show exact eligible and excluded counts, cap blast radius, support cancellation before commit where possible, record item-level results, retry idempotently, and reconcile partial completion.
10. Design optimistic and stale-state handling. Show versions and pending changes where useful, refuse lost updates, refresh authorization at commit, and explain when another operator, directory, job, or policy changed the target.
11. Expose relevant audit and history without leaking secrets or unrestricted personal data. Let an operator trace request, approval, actor, target, reason, before-and-after meaning, result, notification, expiry, reversal, and correlation to provider or background work.
12. Test direct-object access, hidden-field injection, horizontal and vertical privilege escalation, tenant and environment confusion, stale roles, selection drift, pagination changes, concurrent edits, duplicate submission, approval bypass, partial bulk failure, revocation during execution, keyboard and screen-reader operation, zoom, narrow viewport, long content, and provider outage.

## Required Output

- operator-job, action-risk, role, tenant, environment, approval, and separation matrix
- navigation, directory, search, filter, sort, pagination, selection, detail, history, and empty/error state specification
- command contracts with targets, allow-listed inputs, assurance, preconditions, idempotency, side effects, notices, audit, reversal, and reconciliation
- individual and bulk action flows with preflight, preview, partial-result, retry, cancellation, and recovery behavior
- data minimization, accessibility, localization, concurrency, provider, support, and observability requirements
- adversarial and failure test matrix with evidence, unresolved risks, accountable owners, and production authorization gates

## Completion Gate

Do not call the console ready until every visible field and action has server-enforced authorization, operator and target context cannot be confused, selection scope is exact, command inputs are allow-listed, high-impact work has proportionate assurance and preview, stale and partial outcomes are recoverable, all changes are attributable, and critical read and action flows pass accessibility and adversarial tests.

## Conditional Reference

Read [User Administration Console Evidence](references/user-administration-console-evidence.md) when designing searchable user tables, selection, administrative dialogs, sensitive commands, bulk changes, role or identity edits, privileged access, or audit-visible outcomes.
