---
name: user-account-lifecycle
description: Design or review individual user-account creation, identity binding, identifier changes, restriction, suspension, reactivation, closure, and re-registration. Use when account state or sign-in identities can change; use tenant-lifecycle-operations for organization lifecycles and account-recovery-security for lost-authenticator recovery.
---

# User Account Lifecycle

## Outcome

Produce an explicit account state machine that preserves identity, authorization, privacy, and product invariants from enrollment through closure without treating a mutable email address, phone number, username, or external identity as the account itself.

## Required Inputs

- account types, users, age and jurisdiction constraints, and self-service, administrator, support, or enterprise-provisioning actors
- local account identifiers, usernames, contact points, authenticators, federated identities, verification state, and assurance requirements
- memberships, ownership, authorization, entitlements, billing, content, files, jobs, notifications, integrations, and audit dependencies
- restriction, suspension, appeal, reactivation, closure, retention, hold, deletion, and re-registration policies
- provider behavior, event ordering, outage tolerance, support capacity, notification channels, and recovery paths

If the product cannot distinguish a person, product account, sign-in identity, authenticator, contact address, profile, and tenant membership, resolve that model before designing transitions.

## Safety and Permission Constraints

- Give every product account a stable, opaque, non-reassigned internal identifier. Do not use email, phone number, username, display name, or another provider's mutable claim as the primary identity key.
- Treat account linking, unlinking, identifier changes, suspension, and closure as security-sensitive transitions. Require assurance proportional to the consequence and notify through previously established channels when safe.
- Do not automatically link accounts merely because profile attributes match. For federation, bind the exact trusted issuer and subject; prove control of the existing account and the identity being added.
- Distinguish `restricted`, `suspended`, `disabled`, `closure-pending`, `closed`, `anonymized`, and `deleted` where their effects differ. A UI state or identity-provider deletion is not proof that retained, derived, vendor, or backup data was deleted.
- Never store credentials, identity documents, personal data, recovery artifacts, or real account identifiers in the vault. Use synthetic examples.
- Creating, linking, unlinking, suspending, reactivating, merging, closing, deleting, bulk-provisioning, or migrating real accounts is R3. Require immediate authorization, exact targets, accountable ownership, user-impact review, monitoring, and a tested recovery or compensation path.

## Workflow

1. Define the account boundary and stable identity. Model product accounts separately from authenticators, contact points, federated subjects, profiles, tenant memberships, and provider directory objects.
2. Specify the state machine. Keep global account availability, tenant membership, enforcement, billing, and data-retention state separate when they can change independently. For every state and transition, record the initiating actor, authorization, recent-authentication requirement, guards, idempotency key, effects, notifications, audit event, failure state, and reversal or compensation.
3. Design enrollment and invitation. Minimize collected data, verify only what the purpose requires, bound duplicate and automated creation, make retries idempotent, and define when a pending record becomes an active account.
4. Design identity binding. Key federated identities by trusted issuer plus subject, require an authenticated existing account before linking, verify the new identity, prevent confused-deputy and account-takeover paths, and refuse unlinking that would strand the user without an approved access or recovery path.
5. Design sensitive attribute changes. Reauthenticate with an already bound method when appropriate, verify the replacement channel independently, notify established channels, rotate or revoke affected sessions, and handle concurrent, replayed, abandoned, and disputed requests.
6. Propagate lifecycle state to every enforcement point: sessions, tokens, authorization caches, memberships, ownership, entitlements, billing, jobs, notifications, devices, search, exports, support tools, vendors, and provisioned directories. Define which effects are synchronous and which converge through reconciliation.
7. Separate access removal from data disposition. Suspension should block defined access promptly without silently deleting evidence. Closure should address ownership transfer, subscriptions, export, appeal or cooling-off windows, retention, holds, derived data, vendor propagation, backup expiry, and restore anti-resurrection.
8. For enterprise provisioning, define the authoritative source, managed scope, and attribute precedence. Map create, update, deactivate, reactivate, and delete signals into local states without assuming that SCIM `active: false`, directory removal, or one missed event expresses the product's complete policy. A tenant-scoped deprovisioning event must not disable unrelated memberships or a personal account.
9. Define reactivation and re-registration. Revalidate control and eligibility, resolve prior compromise or enforcement, prevent identifier reuse from inheriting old data or privileges, and make any restoration scope visible and auditable.
10. Test the transition matrix with duplicates, races, stale sessions, reordered or missing provider events, provider outage, account enumeration, unauthorized linking, last-identity unlinking, closure during paid or owned activity, appeal, re-registration, backup restore, and partial downstream failure.
11. Reconcile account and dependency state continuously. Alert on active access for suspended accounts, stranded active accounts with no access path, orphaned provider bindings, unowned resources, incomplete closure, and state drift.

Route self-service settings and sensitive-change interaction to [Account Management Experience](../account-management-experience/SKILL.md), authentication method and provider choice to [Identity and Authentication Selection](../identity-auth-selection/SKILL.md), protocol mechanics to [OAuth and OpenID Connect Integration Security](../oauth-oidc-integration-security/SKILL.md), lost-access restoration to [Account Recovery Security](../account-recovery-security/SKILL.md), session invalidation to [Session and Cookie Security](../session-cookie-security/SKILL.md), permissions to [Authorization and Tenancy Design](../authorization-tenancy-design/SKILL.md), organization lifecycle to [Tenant Lifecycle Operations](../tenant-lifecycle-operations/SKILL.md), and data disposal to [Data Retention and Deletion Operations](../data-retention-deletion-operations/SKILL.md).

## Required Output

- account, identity-binding, contact-point, authenticator, profile, and membership model
- state and transition table with actors, assurance, guards, effects, notices, audit, retries, and compensation
- enrollment, linking, unlinking, sensitive-change, suspension, reactivation, closure, appeal, and re-registration flows
- dependency-propagation and reconciliation plan with authoritative sources and failure ownership
- privacy, retention, deletion, export, billing, support, and enterprise-provisioning boundaries
- adversarial and failure test matrix, monitoring, runbooks, authorization gates, and unresolved qualified-review questions

## Completion Gate

Do not call the lifecycle ready until every transition has one authoritative owner, stable identity semantics, explicit security and user-impact controls, idempotent failure handling, downstream reconciliation, tested access revocation, and a truthful retention or deletion outcome. Do not merge ambiguous accounts or leave an account inaccessible merely because its last identity was removed.

## Conditional Reference

Read [User Account Lifecycle Evidence](references/user-account-lifecycle-evidence.md) when defining stable identifiers, federation links, provisioning states, sensitive changes, suspension, termination, or re-registration.
