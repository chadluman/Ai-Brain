---
name: soc2-change-control-design
description: Design change control that satisfies SOC 2 CC8.1 for a small team: protected main, pull-request-only deploys, deployment history as the change log, reviewed schema migrations, and ticketed console changes, with a defined emergency path that is logged and retrospectively reviewed rather than a standing bypass. Use for any production system heading toward SOC 2; do not use to justify direct-to-production changes, and do not treat self-approval as a substitute for a complete record.
---

# SOC 2 Change Control Design

## Outcome

Make every material production change traceable end to end — authorised, reviewed, tested as appropriate, deployed through the pipeline, and retrievable by an auditor sampling any change in the period — with no "direct to prod" gaps.

## Supporting Skills

Load only what the gap requires:

- [SOC 2 Control Matrix and System Description Design](../soc2-control-matrix-and-system-description-design/SKILL.md) for mapping CC8.1 to a control and evidence source.
- [SOC 2 Evidence Operations Design](../soc2-evidence-operations-design/SKILL.md) for filing change evidence by criterion.
- [Dependency Upgrade Operations](../dependency-upgrade-operations/SKILL.md) for routine and breaking dependency changes, which are changes too.

## Design

1. **Protect main, including from the founder.** Require a pull request, required status checks, no force-push, and no direct push — even for a solo builder. A solo pull request is not bureaucracy; it is the record. "I am the reviewer, so I approved my own pull request" is accepted by auditors for a one-person organisation only if the record is complete and consistent (pull request plus checks plus deploy log plus ticket), and they will probe it harder, not less.
2. **Deploy only through the pipeline.** Git deployments only; no manual drag-and-drop production deploys, no unrecorded manual uploads. Preview deployments for every pull request, so the change that reaches production is the change that was reviewed.
3. **Treat every production change as a change.** Code, schema, configuration, environment variables, and infrastructure all count. Schema migrations are reviewed files, never ad-hoc direct database DDL on production without a ticket. Environment-variable changes are logged as a change — the value never goes in the ticket.
4. **Ticket console changes.** Every manual console change — a database data fix, a hosting environment tweak, a payments dashboard setting — gets a ticket before or immediately after, recording what, why, and who. Console hotfixes without a ticket are the classic Type II exception.
5. **Define the emergency path, then close it after use.** An emergency change may bypass the normal pipeline only through a defined, logged path: what counts as an emergency, who may invoke it, what record is created, and what retrospective review follows. The retrospective review is mandatory, not optional, and it either ratifies the change with a follow-up pull request or rolls it back. A standing bypass is not an emergency path.
6. **Retain the deployment history as the change log.** Hosting deployment history (who, what, when, preview-to-production promotion) is the auditor's sample set. Do not delete or prune it inside the observation period, and do not deploy in a way that leaves no history.
7. **Version and retain releases.** For a desktop or app component, releases are versioned, signed where applicable, with a changelog and a retained rollback build. A release that cannot be rolled back is a change without a recovery plan.

## Guardrails

- Do not approve your own change and call the record complete if any link is missing. A pull request without checks, a deploy without a pull request, or a console change without a ticket is a gap, however good the change was.
- Do not put secrets in a change ticket, a migration file, or a changelog. The change record describes the change; credentials live in the secret store.
- Do not let a hotfix habit form. Three emergency changes in a quarter are a process failure to fix, not a pattern to normalise.
- Do not confuse "tested" with "reviewed" or "approved". A change needs the combination the matrix states for its risk level; a green check suite does not authorise a schema change, and an approval does not test one.

## Verification

Change control is ready when: a sample of ten production changes, chosen by someone other than the author where possible, traces end to end (ticket or pull request, approval, checks, deployment record, and, for console changes, the retrospective ticket) with no gaps; no direct pushes to main exist in the period; no production deploy exists without a pipeline record; and at least one emergency-path invocation, if any occurred, has a completed retrospective review.
