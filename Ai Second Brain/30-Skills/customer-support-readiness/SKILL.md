---
name: customer-support-readiness
description: Design and review user support, assisted journeys, ticket intake, identity verification, escalation, knowledge, staffing, privacy, feedback, and launch readiness. Use when a product will have users who may be blocked, harmed, billed, locked out, or unable to complete a digital journey independently.
---

# Customer Support Readiness

## Outcome

Create a support system that helps users complete or recover critical journeys safely, protects private data and privileged actions, matches expected demand, and turns recurring contacts into product improvements.

## Required Inputs

- users, critical journeys, accessibility and assisted-support needs, languages, and regions
- expected contact reasons, channels, volume, peaks, severity, and response objectives
- account, identity, payment, abuse, privacy, legal, accessibility, and incident escalations
- support roles, hours, staffing, training, tools, permissions, and third-party providers
- data captured, retention, recording, export, audit, and deletion requirements

## Safety and Permission Constraints

- Support authority is a privileged attack surface. Define what agents may view or change, require strong identity verification proportionate to harm, and prevent password, MFA, or secret disclosure.
- Minimize ticket content and recordings. Redact secrets and payment data; restrict access, export, integrations, analytics, AI summarization, and retention.
- Do not let support bypass authorization, ledger controls, legal holds, consent, account-recovery policy, or incident command through an undocumented workaround.
- Contacting real users, enabling recording, connecting support SaaS, granting agent access, issuing credits or refunds, or changing production accounts is R3 and requires authorization.
- Provide accessible and appropriate non-digital or assisted paths when research shows users cannot complete the journey alone.

## Workflow

1. Map where users can fail, become uncertain, lose access, suffer harm, or need human judgment across the complete journey.
2. Define channels, availability, languages, accessibility, expected demand, peak scenarios, severity, first response, resolution, and handoff objectives.
3. Create a minimal taxonomy and required fields. Keep free text optional and constrained; never request secrets or unnecessary identity documents.
4. Define verification and authority for each action, including account recovery, data requests, payments, abuse, safety, security, and legal escalation.
5. Build accessible self-service guidance for common safe tasks while preserving human help for exceptions, assisted needs, and consequential decisions.
6. Give agents versioned procedures, approved responses, known-issue status, escalation owners, incident linkage, and a safe way to stop uncertain actions.
7. Forecast staffing and tool capacity, protect worker wellbeing, separate production privileges, and test provider outage plus manual continuity.
8. Measure contact reasons, wait, abandonment, first-contact resolution, repeat contact, user outcome, escalation quality, accessibility, and privacy incidents without rewarding unsafe speed.
9. Feed recurring contacts to product, content, engineering, and operations owners. Treat avoidable contacts as evidence of a journey fault.
10. Run launch and incident exercises covering lockout, billing dispute, privacy request, vulnerable user, suspected takeover, outage, abuse, and inaccessible journey.

## Required Output

- contact and assisted-journey map
- channel, staffing, hours, demand, severity, and service objectives
- taxonomy, data minimization, retention, access, and recording policy
- identity-verification and action-authority matrix
- knowledge, escalation, incident, accessibility, and continuity procedures
- launch exercise evidence, metrics, feedback loop, and improvement owners

## Completion Gate

Do not call support ready until users can find accessible help, agents can safely resolve or escalate critical scenarios, privileged actions are bounded and audited, demand has an owner and capacity plan, and recurring contacts reach product decision makers.

## Conditional Reference

Read [Support Readiness Evidence](references/support-readiness-evidence.md) when estimating demand, designing assisted channels, or treating contacts as product evidence.
