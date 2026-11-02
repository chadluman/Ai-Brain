---
name: application-threat-modeling
description: Build or update an application threat model from system boundaries, assets, actors, data flows, business invariants, misuse, and operational context. Use during discovery, architecture, material feature or integration changes, and incident-driven redesign.
---

# Application Threat Modeling

## Outcome

Produce a maintained, testable view of what can go wrong in the specific system, which risks will be eliminated, mitigated, transferred, or accepted, and who owns the remaining work and residual risk.

## Required Inputs

- scope, critical journeys, architecture, environments, clients, services, stores, and dependencies
- assets, sensitive data, secrets, identities, roles, tenants, privileges, and business invariants
- actors, administrators, insiders, partners, automated agents, threat capabilities, and abuse incentives
- data flows, trust boundaries, entry points, external effects, availability, safety, and recovery needs
- existing controls, incidents, assumptions, constraints, risk owner, and review triggers

## Safety and Permission Constraints

- Model the real system and intended change, not an abstract checklist. Label unknowns and assumptions; do not claim exhaustive coverage.
- Protect diagrams and findings that expose sensitive architecture, credentials, exploit paths, private data, or defensive gaps. Store by need to know.
- Do not perform intrusive scanning, exploitation, account access, social engineering, or production tests without explicit authorization and bounded rules of engagement.
- Risk transfer does not remove technical harm. Record who operates the controls and who accepts residual consequences.
- Accepting high-impact risk, disclosing a vulnerability externally, or testing a production exploit path is R3 and requires immediate authorization and qualified coordination.

## Workflow

1. State scope, version, environment, owner, assumptions, and review trigger. Include the whole critical journey and operator paths, not only application code.
2. Draw the smallest useful model showing actors, processes, data stores, external services, data flows, trust boundaries, administrative planes, and deployment boundaries.
3. Inventory valuable assets and invariants: who may do what, which states and transitions are valid, what must remain secret or available, and what must be auditable or recoverable.
4. Identify threats using fit-for-purpose prompts. Apply technical categories to components and flows, business-logic misuse to journeys, and privacy or safety analysis when those harms are in scope.
5. Explore valid actions out of order, repeatedly, concurrently, at scale, across identities or tenants, with stale state, partial failure, malicious content, or compromised dependencies.
6. Rank with consequence, exposure, attacker effort, detectability, affected population, recovery, existing controls, and uncertainty. Avoid false precision from unsupported numeric scores.
7. Choose eliminate, mitigate, transfer, or accept for every material threat. Turn mitigations into owned requirements and observable negative tests.
8. Review with engineering, product, operations, support, privacy, and domain experts appropriate to the harm. Have an independent reviewer challenge boundaries and assumptions for high-risk systems.
9. Verify implemented controls, monitoring, incident response, and recovery. Update the model when architecture, data, privilege, dependency, threat, or incident evidence changes.

## Required Output

- scoped, versioned system and trust-boundary model
- asset, actor, entry-point, dependency, and invariant inventory
- threat and misuse register with evidence, consequence, uncertainty, and priority
- response, control, test, monitor, owner, due date, and residual-risk record
- validation results, accepted risks, unresolved questions, and review triggers

## Completion Gate

Do not call the model complete until every material threat has an accountable response, high-impact assumptions have evidence or escalation, mitigations map to tests or monitoring, and reviewers agree the system diagram reflects deployed reality.

## Conditional Reference

Read [Threat Modeling Evidence](references/threat-modeling-evidence.md) when choosing analysis prompts, modeling misuse, or defining review quality.
