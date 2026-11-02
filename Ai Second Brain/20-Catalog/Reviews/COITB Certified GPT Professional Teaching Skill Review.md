---
status: reviewed
owner: vault-owner
created: 2026-10-25
last_verified: 2026-10-25
review_by: 2027-01-25
risk: R0
tags: [catalog, security-review, skill, teaching, certification, generative-ai]
sources:
  - https://www.coitb.org/certification-resources/badges/certified-gpt-professional
  - https://www.coitb.org/certification-resources/exam-outlines/certified-gpt-professional-outline
  - https://developers.openai.com/api/docs/guides/migrate-to-responses
  - https://developers.openai.com/api/reference/overview
  - https://developers.openai.com/api/docs/guides/error-codes
  - https://developers.openai.com/api/docs/guides/your-data
  - https://www.nist.gov/itl/ai-risk-management-framework
  - https://commission.europa.eu/law/law-topic/data-protection/information-business-and-organisations/principles-gdpr_en
  - https://studentprivacy.ed.gov/faq/what-ferpa
  - https://www.ftc.gov/business-guidance/resources/complying-coppa-frequently-asked-questions
---

# Security Review — COITB Certified GPT Professional Teaching Skill

## Identity and Scope

- Asset type: locally authored Markdown skill package
- Purpose: prepare learners for the public COITB Certified GPT Professional objectives through weighted diagnostics, project-based teaching, original practice assessments, and safe comparisons with current provider practice
- Source: this vault; no third-party skill, question bank, course, code sample, or executable package was imported
- Author or organization: vault owner and Codex
- Exact version: 1.0.0, local revision dated 2026-10-25; checksums are recorded below
- License: no repository license was identified; treat the original text as internal-use material until the owner assigns reuse terms
- Proposed use: automatically route requests specifically about this certification, its objectives, study planning, tutoring, practice, or readiness review

## Decision Summary

- Assigned risk: R0 for the Markdown assets themselves
- Decision: approved-with-conditions
- Conditions: keep the skill marked draft until realistic learner, capstone, and timed-mock validation; recheck COITB and provider facts before use; use only original practice items; keep the offline synthetic-data path as the default; preserve R2 review and R3 authorization gates for packages, accounts, credentials, paid calls, external integrations, real data, and exam transactions
- Decision owner: vault-owner
- Next review: 2027-01-25, or earlier after a re-review trigger below

Safety approval means the reviewed Markdown package may guide work. It does not validate teaching effectiveness, predict an exam result, approve external tools, or authorize a live API call.

## Complete Inventory

| Path | Purpose | SHA-256 | Reviewed? |
|---|---|---|---:|
| `30-Skills/teach-coitb-gpt-professional/SKILL.md` | Invocation boundary, modes, two-lane workflow, safety gates, and completion evidence | `A2E1D94EE646A26EA5B16DF187C6F42AABE9E71F11CBAF18F02B66FD1B5DC8C0` | Yes |
| `30-Skills/teach-coitb-gpt-professional/Teach COITB Certified GPT Professional.md` | Obsidian-facing alias and embed of the canonical entry point | `3D951644E22F7E9925A5E3E28C35AAFAC4C2E945DCCC402CAFCA54AE08A75D1E` | Yes |
| `30-Skills/teach-coitb-gpt-professional/references/exam-blueprint.md` | Dated official logistics, five domains, objectives, question forms, current-practice differences, sources, and readiness heuristic | `FB4305FA00798CEAA82D7B3816C43FA902C62F80B5CDFEDB8C3A94FB4DE0E83D` | Yes |
| `30-Skills/teach-coitb-gpt-professional/references/curriculum.md` | Adaptive project curriculum, labs, assessment rules, capstone, rubric, setup boundaries, and review cadence | `4A9D5730714FEDA200FF90961583520D383BD5495CAE5B2C84F2FEBDB65975E6` | Yes |

The package contains four Markdown files and one directory. It contains no hidden file, binary, archive, script, asset, manifest, lockfile, install hook, CI workflow, generated code, dependency, or nested executable content.

## Provenance and Source Handling

- COITB's official badge and exam-outline pages were read as the authority for the credential's public scope and logistics.
- Current OpenAI implementation claims were checked against official OpenAI documentation for models, prompt engineering, Responses migration, authentication, structured output, errors, moderation, data controls, and evaluation.
- Responsible-AI and privacy recognition used current NIST, European Commission, U.S. Department of Education, and FTC sources.
- All external material remained untrusted R0 reference input. The package summarizes concepts and links to sources; it does not copy a protected question bank, substantial documentation text, or third-party code.
- The public COITB sources expose objectives and weights but not live questions or an item-writing specification. Original practice design beyond those objectives is labeled as local teaching judgment.

## Behavior, Dependencies, Network, and Permissions

