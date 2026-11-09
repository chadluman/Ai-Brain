---
name: version-control-workflow-design
description: Choose and operate a branching workflow — trunk-based, GitHub Flow, or legacy GitFlow — with short-lived branches, Conventional Commits, SemVer releases, and repository rulesets. Use when deciding how a team branches, merges, and releases.
---

# Version Control Workflow Design

## Outcome

Produce a branching and release workflow the team can actually follow: one named workflow, a stated branch lifetime, a commit convention, a versioning rule, and enforcement that makes the main branch stay deployable.

Use [Repository Topology Selection](../repository-topology-selection/SKILL.md) to decide monorepo versus polyrepo and ownership boundaries first; this skill decides how changes flow through whichever topology was chosen. Use [CI/CD and Release Design](../ci-cd-release-design/SKILL.md) for the pipeline that the workflow feeds.

## Snapshot and re-check

Research for this skill was checked 2026-11-09. Treat workflow guidance as durable, but re-check version numbers, platform features, and policy dates before citing them — they are a 2026-11-09 snapshot and may have moved on.

## Choosing a workflow

Match the workflow to how the team actually releases, not to how it wishes it released:

- **Trunk-based development** — developers commit to the main branch several times a day, either directly or through branches that live a day or less. It needs fast CI, feature flags to hide unfinished work, and a merge queue or equivalent to keep main green. It fits teams shipping continuously.
- **GitHub Flow** — the main branch is always deployable; work happens on short-lived feature branches merged through a pull request. This is the lightweight default for most web and SaaS teams that deploy frequently but want a review gate on every change.
- **GitFlow** — five branch kinds (main, develop, feature, release, hotfix), built for scheduled, versioned releases. Its creator added a note in 2020 recommending against it for continuous delivery, and it is now commonly labelled legacy. It remains a reasonable fit for versioned, on-premises software where several released versions are supported at once.
- **GitLab Flow** adds environment branches to the GitHub Flow shape; consider it only when environments genuinely need distinct branches rather than distinct deployments from the same branch.

Decide by release cadence and support obligations: continuous deployment points to trunk-based or GitHub Flow; scheduled versioned releases with multiple supported versions point to GitFlow. Record the decision and the reason; a workflow nobody can state is a workflow nobody follows.

## Branch lifetime

Branch lifetime is the metric that matters most. Long-lived branches accumulate merge conflicts, hide integration risk, and make review harder. Set a stated limit — a day or less for trunk-based work, a few days at most for GitHub Flow feature branches — and treat a branch that outlives it as a signal to split the work, not to extend the branch. Use feature flags or stacked changes (see [Code Review Practice Design](../code-review-practice-design/SKILL.md)) to land large work in small pieces instead of letting one branch grow.

## Commit and versioning conventions

- **Conventional Commits** (`feat:`, `fix:`, `BREAKING CHANGE:`) map onto Semantic Versioning (SemVer 2.0.0) so tooling can derive release versions and changelogs from commit history. They pay off most when downstream tooling consumes them — a changelog generator, a release automation tool, or consumers who upgrade by version number.
- On an internal service with continuous deployment and no versioned releases, the convention is ritual without semantic value; keep it only if the team finds the history readable, and say so explicitly rather than pretending it drives releases.
- One logical change per commit. Keep refactoring and behaviour change in separate commits so each can be reviewed and, if needed, reverted on its own.
- Every commit on the main branch builds and passes tests, so history stays bisectable. Rebase private, unshared branches freely; never rewrite history that others have already pulled.

## Repository rulesets

Hosting platforms are moving from classic branch protection toward repository rulesets as the enforcement mechanism. Encode the workflow in rulesets rather than in team habit alone: required pull-request review, required status checks (lint, typecheck, tests, build), and restrictions on who can push directly to protected branches. A gate that can be bypassed casually is not a gate; decide deliberately who may bypass and when, and log it.

## Failure modes

- Long-lived branches merged in one large, conflict-ridden pull request.
- A workflow chosen for a release cadence the team does not have — GitFlow overhead on a team that deploys daily, or trunk-based commits on a team with no fast CI and no flags.
- Commit conventions enforced by tooling nobody understands, producing meaningless `feat:` prefixes on every change.
- Branch protection that exists in the platform but is not required, so a failing check is ignored and merged anyway.

## Supporting skills

- [Repository Topology Selection](../repository-topology-selection/SKILL.md) — monorepo versus polyrepo, ownership, and release boundaries.
- [CI/CD and Release Design](../ci-cd-release-design/SKILL.md) — the pipeline, gates, and promotion path the workflow feeds.
- [Code Review Practice Design](../code-review-practice-design/SKILL.md) — pull-request size, review cadence, and stacked changes.

## State

Risk: R0 (draft).
Draft pending representative validation.
