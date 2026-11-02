---
name: release-quality-evaluation
description: Evaluate an exact software release candidate against quality requirements, risk, test evidence, known defects, and operational readiness, then produce a ready, conditional, not-ready, or insufficient-evidence recommendation. Use for release quality control or go/no-go preparation; it does not authorize deployment.
---

# Release Quality Evaluation

## Outcome

Produce a reproducible quality-control decision for one identified candidate and target environment. The result must show what the evidence establishes, what remains unknown, which defects or exceptions remain, and why the recommendation follows.

Read [Release Quality Evidence](references/release-quality-evidence.md) when defining evaluation criteria, evidence traceability, testing independence, defect handling, or the decision record.

## Required Inputs

- exact source revision, build or artifact identity, configuration, data or schema version, and target environment
- release scope, change inventory, supported users and platforms, critical journeys, and rollback unit
- approved acceptance and quality requirements, risk assessment, release gates, and exception authority
- tests and reviews actually run, environments and data used, results, artifacts, known defects, incidents, and unresolved findings
- deployment, observation, rollback or roll-forward, support, privacy, security, and operational readiness evidence

If the candidate, criteria, or evidence identity is ambiguous, return `insufficient evidence` until the ambiguity is resolved.

## Boundaries and Safety

- This skill evaluates evidence and recommends a disposition; it does not authorize production deployment, publication, real-data migration, paid resources, destructive cleanup, or acceptance of residual R3 risk.
- Use synthetic or explicitly approved data. Do not run active security testing, load or fault injection, production checks, credentialed tests, or external-system mutations without their required authorization and safeguards.
- Route test-portfolio gaps to [Test Strategy Design](../test-strategy-design/SKILL.md), code findings to [Software Quality Review](../software-quality-review/SKILL.md), and process weaknesses to [Software Quality Assurance](../software-quality-assurance/SKILL.md).
- Use specialist evidence for accessibility, security, privacy, performance, resilience, recovery, mobile, AI, payments, or regulated behavior. A single aggregate score cannot substitute for a failed critical gate.

## Workflow

1. Freeze the evaluation object. Record the candidate, environment, dependencies, configuration, data or schema state, feature flags, build provenance, evaluation time, and differences from the intended release target.
2. Confirm the decision basis. List applicable requirements, acceptance criteria, risk tolerances, release gates, stop conditions, approvers, and authorized exception paths. Flag criteria invented after results were known.
3. Build traceability from each critical requirement and high-impact risk to the evidence, result, environment, artifact, owner, and date. Mark each item `pass`, `fail`, `pending`, `blocked`, or `not applicable` with rationale.
4. Qualify the evidence. Check version and environment match, data representativeness, test oracle, assertion relevance, sampling, independence, reproducibility, flake and retry history, artifact integrity, recency, and whether a representative break was shown to make the test fail.
5. Evaluate the relevant quality characteristics and end-to-end journeys. Combine static reviews, automated and manual tests, exploratory evidence, operational exercises, user or expert evaluation, and production-equivalent measurements according to risk.
6. Triage every known defect and contradiction by affected requirement, user impact, severity, reach, likelihood, detectability, recurrence, workaround, security or privacy effect, recoverability, and regression status. Keep priority and business scheduling separate from technical severity.
7. Evaluate exceptions explicitly. Record rationale, decision owner, affected users, compensating controls, time limit, monitoring, support plan, remediation owner and date, rollback or kill-switch path, and conditions that revoke the exception.
8. Choose one recommendation:
   - `ready`: required gates pass and residual risk is within the documented tolerance;
   - `conditional`: required evidence supports limited release under named constraints and monitored exceptions;
   - `not ready`: a release-blocking requirement fails or residual risk exceeds tolerance;
   - `insufficient evidence`: identity, criteria, or critical evidence is missing, stale, contradictory, or untrustworthy.
9. Define the post-release observation window, signals, support ownership, abort thresholds, rollback or containment action, and evidence needed before widening exposure.
10. Preserve the decision record and link it to the exact release. A later build, configuration, data migration, platform change, or material exception requires impact analysis and partial or full re-evaluation.

## Required Output

- exact candidate, target, scope, changes, evaluator, and evidence timestamp
- requirement-and-risk traceability matrix with explicit gaps
- evidence-quality assessment and tests or reviews actually performed
- known-defect, contradiction, exception, and residual-risk register
- `ready`, `conditional`, `not ready`, or `insufficient evidence` recommendation with rationale
- required remediation, owners, expiry dates, re-test scope, and re-evaluation triggers
- observation, containment, rollback, support, and escalation conditions
- separate authorization boundary for deployment and accepted high-impact risk

## Completion Gate

Do not issue `ready` or `conditional` when a critical requirement lacks trustworthy evidence, a release blocker remains unresolved, or the rollback and observation plan is not credible for the release risk. Never describe an unrun check as passed or turn unknowns into an aggregate quality score.
