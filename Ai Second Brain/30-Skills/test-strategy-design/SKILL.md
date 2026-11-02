---
name: test-strategy-design
description: Design or review a risk-based software test strategy spanning specifications, unit, integration, contract, browser, end-to-end, accessibility, security, performance, resilience, migration, and release evidence. Use when deciding what to test, at which boundary, with which data and environments; do not equate coverage or a passing suite with product correctness.
---

# Test Strategy Design

## Outcome

Produce a maintainable test portfolio that gives fast evidence about important invariants and critical user journeys while reserving expensive end-to-end tests for risks that smaller tests cannot cover.

Use [Software Quality Assurance](../software-quality-assurance/SKILL.md) for the wider preventive quality system and [Release Quality Evaluation](../release-quality-evaluation/SKILL.md) to turn completed evidence into a candidate-specific quality-control recommendation.

## Required Inputs

- product scope, critical journeys, requirements, invariants, and unacceptable failures
- architecture boundaries, external services, browsers, devices, data, and deployment environments
- security, privacy, accessibility, performance, recovery, migration, and compliance risks
- release cadence, team ownership, incident history, and acceptable feedback time

## Safety and Permission Constraints

- Use synthetic, minimized, or explicitly approved test data. Never copy production secrets or personal data into fixtures, recordings, snapshots, or reports.
- Keep tests isolated from production systems unless a separately authorized, non-destructive production check is designed for that purpose.
- Treat test tools, browser binaries, plugins, containers, fixtures, and generated code as executable assets requiring review.
- Security testing that can affect external systems, load testing, fault injection, destructive migration testing, or real-user experiments are R3 and require immediate authorization and safeguards.
- A scanner, coverage number, snapshot, or passing end-to-end test is evidence for a bounded claim, never a general safety guarantee.

## Workflow

1. Map requirements and failure consequences to observable acceptance criteria. Include denied, degraded, and recovery behavior, not only happy paths.
2. Build a risk matrix from likelihood, impact, detectability, change frequency, and history. Spend the strongest evidence on the highest residual risk.
3. Place each test at the narrowest reliable boundary:
   - specification and static checks for contracts and invalid states;
   - unit or property tests for deterministic logic and invariants;
   - integration and contract tests for real boundary behavior;
   - browser or device tests for rendering and platform behavior;
   - a small end-to-end set for critical user journeys and system assumptions.
4. Add dedicated accessibility, authorization, security, performance, concurrency, retry, migration, backup/restore, and resilience tests where the risk requires them.
5. Make tests independent and deterministic: control time and randomness, isolate state, avoid arbitrary sleeps, bound external dependencies, and capture diagnostic evidence.
6. Define realistic factories and fixtures with explicit lifecycle and cleanup. Test schema and client compatibility across supported versions.
7. Separate fast pull-request gates from slower scheduled, pre-release, and controlled environment suites. State failure ownership and release-blocking policy.
8. Track duration, flake rate, retry masking, false signals, defect escapes, and maintenance cost. Quarantine only with an owner and deadline; do not normalize flaky red builds.
9. Test the test: deliberately break representative behavior and confirm the expected test fails for the right reason.
10. Record exact versions, environment, seed, data, result, artifacts, and untested risks in release evidence.

## Required Output

- risk-to-test traceability matrix
- test layers, boundaries, environments, and ownership
- critical-journey and negative-case inventory
- data, isolation, determinism, and cleanup policy
- CI and release gates with expected evidence
- accessibility, security, performance, migration, and recovery coverage
- flake and maintenance policy
- known gaps, re-review triggers, and completion evidence

## Completion Gate

Do not call the strategy complete until critical requirements and high-impact failures map to executable or explicitly manual evidence, tests fail when representative behavior is broken, and untested risks are visible. Do not describe a change as tested when the relevant suite did not run.

## Conditional Reference

Read [Testing Evidence](references/testing-evidence.md) when choosing test layers, browser tools, accessibility evaluation, or security coverage.
