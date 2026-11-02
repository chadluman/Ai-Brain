---
name: soc2-control-matrix-and-system-description-design
description: Build the two artefacts a SOC 2 audit starts from: a criterion-by-criterion control matrix (Trust Services Criteria → control → owner → evidence source) and a truthful system description covering services, boundaries, components, commitments, subservice organisations and their method, complementary controls, and non-applicable criteria. Use when starting any SOC 2 effort or preparing for an auditor; do not use to write a marketing description of the system, and do not start an observation period before the matrix and description are stable.
---

# SOC 2 Control Matrix and System Description Design

## Outcome

Produce a control matrix and a system description that an auditor can sample from and a customer can trust: every in-scope criterion mapped to a control that actually operates, an owner, and an evidence source — and a system description that describes the system as it is, not as it is wished to be.

## Supporting Skills

Load only what the gap requires:

- [SOC 2 Trust Services Criteria Design](../soc2-trust-services-criteria-design/SKILL.md) for category election and Type I versus Type II.
- [SOC 2 Evidence Operations Design](../soc2-evidence-operations-design/SKILL.md) for the evidence cadence the matrix must feed.
- [SOC 2 Vendor and Subservice Review Design](../soc2-vendor-and-subservice-review-design/SKILL.md) for carve-out, complementary controls, and vendor review records.
- [Privacy and Data Governance](../privacy-data-governance/SKILL.md) for data-flow mapping that feeds the description.
- [Authorization and Tenancy Design](../authorization-tenancy-design/SKILL.md) for the tenancy controls the description must state accurately.

## Design

1. **Start with the boundary, not the controls.** Define the service in scope: the production service only, or production plus marketing site, plus desktop app? Decide and document it. List the system components: infrastructure, software, people, procedures, and data. A boundary that is not written down will drift, and drift during an observation period expands the audit.
2. **Build the matrix criterion by criterion.** For every in-scope criterion and sub-criterion (for example CC6.1, CC7.2, CC8.1, CC9.2), record: the control, the owner (named, even if one person owns many controls — state that explicitly), and the evidence source (where the auditor will find proof, and over what period). A criterion with no control is a gap; a control with no evidence source is a hope.
3. **Write the system description to the description criteria (DC1–DC9 in the research run's account).** Cover: services provided; system boundaries; components; principal service commitments (from terms, data-processing agreement, and marketing, reconciled — do not let marketing over-promise); subservice organisations and the method chosen for each (carve-out or inclusive, with reasons); complementary user entity controls and complementary subservice organisation controls relied upon; incidents arising from control failures, if any; non-applicable criteria and why; and significant changes during the period.
4. **Choose carve-out as the default for hosted vendors.** Carve-out means the subservice organisation's controls are excluded from the report, the report references their SOC 2, and the schedules list the controls relied upon. Inclusive means their controls are included and tested by the auditor, which requires their assertion, representation letter, and auditor access. For vendors such as Vercel, Neon, Clerk, and Stripe, inclusive is effectively unavailable — they publish their own reports and will not submit to a customer's auditor testing — and attempting it wastes months. Carve-out does not remove vendor monitoring from the organisation: it still owns the vendor review (see the vendor skill).
5. **Reconcile commitments before the clock starts.** Read marketing, terms, and the data-processing agreement against the matrix. An uptime promise without an Availability control, a privacy promise without a Privacy control, or a security promise without the corresponding control is a commitment gap the auditor will probe. Fix the promise or build the control, before the observation period.
6. **Freeze scope at the observation start, and log changes after it.** Adding a feature, an integration, or an uptime promise mid-period without controls expands the audit. Scope changes during the period are logged as significant changes in the description, not silently absorbed.

## Guardrails

- Do not write the system description like marketing copy. A description written like marketing can qualify the opinion for reasons unrelated to security.
- Do not copy a template matrix verbatim. A matrix whose controls do not match the actual system will be sampled and found false, criterion by criterion.
- Do not start the observation clock on an unstable matrix. Controls implemented during the observation period only evidence the post-implementation part, and a control that starts mid-period may be sampled as not operating for the full period. Start the cadence, then start the clock.
- Do not hide a subservice without a SOC 2 report. Carve-out leaves a gap that must be filled with other evidence (questionnaire, penetration test, contractual controls) — flag it, do not hide it.
- If a subservice has no SOC 2 report at all, do not claim inheritance from it in any form.

## Verification

A matrix and description are ready when: every in-scope criterion has a control, an owner, and an evidence source; every out-of-scope criterion has a written reason; the boundary, commitments, subservice method, and complementary controls are stated and mutually consistent; marketing, terms, and the data-processing agreement match the description; and an independent reader can trace any criterion from the matrix to evidence without asking the author what was meant.
