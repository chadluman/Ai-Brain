---
name: incident-response
description: Prepare for, coordinate, document, and learn from reliability or cybersecurity incidents affecting websites, applications, data, or delivery systems. Use for severity, roles, containment, service restoration, communications, evidence, handoffs, and postmortems; do not use as a substitute for legal, forensic, safety, or regulatory specialists.
---

# Incident Response

## Outcome

Create or run a calm, auditable response that protects people and data, limits impact, restores a verified safe service, preserves evidence, communicates clearly, and produces owned corrective work.

## Required Inputs

- observed impact, affected users and services, start time, and detection source
- data sensitivity, safety consequences, contractual or regulatory obligations, and reporting deadlines
- service owners, on-call contacts, decision authority, vendors, and communication channels
- current architecture, dependencies, runbooks, SLOs, recovery priorities, and known-safe rollback paths
- evidence sources, retention rules, and forensic or legal contacts

When safety, regulated data, active compromise, or reporting obligations may apply, engage the designated qualified responders immediately rather than improvising legal or forensic conclusions.

## Safety and Permission Constraints

- Prioritize human safety, containment of harm, service restoration, and evidence preservation over diagnosis elegance.
- Use least privilege, a recorded command structure, and a single source of incident state. Do not paste secrets, tokens, personal data, exploit payloads, or unnecessary evidence into general chat or the vault.
- Separate facts, hypotheses, decisions, actions, owners, and timestamps. Preserve original evidence and chain-of-custody requirements where applicable.
- Destructive containment, production changes, account suspension, key rotation, external notification, public statements, law-enforcement contact, or real-data recovery is R3 and requires the authorized incident lead or user approval except where an established emergency policy already grants it.
- Prefer reversible mitigations. State blast radius and rollback before consequential action when time permits.
- Do not blame individuals. Analyze system conditions and decision context while preserving accountability for corrective work.

## Workflow

1. Triage impact and declare a provisional severity. Open a timestamped incident record and name the current incident commander.
2. Assign explicit roles as scale requires: command, operations, communications, planning or scribe, security, privacy/legal, and vendor coordination. One person may hold several roles in a small incident.
3. Establish a dependable command channel and living state document independent of the failing system where practical.
4. Stabilize: stop harmful automation, reduce blast radius, preserve evidence, protect credentials and data, and choose the safest reversible mitigation.
5. Investigate with tracked hypotheses. Record what changed, what is known, what was tested, and why each action was approved. Avoid simultaneous uncoordinated production changes.
6. Communicate on a declared cadence. Give impact, scope, mitigation, uncertainty, next update time, and action needed; do not speculate. On a public status page, move through the states acknowledged, then identified, then resolved, updating at each transition rather than only at resolution.
7. Restore service in controlled stages. Verify security, data integrity, critical journeys, backlog or replay behavior, monitoring, and rollback readiness before declaring recovery.
8. Conduct an explicit handoff when command or operational ownership changes. The receiving owner acknowledges current state, risks, next actions, and authority.
9. Close only when exit criteria are met and residual risks have owners. Preserve the timeline, evidence references, decisions, and customer or regulatory records.
10. Write a timely blameless postmortem for significant incidents: impact, timeline, detection, contributing conditions, response quality, what went well, what failed, and prioritized corrective actions with owners and dates.
11. Test the improved response through a tabletop or controlled exercise and update the source runbook rather than layering contradictory notes.

## Runbooks, On-Call Burden, and Assisted Triage

- Every alert that can page must have a runbook: what the alert means, the first checks, the safe mitigations, and the escalation path. An alert without a runbook is an interruption, not a response.
- Track on-call burden as a metric alongside incident counts: pages per shift, pages outside working hours, and time to acknowledge. A rising burden is a reliability problem even when incidents are handled well, and it is a reason to fix noisy alerts, not to staff more on-call.
- Treat AI-assisted triage as an unproven aid, not a responder: vendor claims that automated triage shortens incidents are unproven until measured against your own incidents. Any triage aid must be evaluated on real incident data, with a human keeping command, before it is trusted in the response path.

## Required Output

- severity and impact statement with confidence and timestamps
- roles, command channel, update cadence, and handoff record
- fact/hypothesis/action timeline and evidence references
- containment, mitigation, rollback, and recovery verification
- stakeholder, customer, vendor, and regulatory communication decisions
- postmortem with owned corrective actions and review dates
- exercise evidence and remaining risks

## Completion Gate

Do not declare an incident resolved until the incident commander accepts the exit criteria, critical service and data checks pass, monitoring is stable for the defined observation period, and residual risk has named owners. Do not call corrective work complete until it is verified, not merely ticketed.

## Conditional Reference

Read [Incident Response Evidence](references/incident-response-evidence.md) when defining the program, command roles, lifecycle, communications, or postmortem practice.
