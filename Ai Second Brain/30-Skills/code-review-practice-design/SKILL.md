---
name: code-review-practice-design
description: Design a code review practice with small pull requests, a first-response target, checklists, stacked changes, and AI-assisted review as a first pass with a human gate. Use when review is slow, rubber-stamped, or a bottleneck.
---

# Code Review Practice Design

## Outcome

Produce a review practice that catches real defects and spreads knowledge without becoming the bottleneck: small pull requests, a stated first-response target, a shared checklist, and a clear rule for when AI-assisted review helps and when a human decides.

Use [Software Quality Review](../software-quality-review/SKILL.md) for the wider review of specifications, tests, and maintainability, and [Test Strategy Design](../test-strategy-design/SKILL.md) for deciding what test evidence a change should carry into review.

## Snapshot and re-check

Research for this skill was checked 2026-11-09. Treat review-practice guidance as durable, but re-check version numbers, platform features, and policy dates before citing them — they are a 2026-11-09 snapshot and may have moved on.

## Pull-request size

Size is the single most controllable lever on review quality. Defect detection drops sharply above roughly 400 lines in one review session, or above about 60 minutes spent reviewing in one sitting — figures from a cited study of 2,500 reviews, treated here as a guide rather than a hard law. Under roughly 100 lines is the fastest-reviewed sweet spot. Set a size expectation for the team, measure it, and treat a consistently oversized pull request as a planning failure (the work was not split), not as a reviewer failure.

## First-response target

Set a first-response target and publish it. A common target is a first response within 24 hours, with 24–48 hours as the usual service-level range. The target is for a first substantive response, not for approval: a reviewer who asks a question or requests a change within the window has met it. Track the target; a target nobody measures is a wish. If review consistently misses the target, the cause is usually too few reviewers, too-large pull requests, or review treated as lower priority than new work — fix the cause, not the clock.

## Review checklist

Review against a short, shared checklist rather than from memory or taste. A useful checklist covers: correctness (does it do what the change claims, including edge cases), security and privacy, performance (for example, queries in loops or unbounded work), readability, and whether tests are included and actually exercise the change. Keep the checklist short enough to use every time; a checklist nobody reads is decoration. Automate what a machine can check — formatting, lint, types, tests — in CI, so human review time goes to intent and risk, which machines cannot judge.

## Separating refactor from behaviour change

Never mix a refactor and a behaviour change in one pull request. A reviewer cannot tell whether a behaviour change is intended when it is buried inside moved code, and a revert then takes the refactor down with the fix. Put the refactor in its own change first, land it, then put the behaviour change on top. When a change is too large to review as one pull request, use stacked pull requests — a chain of small, independently reviewable changes — or a feature flag to land work incrementally behind a switch.

## AI-assisted review

AI-assisted review is now common as a first pass: it is good at spotting surface issues, missing tests, and style drift. Treat it as a first pass only. A human reviewer remains the gate for intent (is this the right change at all?), risk (what breaks if this is wrong?), and context the model cannot see (team conventions, product history, security judgement). Never let an automated approval substitute for a human one on a change that touches security, payments, data migration, or user-facing behaviour.

## Failure modes

- Large pull requests rubber-stamped because nobody can hold the whole change in mind.
- Review as gatekeeping — the reviewer as an obstacle — instead of knowledge transfer; the author should come out of review understanding the code better, and the reviewer should too.
- Review latency that pushes authors to merge without review, or to batch work into even larger pull requests.
- Checklist items that are really style preferences argued as if they were correctness issues; settle style with tooling, not with review comments.

## Supporting skills

- [Software Quality Review](../software-quality-review/SKILL.md) — reviewing specifications, tests, clarity, and maintainability.
- [Test Strategy Design](../test-strategy-design/SKILL.md) — what test evidence a change should carry.
- [CI/CD and Release Design](../ci-cd-release-design/SKILL.md) — automated gates that run before human review.
- [Version Control Workflow Design](../version-control-workflow-design/SKILL.md) — branch lifetime and commit hygiene that keep pull requests small.

## State

Risk: R0 (draft).
Draft pending representative validation.
