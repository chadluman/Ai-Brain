---
status: reviewed
owner: vault-owner
created: 2026-10-22
last_verified: 2026-10-22
review_by: 2027-01-22
risk: R0
tags: [catalog, security-review, skill, teaching, web-development, certification]
sources:
  - https://www.coitb.org/certification-resources/badges/html-css-web-designer
  - https://www.coitb.org/certification-resources/exam-outlines/html-css-web-designer-outline
  - https://html.spec.whatwg.org/
  - https://www.w3.org/TR/css-2026/
  - https://www.w3.org/TR/WCAG22/
---

# Security Review — Senior Web Development Teaching Skills

## Identity and Scope

- Asset type: locally authored Markdown skill family
- Purpose: route web-development teaching through a shared project-based lesson contract, seven broad subject modules, and a focused COITB HTML/CSS certification-preparation module
- Source: this vault; no third-party package or copied curriculum
- Author or organization: vault owner and Codex
- Exact version: 1.1.0, local revision dated 2026-10-22; checksums are recorded below
- License: no repository license was identified; treat the original text as internal-use material until the owner assigns reuse terms
- Proposed use: automatically route tutoring, curricula, mentoring, code walkthroughs, and assessment requests to the smallest relevant maintained domain skills

## Decision Summary

- Assigned risk: R0 for the Markdown assets themselves
- Decision: approved-with-conditions
- Conditions: keep all modules draft until realistic learner validation; recheck version-sensitive and COITB exam claims through the routed evidence; preserve dependency review and R3 authorization boundaries; use security exercises only in authorized isolated environments; use only original practice items
- Decision owner: vault-owner
- Next review: 2027-01-22, or earlier after the first substantive curriculum, repeated routing failure, material file change, new executable resource, or safety failure

## Complete Inventory

| Path | Purpose | SHA-256 | Reviewed? |
|---|---|---|---:|
| `30-Skills/teach-senior-web-development/SKILL.md` | Main teaching stance, workflow, subject router, and boundaries | `94B424ACB18A8DEA940EECCE95E617B071354728373A5DF51C03BEC2B39AAAA7` | Yes |
| `30-Skills/teach-senior-web-development/references/lesson-contract.md` | Shared lesson, curriculum, hints, assessment, readiness, and evidence contract | `1CBBA45FAD5C70BCB7C2AF6E3DE656891D89B1ECF451099BDB190EE4FC0BE677` | Yes |
| `30-Skills/teach-web-foundations/SKILL.md` | Browser, language, protocol, toolchain, and COITB HTML/CSS routing | `AEE27E85D147205B811C707EF2FE52F6AC3ECAC847B0329040F27EA1888A7EB6` | Yes |
| `30-Skills/teach-frontend-engineering/SKILL.md` | Frontend product and architecture teaching route | `02F1EDAB6F6DF3A894F60220DED6BE5E903BED836ED30280C3337D310D9D3D09` | Yes |
| `30-Skills/teach-backend-api-engineering/SKILL.md` | Backend, API, integration, and resilience teaching route | `DF055C3334FA5CDA736DE3E563BFF3072E5F727E5E2A0AF9FD4B1408AC954402` | Yes |
| `30-Skills/teach-web-data-engineering/SKILL.md` | Data modeling, storage, change, lifecycle, and recovery teaching route | `7338F96716E9C1E8C83C686C9A89F935D76A26563AA1124F04AB6F082C59C9AE` | Yes |
| `30-Skills/teach-web-security/SKILL.md` | Defensive web-security teaching route and authorization boundary | `0541B4BD4556554EB71C6F9C116F6F081F73887E8426DBCC6739A53631A665FF` | Yes |
| `30-Skills/teach-web-quality-delivery/SKILL.md` | Testing, delivery, operation, incident, and handoff teaching route | `4A97647980290F7ADD8A389EA4A8B46105F423DEE4F3379E360BBD1E662CED83` | Yes |
| `30-Skills/teach-web-architecture-leadership/SKILL.md` | Requirements, architecture, economics, risk, and leadership teaching route | `EB5F02755F723B65774FCAF4CE460988075470696B120241B9DBD14BB6C55441` | Yes |
| `30-Skills/teach-coitb-html-css/SKILL.md` | COITB-specific diagnostic, teaching, assessment, readiness, integrity, and permission workflow | `0696EE9DD6898568D0D15B86AA20E74398480CA2E8B79C8029D10C2043ACECB8` | Yes |
| `30-Skills/teach-coitb-html-css/references/exam-blueprint.md` | Dated official exam domains, weights, logistics, discrepancy, readiness heuristic, and standards cross-check | `97BDD16FF48CF2D2729F043B389AE19D59EA4AC9195A7014A529477C71D2B312` | Yes |
| `30-Skills/teach-coitb-html-css/references/curriculum.md` | Project-based domain curriculum, capstone, practice-assessment rules, and rubric | `1940D8145F28E54AA03C736E8E7CC78299EC17FD9F15CF396EBE6DAE52E294AB` | Yes |