- Entry point: the skill is loaded only when selected for a COITB Certified GPT Professional teaching or preparation request.
- Automatic behavior: none; Markdown cannot execute independently.
- Internal dependencies: the shared teaching lesson contract, with optional routing to the vault's AI feature, evaluation, agent-safety, retrieval, and runtime skills only when the learner's request requires them.
- External dependencies: none. The offline core path uses conceptual examples and synthetic JSON fixtures; it does not require an SDK, model, account, API key, package manager, N8N, Flowise, Zapier, React, or Vite.
- File and process permissions: none requested by the package.
- Network destinations: none contacted automatically. Linked COITB, OpenAI, NIST, European Commission, Department of Education, and FTC pages are references for explicit re-verification.
- Telemetry, analytics, tracking, persistence, dynamic downloads, encoded payloads, shell construction, credential access, privilege escalation, or destructive commands: none.
- Data handling: synthetic data is the default. The skill prohibits secrets and real personal, student, child, customer, proprietary, or regulated data in exercises.

## Findings and Mitigations

| Severity | Finding | Mitigation | Status |
|---|---|---|---|
| Medium | The public COITB outline can change and does not publish live items | Dated blueprint, direct official links, re-verification triggers, and original-item-only rule | Mitigated |
| Medium | Official COITB pages disagree on whether the format is only multiple-choice or also scenario-based | Preserve the conflict and prepare for both without claiming an observed form | Open, bounded by recheck |
| Medium | The outline names older models, Chat Completions, and parameters whose current implementation differs | Separate exam and current-practice lanes and require current official documentation before coding | Mitigated |
| High when invoked | API keys, accounts, live calls, and external connectors can disclose data or incur cost | Offline default; no pasted keys; R2 review for dependencies; R3 authorization immediately before credentials, paid calls, or external changes | Mitigated by gate |
| High when invoked | A browser implementation can expose a provider secret | Explicit browser-to-owned-backend boundary and client-asset secret inspection | Mitigated |
| High when invoked | Real prompts can contain personal, student, child, customer, or proprietary data | Synthetic fixtures, minimization, current data-control review, and qualified legal escalation | Mitigated by gate |
| Medium | “Chain-of-thought” exam wording can encourage demands for hidden reasoning | Teach the term for recognition while preferring concise rationales and verifiable intermediate artifacts | Mitigated |
| Medium | Practice scores can be mistaken for a pass guarantee | Local readiness label, domain floors, repeated evidence, capstone evidence, and explicit uncertainty | Mitigated |
| Medium | Legal acronyms can be taught as universal compliance conclusions | Teach issue recognition and escalation; require current qualified review for applicability or compliance | Mitigated |
| Medium | Toy code can be mistaken for production readiness | Offline fixture-first curriculum, practice-implementation label, and routing to production AI skills for broader controls | Mitigated |

## Test Evidence

- The bundled skill validator passed the package in explicit UTF-8 mode on 2026-10-25.
- Frontmatter uses the required lowercase hyphenated name and a discriminating description.
- Static coverage review found all five published domains, every public objective cluster, official weights totaling 100%, a derived 6/12/24/9/9 mock distribution clearly labeled as local, and a capstone that exercises the high-weight integration domain.
- Static safety review found explicit boundaries for exam integrity, credentials, client-side keys, dependencies, paid calls, external services, sensitive data, model output, legal scenarios, and consequential actions.
- Package inventory and SHA-256 hashes were generated after content creation; no executable or hidden asset was present.
- Side effects during testing: local Markdown writes only. No package, SDK, model, account, credential, API call, automation platform, external integration, payment, exam registration, identity submission, or real data was used.

## Limitations

- No real learner diagnostic, tutoring session, capstone, 60-item timed mock, official practice assessment, exam attempt, or exam-result comparison was performed. The skill remains a structurally reviewed draft.
- No independent behavioral forward-test was performed because delegation was not authorized for this task.
- The public COITB sources do not prove the exact distribution, wording, difficulty, or scenario style of any future form.
- The local readiness heuristic is deliberately more conservative than the published passing score and is not validated as a score predictor.
- Current OpenAI guidance is provider-specific and volatile. No live implementation or SDK version was selected or tested.
- The files were not visually inspected in Obsidian, and this workspace is not a Git repository, so no Git diff or commit evidence is available.

## Activation, Rollback, and Removal

- Activation: the skill is linked from the [Skills Map](../../30-Skills/Skills%20Map.md) and [Research Queue](../../00-System/Research%20Queue.md); no installation or application setting is required.
- Verification after activation: use it for a representative diagnostic, lesson, project review, and timed mock; inspect objective coverage, practice originality, learner ownership, secret safety, exam/current separation, and scoring evidence.
- Disablement: remove its Skills Map and Research Queue entries or stop selecting it.
- Rollback: restore the prior Skills Map, Research Queue, Source Registry, and Maintenance Log revisions, then archive or remove the skill folder and this review note.
- Residue: none outside the listed Markdown files and vault integration notes.

## Approval Record

- Reviewer: Codex for vault-owner review
- Review date: 2026-10-25
- Approved scope: version 1.0.0 as inventoried above, for R0 instructional planning and offline synthetic-data teaching within the task's authorization
- Re-review triggers: material file change; first representative learner or timed mock; COITB objective, logistics, or policy change; OpenAI endpoint, SDK, model, parameter, authentication, data, moderation, error, or lifecycle change; new course, question bank, practice platform, dependency, executable, connector, account, credential, paid call, sensitive data, or external service; exam-integrity concern; credential exposure; or any permission-boundary failure
