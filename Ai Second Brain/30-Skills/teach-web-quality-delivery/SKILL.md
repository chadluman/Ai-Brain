---
name: teach-web-quality-delivery
description: Teach software quality and delivery through tests, review, reproducible environments, dependency lifecycle, CI/CD, release evidence, observability, incidents, and handoff. Use for quality engineering, DevOps, production-readiness, or team-practice instruction for web projects.
---

# Teach Web Quality and Delivery

## Outcome

Help the learner build evidence that a change is correct, releasable, observable, recoverable, and maintainable by someone other than its author.

Follow the shared [lesson contract](../teach-senior-web-development/references/lesson-contract.md).

## Route Supporting Knowledge

- [Test Strategy Design](../test-strategy-design/SKILL.md), [Software Quality Review](../software-quality-review/SKILL.md), and [Software Quality Assurance](../software-quality-assurance/SKILL.md) for risk-based evidence and review.
- [Release Quality Evaluation](../release-quality-evaluation/SKILL.md) for candidate-specific disposition and residual risk.
- [Developer Environment Reproducibility](../developer-environment-reproducibility/SKILL.md), [Build and Package Toolchain](../build-package-toolchain/SKILL.md), and [Repository Topology Selection](../repository-topology-selection/SKILL.md) for repeatable engineering workflows.
- [Codebase Module Boundaries](../codebase-module-boundaries/SKILL.md) and [Dependency Upgrade Operations](../dependency-upgrade-operations/SKILL.md) for maintainability and change isolation.
- [CI/CD and Release Design](../ci-cd-release-design/SKILL.md), [Hosting and Runtime Selection](../hosting-runtime-selection/SKILL.md), and [Feature Flag and Rollout Design](../feature-flag-rollout-design/SKILL.md) for delivery.
- [Observability and SLO Design](../observability-slo-design/SKILL.md), [Incident Response](../incident-response/SKILL.md), and [Documentation and Handoff](../documentation-handoff/SKILL.md) for operation and learning.

## Teaching Priorities

Start from product risk and define what evidence would change a release decision. Teach test layers by the failures they catch, not by a target pyramid or coverage percentage. Include reproducible setup, deterministic commands, failure diagnosis, artifact provenance, release criteria, monitoring, rollback, and ownership.

Use exercises with a seeded defect, flaky dependency, failed build, unsafe rollout, missing signal, or incident scenario. Require the learner to distinguish prevention, detection, mitigation, recovery, and follow-up improvement.

For senior-level practice, ask the learner to make a bounded release recommendation, explain evidence gaps, balance speed and confidence, and improve the system so the same class of failure is cheaper to detect next time.

## Boundaries

- Passing tests are evidence for named behaviors, not proof of total correctness or safety.
- Do not install tools, alter CI, deploy, publish, change production monitoring, or trigger failure in a live environment without the applicable review and authorization.
- Keep secrets and private production data out of examples, fixtures, logs, screenshots, and artifacts.
- Distinguish simulated drills from observed production behavior and qualitative review from automated results.

## Completion

The learner maps risks to evidence, reproduces the workflow, diagnoses a controlled failure, explains release and rollback criteria, identifies operational signals and ownership, and leaves a handoff another engineer can follow.
