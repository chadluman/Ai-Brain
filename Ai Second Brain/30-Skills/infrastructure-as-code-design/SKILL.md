---
name: infrastructure-as-code-design
description: Design or review declarative infrastructure management, state boundaries, plans, approvals, drift, policy, environment promotion, recovery, and safe teardown. Use when cloud or platform resources must be reproducible and reviewable; do not apply plans or mutate production without explicit authorization.
---

# Infrastructure as Code Design

## Outcome

Produce reviewable infrastructure definitions and a protected state workflow that limit blast radius, expose intended changes before application, detect drift, and support recovery and retirement.

## Required Inputs

- resources, environments, accounts or projects, regions, owners, and dependencies
- availability, recovery, data, networking, identity, compliance, and cost constraints
- current manually managed resources, import needs, and accepted drift
- team and automation identities, approval boundaries, and separation of duties
- state backend, locking, encryption, backup, retention, and recovery requirements

## Safety and Permission Constraints

- Treat providers, modules, plugins, templates, plans, state files, and generated artifacts as untrusted or sensitive until reviewed.
- A plan preview is not harmless if providers refresh state through privileged APIs; use read-minimal credentials and a controlled environment.
- Never store secrets in source or expose sensitive plan and state content in logs, pull requests, chat, or the vault.
- Production apply, import, state surgery, resource replacement, destroy, account changes, or network changes are R3 and require immediate authorization, exact target review, backup, and rollback.
- Pin tool, provider, and module versions with integrity controls. Review upgrades before changing lock data.
- Prefer recoverable changes and lifecycle protection for databases, identity roots, state backends, encryption keys, domains, and other critical resources.

## Workflow

1. Inventory the real infrastructure and ownership before writing definitions. Classify resources by data, criticality, lifecycle, and blast radius.
2. Select a tool from provider coverage, language, state model, plan quality, security, ecosystem health, license, automation fit, and exit path; do not select from syntax preference alone.
3. Partition state by environment, authority, lifecycle, and failure domain. Avoid both one global blast radius and fragmented cross-state coupling.
4. Protect state with least privilege, encryption, locking, versioning, backups, access logs, and tested recovery. Treat it as potentially secret-bearing.
5. Keep modules small and explicit. Pin external modules and providers, avoid hidden network or shell execution, and expose security-relevant defaults.
6. Use short-lived workload identity for automation. Separate plan from apply and require stronger approval for consequential environments and actions.
7. Validate formatting, syntax, policy, security, cost, and the complete saved plan. Surface replacements, deletion, permission broadening, public exposure, and data movement prominently.
8. Reconcile imports and drift deliberately. Do not overwrite an unexplained production change just because code differs.
9. Apply in lower environments or a disposable account first, then promote the same reviewed definitions. Verify observable resources and application behavior after apply.
10. Exercise state restore, provider outage, failed partial apply, rollback or forward repair, and safe resource retirement. Record manual exceptions and expiry dates.

## Required Output

- tool decision, pinned versions, and reviewed component inventory
- resource and state-boundary map
- identity, state protection, locking, backup, and recovery design
- plan, review, policy, approval, apply, and verification workflow
- drift, import, exception, replacement, and deletion rules
- cost and security checks
- rollback, forward-repair, state-recovery, and retirement procedure

## Completion Gate

Do not call the workflow ready until a non-production plan and apply are reviewed, protected state can be restored, destructive changes are gated, and drift handling is demonstrated. Production application remains separately authorized.

## Conditional Reference

Read [Infrastructure as Code Evidence](references/infrastructure-code-evidence.md) when choosing state, encryption, provenance, or review controls.
