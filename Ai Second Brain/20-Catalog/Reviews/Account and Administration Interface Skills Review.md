---
status: reviewed
owner: vault-owner
created: 2026-10-25
last_verified: 2026-10-25
review_by: 2027-01-25
risk: R0
tags: [review, skills, account-management, administration, dashboards]
sources: []
---

# Account and Administration Interface Skills Review

## Assets and Purpose

This record covers three locally authored, documentation-only skill packages:

| Skill | Owned boundary |
|---|---|
| [Account Management Experience](../../30-Skills/account-management-experience/Account%20Management%20Experience.md) | User-facing account, security, session, identity, membership, privacy, export, closure, and deletion settings |
| [User Administration Console](../../30-Skills/user-administration-console/User%20Administration%20Console.md) | Staff and tenant-admin user discovery, inspection, privileged commands, exact selection scope, and bulk-operation recovery |
| [Management Dashboard Design](../../30-Skills/management-dashboard-design/Management%20Dashboard%20Design.md) | Decision-centered metric contracts, lineage, freshness, comparison, accessible visualization, drill-down, report, and alert behavior |

The packages intentionally do not own authentication selection, authorization policy, account or tenant state machines, privileged-session infrastructure, event collection, audit storage, or data deletion mechanics. They route those concerns to existing specialist skills.

## Provenance, Version, and License

- Source: authored locally in this vault by Codex for the vault owner on 2026-10-25; no third-party skill, template, source code, binary, package, or generated asset was imported.
- Version: the exact reviewed files are identified by SHA-256 below. Any content change requires at least a focused re-review; material scope or behavior changes require full re-review.
- Evidence: linked W3C, NIST, CISA, OWASP, USWDS, and GOV.UK documentation was read as untrusted R0 reference material and qualified in the [Source Registry](../Sources/Source%20Registry.md). No source's instructions override the repository contract.
- License: no repository-level license was identified. The skill text is therefore approved only for use within this vault; redistribution or relicensing remains unresolved. External prose and code were not copied into the packages.

## Exact Reviewed Inventory

| SHA-256 | File |
|---|---|
| `f5d17dde793390b090f8e8ba9586eafbc7b380c9e7e22cb14d0697bd20c1b01f` | `30-Skills/account-management-experience/Account Management Experience.md` |
| `dcb9a354a762873fcc1209b9db2398d24ddb395a0d5e4db0254ffa17ce2f7d51` | `30-Skills/account-management-experience/references/account-management-experience-evidence.md` |
| `0b0eae0e9d2750258eb8deb5b79bd3b3cc7cda190494607434872175966756aa` | `30-Skills/account-management-experience/SKILL.md` |
| `62c19b065f2b3dd72fd04d2b4d2e48ec3d5ccbf281936e49bee1c518c3ead5d2` | `30-Skills/user-administration-console/references/user-administration-console-evidence.md` |
| `f1c29aac84d30bf56210d21ac8313078db2c08f83e6a8bdc7d9e6c2d45bb78f0` | `30-Skills/user-administration-console/SKILL.md` |
| `2c67b7558e4f0244a63d99768cb91d50d457058ef0826fe01ea6e49ec03a89c4` | `30-Skills/user-administration-console/User Administration Console.md` |
| `7a187d6ff287b7552f0512f14ccd7d2110c50e58930da01d2d4c0ec878514b66` | `30-Skills/management-dashboard-design/Management Dashboard Design.md` |
| `68b29e4c397f7019983802138d84893c28cb0269d6bd055288a22d53b3d7a02e` | `30-Skills/management-dashboard-design/references/management-dashboard-design-evidence.md` |
| `31e4b72e8304c7d9af108176804a589e54b3ba91238b01f158f4bfa969687944` | `30-Skills/management-dashboard-design/SKILL.md` |

## Risk, Permissions, Dependencies, and Data Handling