No hidden files, binaries, archives, scripts, assets, packages, lockfiles, install hooks, workflows, generated code, or nested executable content are included in the 12-file teaching family.

## Behavior, Dependencies, Network, and Permissions

- Entry point: the parent or a subject skill is loaded only when selected for a teaching request
- Automatic behavior: none; the Markdown cannot execute independently
- Dependencies: maintained Markdown skills already in this vault; no runtime package dependencies
- File and process permissions: none requested by the package; exercises inherit the exact task's scope and repository safety gates
- Network destinations: none built in; current research is routed to authoritative primary sources only when a changing fact matters
- Telemetry, analytics, tracking, persistence, dynamic downloads, encoded payloads, shell construction, credential access, or privilege escalation: none
- Data handling: lessons require dummy data by default and prohibit secrets or private production data in examples and artifacts
- Certification actions: the focused skill may advise on preparation but cannot register, purchase, schedule, manage identity, or interact with a proctored exam without explicit authorization at that step

## Findings and Mitigations

| Severity | Finding | Mitigation | Status |
|---|---|---|---|
| Medium | A broad teaching skill could load the whole vault or produce generic lessons | Seven explicit subject routes, one lead-module rule, and smallest-relevant-skill loading | Mitigated |
| Medium | Framework, browser, service, pricing, and security facts age quickly | Route to maintained evidence notes and require current primary-source verification for decision-changing claims | Mitigated |
| Medium | A tutor may solve the work instead of developing learner judgment | Prediction-first flow, progressive hints, independent variation, and explicit learner-ownership rule | Mitigated |
| High when invoked | Security labs, deployments, accounts, dependencies, credentials, or production data can exceed teaching scope | Isolated dummy-data defaults and preservation of R2 review and R3 immediate-authorization gates | Mitigated by gate |
| Medium | Toy examples can be mistaken for production guidance | Required readiness label and explicit missing-work statement | Mitigated |
| Medium | Exam objectives, weights, logistics, and badge terms can change | Dated official blueprint, re-verification triggers, and no claims beyond published evidence | Mitigated |
| High when invoked | Leaked questions or reconstructed live items could undermine exam integrity | Public-outline-only scope and original-practice-item requirement | Mitigated by gate |
| Medium | Official COITB pages currently describe the format differently | Preserve the discrepancy and prepare for both code-reading and applied scenarios instead of claiming certainty | Open, bounded by recheck |

## Test Evidence

- Format validation: the COITB skill and all teaching-family skill folders passed the bundled skill validator on 2026-10-22.
- Full-vault validation: all 121 observed skill folders passed in explicit UTF-8 mode, with 121 unique frontmatter names and no duplicates.
- Link validation before this review update: all relative Markdown links across 268 notes resolved.
- Inventory validation: only the 12 listed Markdown files exist in the teaching-family packages.
- Static routing review:
  - a client-state lesson routes through frontend engineering to frontend-state design;
  - an idempotent webhook lab routes through backend and API engineering to webhook integration and the required security boundary;
  - a system-design mentoring request routes through architecture and leadership to product discovery, architecture selection, cost, and resilience only as needed.
  - a COITB HTML/CSS request routes through the dated official blueprint, weighted domain curriculum, original practice rules, and practical capstone criteria.
- Side effects during testing: none; no dependency, tool, service, account, environment, or external system was installed, connected, or changed.

## Limitations

- The files are structurally valid, but no real learner session, COITB diagnostic, full mock, exam result comparison, capstone, grading exercise, or independent behavioral forward-test was performed.
- The family depends on the quality and freshness of routed vault skills; draft upstream guidance remains draft.
- The official COITB outline currently says multiple-choice while the official badge page says multiple-choice and scenario-based items; the actual current form was not observed.
- No visual inspection in Obsidian was performed, and this workspace is not a Git repository, so no Git diff or commit evidence is available.

## Activation, Rollback, and Removal

- Activation: the nine teaching entries are linked from the [Skills Map](../../30-Skills/Skills%20Map.md); no installation or application setting is required.
- Verification after activation: use the parent and focused module on representative teaching and COITB preparation requests; inspect routing, objective coverage, practice originality, learner ownership, and evidence quality.
- Disablement: remove the relevant Skills Map entries or stop selecting the skills.
- Rollback: restore the prior Skills Map, Source Registry, and Maintenance Log revisions, then archive or remove the nine teaching skill directories and this review note.
- Residue: none outside the listed Markdown files and vault integration notes.

## Approval Record

- Reviewer: Codex for vault-owner review
- Review date: 2026-10-22
- Approved scope: version 1.1.0 as inventoried above, for instructional planning and work within the task's existing authorization
- Re-review triggers: material file change, COITB objective or logistics change, new certification module, external curriculum import, executable resource, dependency or service integration, first realistic multi-session or mock-assessment use, repeated routing or teaching failure, exam-integrity issue, or any permission-boundary failure
