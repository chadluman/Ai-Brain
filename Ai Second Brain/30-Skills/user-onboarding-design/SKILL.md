---
name: user-onboarding-design
description: Design a first-run path that gets a new user to one meaningful outcome, not a tour of every feature, so activation can be measured and improved. Use when a product has a free trial, signup, or first-run setup; do not use for marketing pages or for in-product help in general.
---

# User Onboarding Design

## Outcome

Produce a first-run path with one defined activation event, one primary path to it, and measurements for time to activation and drop-off per step, so onboarding can be improved from evidence instead of redesigned from opinion.

Use [Product Discovery and Scope](../product-discovery-scope/SKILL.md) to decide what the product is for. Use this skill for the first session after that decision: getting a new user to the first moment the product actually helps them.

## Required Inputs

- The activation event: the single action in a user's first session that best predicts long-term retention, chosen from cohort data where possible, not from intuition.
- The user segments that change the first path: role, goal, or plan, and only those that change the first outcome, not every persona the marketing site lists.
- The minimum setup the activation event requires: accounts, connections, permissions, or data, with each item justified against that event.
- The measurement plan: time to activation, completion per step, and the recovery path for users who stall.
- The constraints: accessibility, privacy, and billing consent, including anything that must never be collected or charged during onboarding.

If there is no activation event, define one before designing screens. A tour with no activation event is theatre: it can be completed perfectly while the user never receives value.

## Workflow

1. Define activation before designing. Compare users who stayed with users who left early, and find the first-week action that best separates them. That action, not signup and not tour completion, is the target every onboarding decision serves.
2. Build one primary path to that event, the minimum path to first value. Hide everything that does not serve it in the first session, use sane defaults instead of configuration, and defer every other choice until after activation. One path, one outcome, in the first session.
3. Ask only what the first outcome needs. Each question, permission, or connection in onboarding must be justified by the activation event. Anything else is deferred, optional, or removed. Long upfront forms are the most common way to lose a user who was already convinced.
4. Replace blank states with a working starting point. Use sample data that is clearly marked and deletable, a template, or a guided first action on the user's own data, so the user never faces an empty dashboard with no next step.
5. Use progressive disclosure after activation, not before it. A checklist is useful when each item ends in an outcome, not when it ends in a setup state. Contextual guidance belongs at the moment of need, in the flow, not in a separate tour the user must remember.
6. Design recovery for stalled users as part of onboarding, not as a separate retention project. A user who stops mid-path should return to exactly one next step, reachable by a deep link, with progress preserved. Notifications and emails, if used, should reinforce that one next step, not introduce three new features.
7. Measure and iterate per step. Track time to activation and drop-off at each step, review it regularly, and change one step at a time. A redesign that changes every step at once cannot be attributed to anything.
8. Respect consent and accessibility throughout. Onboarding must be keyboard-accessible and screen-reader-usable, must not trap a user in a flow they cannot skip or exit, and must not obtain billing consent, data access, or permissions by confusion. See [Web Accessibility Review](../web-accessibility-review/SKILL.md) and [User Account Lifecycle](../user-account-lifecycle/SKILL.md).

## Safety and Permission Boundaries

- Never collect personal data, platform permissions, or payment details during onboarding that the activation event does not require. Each collection is a privacy and trust decision, reviewed at the boundary that applies.
- Never use onboarding to obscure a charge, a subscription, or a data use. Trial, billing, and cancellation terms belong in plain language before the user commits, not after.
- Sample data must never contain real users' data, and a user's first-run data must never be visible to another user through a shared template or demo state.
- A new onboarding, analytics, or messaging tool still requires the root security-review gate at its exact version. This skill approves no provider or package.

## Outputs and Evidence

- An activation event definition, with the cohort evidence or the hypothesis and the test that will replace it.
- A minimum path to first value, with deferred items listed explicitly.
- A measurement plan: time to activation, per-step drop-off, and the stalled-user recovery path.
- Tests or a test report covering the full first-run path, including skip, exit, return, and accessibility checks.
