---
name: analytics-experimentation-design
description: Design privacy-conscious product analytics, funnels, outcomes, feature experiments, guardrails, event contracts, data quality, and decision rules. Use when teams need to measure product behavior or test a change without defaulting to broad tracking.
---

# Analytics and Experimentation Design

## Outcome

Create a minimal measurement system that answers explicit product decisions with trustworthy data while limiting surveillance, bias, accidental identifiers, vendor lock-in, and experiment harm.

Use [Management Dashboard Design](../management-dashboard-design/SKILL.md) when presenting validated outcomes and operational measures to recurring decision makers. This skill owns measurement purpose, event contracts, data quality, and experiment validity rather than dashboard composition.

## Required Inputs

- product outcomes, decisions, hypotheses, baselines, guardrails, and decision owners
- critical journeys, populations, accessibility, regions, devices, and support channels
- required events, properties, identity level, retention, latency, and accuracy
- consent, privacy, security, legal, child, employee, health, financial, or other sensitive constraints
- traffic, statistical expertise, tooling, budget, export, and operational capacity

## Safety and Permission Constraints

- Collect no event or property without a named decision purpose, owner, retention period, and approved sensitivity. Prefer aggregate and anonymous measurement when it answers the question.
- Never place secrets, message bodies, form contents, free text, full URLs with identifiers, or unexpected personal data into analytics. Validate and allow-list event properties.
- Consent and legal requirements vary by jurisdiction and technology. Obtain qualified review where required; a vendor setting is not legal assurance.
- Experiments must not knowingly withhold safety, accessibility, security, legal rights, required disclosures, or critical recovery. Predefine harm guardrails and stop rules.
- Enabling production tracking, joining data sets, exporting personal data, changing consent, or exposing users to an experiment is R3 and requires immediate authorization and rollback.

## Workflow

1. Start with a decision and falsifiable hypothesis: action, affected population, expected user outcome, time horizon, and what decision follows each result.
2. Define one primary outcome plus guardrails for harm, reliability, accessibility, support burden, privacy, cost, and important segments. Establish a baseline before change.
3. Choose the least identifying unit and shortest useful retention. Separate operational telemetry, product analytics, marketing attribution, research, and experimentation by purpose.
4. Specify a versioned event contract with stable names, trigger semantics, allowed properties, units, ownership, schema validation, and test fixtures. Document late, duplicate, missing, and reordered behavior.
5. Map collection, consent, client and server processing, vendor or warehouse transfer, access, aggregation, export, deletion, and backup. Apply minimization and least privilege at each stage.
6. Validate data quality with end-to-end tests, expected volumes, invariant checks, reconciliation to system-of-record outcomes, and monitoring for schema or consent drift.
7. For experiments, define eligibility, assignment unit, exposure event, interference risks, duration, power assumptions, analysis method, multiple-testing policy, and precommitted stop criteria.
8. Review novelty, seasonality, sample-ratio mismatch, repeated peeking, missing data, bots, returning users, cross-device identity, and segment harm before interpreting a result.
9. Report effect size, uncertainty, guardrails, exclusions, data quality, practical significance, and limitations. A non-significant result is not proof of equivalence.
10. Remove unused events, stale identifiers, expired experiments, and vendor access; preserve only the decision record and minimally necessary evidence.

## Required Output

- decision, hypothesis, outcomes, guardrails, baseline, and decision rules
- event taxonomy and versioned contracts
- data-flow, consent, minimization, retention, access, export, and deletion plan
- data-quality tests, reconciliation, and observability
- experiment design, assignment, exposure, analysis, stop, and rollback plan
- results report with uncertainty, limitations, segment review, and follow-up decision

## Completion Gate

Do not call analytics or an experiment trustworthy until event semantics and consent are verified end to end, the primary outcome and guardrails were defined before interpretation, data-quality failures are bounded, and the decision accounts for uncertainty and practical harm.

## Conditional Reference

Read [Analytics and Experimentation Evidence](references/analytics-experimentation-evidence.md) when selecting metrics, analytics tools, event data, privacy controls, or experiment decision rules.
