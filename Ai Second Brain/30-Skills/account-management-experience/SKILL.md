---
name: account-management-experience
description: Design or review user-facing account settings for profile, contact points, sign-in methods, authenticators, sessions, linked identities, preferences, privacy, export, and closure. Use for self-service account-management journeys; use user-administration-console for staff or tenant-admin operations.
---

# Account Management Experience

## Outcome

Produce a comprehensible, accessible account center in which a person can tell what represents them, what grants access, what is shared or public, what is organization-controlled, and what will happen before a sensitive change is committed.

This skill owns the self-service interaction contract. Route account states to [User Account Lifecycle](../user-account-lifecycle/SKILL.md), authentication choices to [Identity and Authentication Selection](../identity-auth-selection/SKILL.md), lost-access restoration to [Account Recovery Security](../account-recovery-security/SKILL.md), sessions to [Session and Cookie Security](../session-cookie-security/SKILL.md), and data rights or disposal to [Privacy and Data Governance](../privacy-data-governance/SKILL.md) and [Data Retention and Deletion Operations](../data-retention-deletion-operations/SKILL.md).

## Required Inputs

- account, profile, contact-point, authenticator, linked-identity, session, device, membership, subscription, entitlement, and retention models
- user types, assurance needs, accessibility and localization requirements, support capacity, and likely compromise or shared-device scenarios
- which values are self-managed, organization-managed, provider-managed, public, verified, pending, restricted, or immutable
- reauthentication, verification, notification, recovery, cancellation, appeal, export, closure, and deletion policies
- supported channels, provider dependencies, asynchronous delays, outage behavior, and authoritative systems

If one field ambiguously serves as display name, public identity, login identifier, contact channel, recovery channel, and ownership proof, resolve those meanings before designing the settings experience.

## Safety and Permission Constraints

- A visible or editable control is not authorization. Enforce every read and mutation at the trusted server boundary using the current account, tenant, resource, and policy state.
- Do not present an email address, phone number, username, provider profile, or tenant membership as if it were the stable product account. Label each role and source of authority truthfully.
- Minimize displayed personal data, mask sensitive values, prevent shared-device disclosure, and never reveal credential material, raw tokens, secret values, or complete recovery artifacts after issuance.
- Let users inspect consequences before a sensitive action. Apply recent authentication, independent verification, established-channel notice, cooling-off, dual control, or support review according to risk; do not use friction as a substitute for a defined policy.
- Never let linking, unlinking, contact replacement, authenticator removal, or closure strand a user without an approved remaining access or recovery path. Do not imply that a closure request equals immediate deletion from every retained or backed-up copy.
- Changing a real account, identity, authenticator, session, membership, subscription, export, privacy choice, or closure state is R3. Require immediate authorization, exact target and consequence review, observable outcome, and a tested recovery or compensation path.

## Workflow

1. Model the user's account concepts. Separate stable account identity, profile, public identity, contact points, login identifiers, authenticators, recovery methods, sessions, devices, tenant memberships, entitlements, billing, preferences, and retained data.
2. Build task-first information architecture around the user's language and frequency of need. Keep ordinary preferences easy to reach while making security, privacy, export, and closure discoverable rather than hidden behind support or misleading labels.
3. Define a contract for every setting: purpose, displayed value and masking, authority, who may change it, required assurance, validation, pending state, side effects, notification, audit event, failure recovery, reversal, and support boundary.
4. Design an account overview that exposes material state without leaking detail: verification and protection gaps, active or pending changes, unfamiliar sessions or identities, organization control, billing or ownership obligations, and unresolved restrictions.
5. Design sensitive-change journeys as explicit transactions. Name the target and consequence, preserve user input through reauthentication, verify the replacement independently, notify previously established channels when safe, expose pending or delayed state, and provide cancellation, dispute, or recovery where policy permits.
6. Make authenticator and session management legible. Distinguish sign-in methods from recovery methods, show recognizable device and activity context without overstating location accuracy, protect the current session from accidental removal, and make revoke-all scope and propagation delay explicit.
7. Explain organization-managed settings and memberships. Show which organization controls a value, the user's role, how to leave or transfer obligations, and whether a tenant action affects only that membership or the global account.
8. Design privacy, export, closure, and deletion controls around truthful lifecycle states. Explain scope, format, timing, retention, holds, subscription or ownership blockers, cooling-off and restoration, and what the user can do while work is pending.
9. Specify loading, empty, partial, stale, offline, unauthorized, locked, provider-outage, conflict, success, failure, and delayed-completion states. Preserve focus and announce material status; do not rely on color, icons, hover, memory tests, or inaccessible CAPTCHAs to communicate or authorize change.
10. Test with keyboard, screen reader, zoom, small viewport, password manager, long localized content, shared device, concurrent tabs, stale account state, provider delay, lost authenticator, compromise, interrupted reauthentication, notification failure, and downstream partial failure.

## Required Output

- account concept model and task-centered settings map
- per-setting authority, visibility, editability, assurance, validation, notification, audit, failure, and recovery contract
- account overview and sensitive-change, identity, authenticator, session, membership, privacy, export, closure, and deletion flows
- complete state matrix with accessible status, responsive behavior, and localization constraints
- server-enforcement, provider, support, audit, reconciliation, and lifecycle handoffs
- adversarial, accessibility, concurrency, outage, and partial-failure test evidence with unresolved decisions and owners

## Completion Gate

Do not call the experience ready until users can distinguish account concepts and authority, every mutation maps to a server-enforced transition, sensitive changes preserve intent through assurance steps, no flow silently strands access, pending and partial states are truthful, privacy and closure language matches actual retention, and critical journeys pass accessibility, concurrency, and recovery tests.

## Conditional Reference

Read [Account Management Experience Evidence](references/account-management-experience-evidence.md) when designing sensitive account changes, reauthentication, status and error communication, accessible authentication, or settings that affect identity, access, privacy, export, or closure.
