---
name: software-quality-review
description: Review a software change or component for specification quality, tests, defect risk, clarity, and readiness for change. Use for code-review preparation or engineering-quality findings; do not use as a substitute for domain-specific security, accessibility, or performance review.
---

# Software Quality Review

## Outcome

Produce actionable, evidence-based review findings that improve correctness, understandability, and change-readiness without replacing project conventions with personal style preferences.

Read [quality evidence](references/quality-evidence.md) when defining the review model or test expectations.

Use [Software Quality Assurance](../software-quality-assurance/SKILL.md) when the request concerns the preventive quality system or process, and [Release Quality Evaluation](../release-quality-evaluation/SKILL.md) when the request is to judge an exact release candidate.

## Review the Contract First

- Identify the intended behavior, inputs, outputs, preconditions, postconditions, invariants, errors, side effects, concurrency assumptions, and compatibility constraints.
- Flag ambiguity or mismatch between implementation, tests, documentation, and user-visible behavior.
- Prefer declarative contracts that let callers reason about behavior without reading implementation details.

## Review Correctness and Tests

- Partition meaningful input and state spaces; cover boundaries, invalid cases, empty cases, failure paths, and interactions between conditions.
- Distinguish unit, integration, contract, end-to-end, regression, property, and manual tests by the risk each addresses.
- Check that assertions verify user- or contract-relevant outcomes rather than incidental implementation details.
- Review static types, validation, defensive checks, failure timing, cleanup, retries, concurrency, determinism, and observability where applicable.
- Treat coverage as a clue to untested code, not proof of test quality.

## Review Understanding and Change-Readiness

- Check naming, cohesion, scope, dependency direction, duplication, hidden coupling, global state, control flow, comments, and module boundaries.
- Prefer comments that explain contracts, rationale, invariants, constraints, and non-obvious decisions rather than narrating syntax.
- Follow the repository's established formatter and conventions unless the task explicitly changes them.
- Distinguish a blocking defect from a maintainability suggestion or personal preference.

For browser behavior, prefer standards and interoperability evidence. The web-platform-tests project can inform cross-browser assumptions, but cloning or executing it requires separate review.

## Findings and Completion

Report findings in descending impact with location, violated contract or risk, evidence, consequence, and a concrete correction or test. Also report reviewed scope, tests actually run, untested areas, assumptions, and residual uncertainty.

Do not claim a change is correct because tests passed; state what those tests establish and what they do not.

