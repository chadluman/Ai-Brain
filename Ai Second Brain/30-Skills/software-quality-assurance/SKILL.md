---
name: software-quality-assurance
description: Plan or assess the preventive software quality system for a project, including quality objectives, measurable requirements, responsibilities, lifecycle controls, audits, and improvement. Use when a team needs confidence in how quality will be produced; use release-quality-evaluation to judge one release candidate.
---

# Software Quality Assurance

## Outcome

Produce a proportionate quality-assurance plan that connects stakeholder needs and unacceptable failures to measurable quality requirements, owned delivery controls, trustworthy evidence, and improvement. Do not create ceremony that does not change a decision or reduce a material risk.

Read [Quality Assurance Evidence](references/quality-assurance-evidence.md) when selecting a quality model, measurement approach, audit method, or standards claim.

## Required Inputs

- product stage, users, critical journeys, contexts of use, and expected lifespan
- stakeholder, contractual, regulatory, accessibility, privacy, security, safety, and operational needs
- architecture, suppliers, delivery lifecycle, release cadence, team responsibilities, and maintenance capacity
- unacceptable outcomes, risk tolerance, incident history, support evidence, and known quality gaps

If these are incomplete, state the assumptions that materially affect the plan and identify who must confirm them.

## Boundaries and Safety

- Quality assurance is preventive and process-oriented; it does not prove that a particular build meets its requirements. Route candidate assessment to [Release Quality Evaluation](../release-quality-evaluation/SKILL.md).
- Testing and code review are controls within assurance, not the whole assurance system. Use [Test Strategy Design](../test-strategy-design/SKILL.md) and [Software Quality Review](../software-quality-review/SKILL.md) for their focused work.
- Apply domain-specific skills for security, accessibility, performance, privacy, AI, payments, mobile, recovery, or regulated requirements. A generic quality plan cannot replace specialist or qualified review.
- Do not claim ISO conformity, certification, legal compliance, safety, or absence of defects from a plan or audit. Certification and external assurance require separately authorized, competent parties and the complete applicable criteria.
- Keep production access, user data, credentials, active scanning, load or fault injection, deployment, and external audit activity behind their existing R2 or R3 review and authorization boundaries.

## Workflow

1. Define the quality scope: target product or service, lifecycle stage, supported contexts, stakeholders, critical journeys, exclusions, suppliers, and decision horizon.
2. Identify quality needs and unacceptable outcomes. Use a current quality model as a completeness prompt, then keep only characteristics that affect the product's value or risk.
3. Turn each material need into a quality requirement with an observable property, method, conditions, threshold or decision rule, tolerance, evidence source, owner, and review trigger. Separate product quality from quality in use and delivery-process performance.
4. Map each requirement and high-impact risk to the smallest effective prevention, detection, recovery, and learning controls across discovery, design, implementation, review, testing, release, operation, support, and retirement.
5. Assign accountable decision owners and proportionate independence. People may verify their own low-risk work; require a fresh or independent view when consequence, conflict of interest, contractual duty, or regulation warrants it.
6. Define evidence integrity: exact product and environment identity, traceability, configuration control, data provenance, retained artifacts, access, retention, and how missing or contradictory evidence is handled.
7. Select a small set of measures tied to decisions. For each measure, state its purpose, calculation, source, cadence, segmentation, target, uncertainty, gaming risk, owner, and action threshold. Balance leading signals with user-visible outcomes and escaped defects.
8. Define assurance reviews or audits by objective, criteria, scope, competence, independence, sampling, evidence, reporting, follow-up, and re-review trigger. Treat an audit as evidence about the sampled criteria, not a blanket quality verdict.
9. Define nonconformity and improvement handling: containment, severity, cause analysis proportional to impact, corrective action, effectiveness check, recurrence monitoring, and update of requirements or controls.
10. Revisit the plan when product scope, users, architecture, suppliers, quality objectives, risks, incidents, regulations, or release model change.

## Required Output

- quality scope, contexts of use, assumptions, and exclusions
- stakeholder needs, quality objectives, and measurable quality requirements
- requirement-to-risk-to-control-to-evidence traceability
- responsibilities, competence, independence, and escalation boundaries
- lifecycle assurance activities, review cadence, and audit criteria
- measure definitions, decision thresholds, and anti-gaming safeguards
- nonconformity, corrective-action, exception, and improvement process
- unresolved gaps, residual risks, evidence dates, and re-review triggers

## Completion Gate

Do not call the plan complete until every material quality objective and unacceptable outcome has an owner, observable acceptance rule, evidence route, and response to failure. Mark unavailable evidence and unfunded controls explicitly; never convert them into an implied pass.
