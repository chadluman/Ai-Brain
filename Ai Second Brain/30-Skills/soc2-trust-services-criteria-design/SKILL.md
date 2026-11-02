---
name: soc2-trust-services-criteria-design
description: Design a SOC 2 scope from the AICPA Trust Services Criteria: Security as the mandatory category, Availability, Processing Integrity, Confidentiality, and Privacy as optional categories elected only when they match real service commitments, Type I versus Type II, and the misconceptions that most often mislead a small team. Use when scoping any SOC 2 effort, answering a customer security questionnaire, or writing a system description; do not use as a substitute for an auditor's reading of the criteria, and never use it to claim a report, certification, or compliance status the organisation does not hold.
---

# SOC 2 Trust Services Criteria Design

## Outcome

Design a SOC 2 scope that is honest, testable, and no larger than the organisation can evidence: the right categories elected, the right criteria in scope, and language in marketing, terms, and questionnaires that matches the report that actually exists — or the absence of one.

## The facts that anchor this skill

- **SOC 2 is an attestation, not a certification.** The AICPA publishes the Trust Services Criteria (TSP Section 100; 2017 criteria with revised Points of Focus in 2022). A licensed CPA firm, not the AICPA, performs the examination under AICPA attestation standards and issues the report. The AICPA does not audit individual companies, approve individual reports, or maintain a registry of "SOC 2 compliant" companies. ISO 27001 issues a certificate through a certification body; SOC 2 issues a report with an opinion (unqualified, qualified, or adverse). An adverse or qualified report is still a report, and customers read its exceptions.
- **Security (Common Criteria CC1–CC9) is mandatory in every SOC 2 report.** Availability (A1), Processing Integrity (PI1), Confidentiality (C1), and Privacy (P1–P8) are optional, added only when they match service commitments or customer contracts.
- **Type I** opines that controls are suitably designed and implemented as of a specific date. **Type II** opines that controls were suitably designed and operated effectively over a period, by sampling evidence from that period. Enterprise buyers overwhelmingly want Type II; Type I is a bridge, not a destination.
- **There is no pass mark.** There is an opinion plus a list of exceptions. A single exception does not automatically qualify a criterion; a criterion is qualified only if effectively all its controls fail — do not over-read or under-read a single exception.
- **The full AICPA criteria text is a paid publication.** Free summaries paraphrase it. The engaged auditor's reading of TSP Section 100 governs, and criterion wording in this skill must be re-verified against that reading at engagement time.

## The Common Criteria, in brief

- **CC1 Control environment** — integrity, accountability, structure, and responsibilities, stated explicitly even when one person wears all hats.
- **CC2 Communication and information** — the information needed to operate controls is identified, captured, and communicated.
- **CC3 Risk assessment** — risks to meeting service commitments are identified, analysed, owned, and reassessed at least annually and on significant change.
- **CC4 Monitoring activities** — controls are monitored, and findings are tracked to closure.
- **CC5 Control activities** — control activities are selected, developed, and operated, including through technology.
- **CC6 Logical and physical access** — access is restricted to authorised parties, with logical access, authentication, and authorisation controls. CC6 and CC7 generate the most exceptions in practice.
- **CC7 System operations** — operations are monitored, incidents are managed, and changes to operations are controlled.
- **CC8 Change management** — changes to systems are authorised, tested as appropriate, and deployed through a controlled process.
- **CC9 Risk mitigation** — risks are mitigated, including business continuity (CC9.1) and vendor and subservice management (CC9.2).

## Design

1. **Elect categories by commitment, not by ambition.** For each optional category, ask: do our terms, data-processing agreement, or marketing actually commit to this? Security is non-negotiable. Availability is strongly indicated for a livestream tool whose core commitment is working during a live show. Confidentiality is indicated when streamer OAuth tokens, stream keys, or unpublished show configurations are confidential, not merely personal data. Processing Integrity is indicated only if billing or control-action accuracy is claimed (for example, Stripe amounts or scene and overlay state changes). Privacy only if personal-information lifecycle promises beyond generic privacy handling are committed to.
2. **Adding a category adds evidence burden.** Every in-scope criterion is tested. Electing a category that cannot be evidenced is worse than omitting it. Conversely, omitting Availability while promising "99.9% uptime" in marketing or contracts creates a commitment gap the auditor will probe. Reconcile marketing, terms, and the data-processing agreement to the elected scope before the observation period starts, and freeze scope at that point.
3. **Record non-applicable criteria with reasons.** The system description must state which criteria are in scope, which are not applicable, and why (description criteria DC8 in the research run's account). "Not applicable because we do not process that data type" is a reason; "not applicable because it is hard" is not.
4. **Choose Type I or Type II deliberately.** Type I says nothing about operation after its date and ages immediately. Type II requires controls running before the observation window starts, because evidence cannot be backdated. The "3-month minimum" observation period is widely repeated industry guidance that was not verified against published AICPA rule text in the 2026-11-02 research run — confirm the minimum, and the period target buyers require (3, 6, or 12 months), with the engaged CPA firm before committing.
5. **Write the scope so a questionnaire can be answered from it.** The scope election, report type, period, and opinion are the answers to the questions enterprise buyers actually ask. If the organisation holds no report, the honest answer is "no report yet; here is our control matrix and our roadmap", not a borrowed vendor badge.

## Guardrails

- Do not write "SOC 2 certified", "fully compliant", or "guaranteed secure" on a site or in a questionnaire. Write "SOC 2 Type II report issued by [CPA firm], period [dates], criteria [Security (+ …)]" and share the report under NDA — or, if no report exists, say so.
- Do not write "my vendors are SOC 2, so I am SOC 2". Vendor reports cover the vendor's systems, and only if their complementary user entity controls are implemented. See the vendor and subservice review skill.
- Do not conflate SOC 2 with GDPR, HIPAA, or PCI. Controls overlap; scopes and legal bases differ.
- Do not treat a compliance platform's "audit-ready" dashboard as an audit. Only a licensed CPA firm can issue a SOC 2 report; platforms, consultants, and readiness firms prepare an organisation for one.
- Do not let a policy, a tool, or a badge substitute for a control. MFA enabled but not enforced, a policy nobody follows, and a review done the week before the audit are findings, not controls.
- SOC 2 is voluntary in law and market-required in enterprise procurement. Do not claim it is legally required, and do not dismiss it as optional when the buyers who matter require it.

## Verification

A scope design is ready when: the elected categories trace to specific commitments in terms, the data-processing agreement, or marketing; every in-scope criterion has a named control and evidence source in the control matrix; every out-of-scope criterion has a written reason; the Type I versus Type II choice and observation period are confirmed with an auditor (or explicitly marked unconfirmed); and no public or questionnaire language claims a report, certification, or vendor inheritance that does not exist.
