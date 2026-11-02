---
name: privileged-access-operations
description: Design or review administrative, support, production, break-glass, impersonation, and just-in-time access operations. Use when humans or automation can change security, identity, data, infrastructure, billing, deployments, moderation, or other high-impact systems.
---

# Privileged Access Operations

## Outcome

Produce a least-privilege operating model in which elevated access is separate, strongly authenticated, purpose-bound, approved when warranted, time-limited, observable, reviewable, revocable, and safe during emergencies.

Use [Authorization and Tenancy Design](../authorization-tenancy-design/SKILL.md) for application policy, [User Administration Console](../user-administration-console/SKILL.md) for privileged user-management interaction, [Audit Log Design](../audit-log-design/SKILL.md) for evidence, [Secrets and Configuration Management](../secrets-config-management/SKILL.md) for credentials, and [Incident Response](../incident-response/SKILL.md) for emergency coordination. This skill owns operational elevation and human or automated privileged sessions.

## Required Inputs

- privileged actions, protected resources, data classes, environments, tenants, systems, blast radius, irreversible effects, regulatory duties, and availability needs
- administrators, developers, support, moderators, vendors, service accounts, automation, incident responders, approvers, reviewers, and emergency roles
- identity provider, phishing-resistant authentication, device trust, network and console paths, privileged-access platform, logging, ticketing, secrets, and recovery capabilities
- standing roles, dormant accounts, group and role propagation, session lifetime, credentials, impersonation, exports, data repair, deployment, billing, identity, and security changes
- on-call, incident, provider outage, lost authenticator, identity-provider failure, and disaster-recovery scenarios

## Safety and Permission Constraints

- Separate ordinary and privileged identities or sessions. Do not use shared administrator accounts except a tightly controlled emergency mechanism with individual attribution before and after use.
- Require phishing-resistant authentication and reauthentication appropriate to the action. A VPN, office network, or existing session alone does not justify elevation.
- Never expose secrets, recovery material, full sensitive records, or unrestricted production consoles merely for convenience. Mask data and prefer task-specific operations, read-only views, synthetic data, or audited repair tools.
- Impersonation must be exceptional, visibly indicated, purpose- and tenant-bound, unable to reveal user credentials, and designed with notice or policy appropriate to the context. It must not bypass stronger transaction confirmation invisibly.
- Granting, using, or revoking real production privilege; viewing private data; impersonating users; changing billing, identity, security, infrastructure, or deployment state; or invoking break-glass is R3 and requires immediate authorization or a pre-authorized emergency policy with after-action review.

## Workflow

1. Inventory every privileged action and path, including web consoles, APIs, shells, databases, cloud control planes, support tools, CI, vendor access, local accounts, scripts, and recovery consoles. Assign owner, risk, environment, tenant scope, and required evidence.
2. Remove unnecessary standing access. Define task-specific roles and separate production, non-production, billing, security, identity, support, data, and deployment powers. Prevent a single broad role from becoming the default.
3. Establish an individually attributable administrative identity with phishing-resistant authentication, managed recovery, device or posture requirements where justified, short privileged sessions, reauthentication for sensitive actions, and no routine email or browsing use.
4. Design just-in-time elevation: eligible population, requested role and resource, business purpose, ticket or incident, approver independence, policy checks, start, maximum duration, automatic expiry, extension, revocation, and emergency override.
5. Add dual control or separate approval for high-impact or irreversible actions such as key destruction, mass export or deletion, payout changes, identity-provider policy, audit disabling, production data repair, and break-glass credential rotation.
6. Constrain support and impersonation. Show the actor that they are elevated, bind to one user or tenant and purpose, mask unnecessary fields, block credential and secret access, require reasons, prevent silent privilege escalation, and make termination immediate.
7. Capture authoritative events for request, approval, denial, grant, start, command or high-level action as appropriate, resource, tenant, reason, outcome, expiry, revocation, emergency use, and reviewer. Protect log integrity while minimizing sensitive command output and personal data.
8. Maintain independently protected break-glass paths for identity-provider or control-plane outage. Limit accounts and capabilities, store credentials under split or controlled custody, alert on every access attempt, rotate after use, and test availability without exposing secrets.
9. Review entitlements on join, move, leave, role change, inactivity, incident, vendor end, and a risk-based schedule. Reconcile actual provider and local permissions rather than trusting only the central directory.
10. Test unauthorized and expired elevation, approval bypass, self-approval, tenant crossing, role-propagation delay, concurrent revocation, lost device, compromised operator, support social engineering, audit failure, IdP outage, emergency access, restore, and complete offboarding.

## Required Output

- privileged action and access-path inventory with blast radius and owners
- role and separation model, administrative identity, strong-authentication, device, session, reauthentication, and data-minimization rules
- just-in-time request, approval, grant, expiry, extension, revocation, dual-control, support, and impersonation workflows
- audit schema, alerting, entitlement review, vendor, offboarding, emergency, compromise, migration, and rollback procedures
- negative, outage, break-glass, revocation, tenant, and operator-recovery test evidence

## Completion Gate

Do not call privileged access ready until all paths are inventoried, standing power is minimized, operators are individually attributable and strongly authenticated, grants expire automatically, high-impact actions have appropriate separation, impersonation is visible and bounded, every use is reviewable, removal is reconciled at the provider, and break-glass and revocation have passed controlled tests.

## Conditional Reference

Read [Privileged Access Evidence](references/privileged-access-evidence.md) when designing phishing-resistant administration, separate accounts, just-in-time elevation, zero-trust resource decisions, logging, or emergency access.