- Risk: R0. The reviewed packages contain nine Markdown files and no hidden files, scripts, binaries, archives, lockfiles, install hooks, agent configuration, prompts for external execution, or generated assets.
- Required permissions at use time: read these local notes and the minimum linked local skills needed for the request. The skills grant no permission to inspect real users, connect an identity provider, read production data, change accounts, export records, publish dashboards, or contact people.
- Dependencies: none. The packages do not require a library, framework, plugin, service, account, credential, secret, or network connection.
- Network destinations: none during normal invocation. Following an evidence link is a separate research action governed by the repository research and permission rules.
- Telemetry and data handling: none. The instructions prohibit storing real credentials, secrets, recovery material, or account identifiers in the vault and require synthetic examples for design work.
- Consequential operations: all real account, privilege, export, production-data, alert, publication, or dashboard-access changes remain R3 and require immediate authorization, exact scope, and rollback or recovery.

## Findings and Mitigations

1. **Scope collision:** account lifecycle, authorization, privileged access, analytics, and dashboard UI could easily become one catch-all. The packages assign separate self-service, privileged-operator, and management-decision boundaries and link to existing sources of truth.
2. **UI mistaken for enforcement:** every mutation, row, field, export, and drill-down is explicitly treated as untrusted presentation. The skills require current server-side authorization and trusted state at execution.
3. **High-impact ambiguity:** sensitive and bulk actions require named targets, exact selection semantics, consequence previews, assurance proportional to harm, idempotency, partial-result handling, audit, and reversal or compensation.
4. **Misleading dashboards:** the dashboard skill requires metric contracts, lineage, reconciliation, freshness, missingness, denominator and comparison integrity, accessible equivalents, and prohibited-use statements.
5. **Privacy and accessibility:** all three skills minimize personal data, preserve account and tenant boundaries, include complete non-success states, and route conformance or governance work to specialist skills.
6. **Dependency and supply-chain exposure:** no implementation library or starter asset is recommended or bundled. Any later design system, table, chart, identity, or analytics dependency must pass its own exact-version review.

No obfuscation, encoded payload, dynamic download, shell construction, privilege escalation, persistence, destructive command, prompt-injection instruction, analytics, tracking, or credential access was found.

## Test Evidence

- The bundled skill validator passed all 125 skill folders with 125 unique frontmatter names.
- A vault-wide link check resolved 401 Markdown notes with zero missing relative links, zero missing Wikilinks, and zero ambiguous Wikilinks.
- The Source Registry contains the new evidence links with verification dates and source boundaries. Five duplicate URL occurrences already exist elsewhere in the registry; none is one of the ten sources added for these packages.
- Manual synthetic trace: an account with a pending contact change, multiple authenticators, and an organization-managed membership preserved separate authority, assurance, notification, and no-stranding rules.
- Manual synthetic trace: a tenant administrator changed filters after selecting a page of users; the console contract required explicit selection scope, target-set revalidation, eligible and excluded counts, item-level outcomes, and idempotent recovery.
- Manual synthetic trace: a partial current-month metric with a delayed source and a small sensitive segment remained distinguishable from zero or a completed period and required freshness, comparison, and cohort safeguards.

No live account, provider, user directory, production data source, dashboard, charting library, assistive-technology session, or real administrative operation was used.

## Decision and Conditions

Decision: `approved-with-conditions` as R0 draft instruction assets for architecture and interface planning. They are not approved as proof that any account system, administrative console, dashboard, authorization model, metric, accessibility claim, or production operation is safe or complete.

Conditions:

- Keep each skill `draft` until it succeeds on a representative request and its observable output is reviewed against the completion gate.
- Use synthetic data for design and testing unless separate authorization covers protected data.
- Run specialist authorization, security, privacy, accessibility, lifecycle, audit, and analytics reviews when those boundaries are material.
- Review every implementation dependency and external service before installation or activation.
- Obtain immediate R3 authorization before any real account, privilege, data-access, export, publication, alert, or production change.

## Removal and Re-Review

Removal is local and reversible from a prior vault backup: remove the three exact skill folders, their Skills Map and Research Queue entries, the three inbound canonical-skill routes, and source rows that have no remaining consumer. Re-run skill and link validation after removal. No account, provider, service, package, or external state needs disconnection.

Re-review by 2027-01-25, or earlier after the first representative use, a failed completion gate, a material change to linked identity or accessibility standards, a new administrative or dashboard dependency, scope expansion, real-data use, an authorization or privacy incident, a misleading metric decision, or observed operator or user harm.
