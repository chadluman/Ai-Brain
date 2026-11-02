---
name: soc2-evidence-operations-design
description: Operate the evidence discipline a SOC 2 Type II audit is actually won or lost on: timestamped, indexed, never-backdated evidence organised by criterion, a calendar cadence for quarterly and monthly artefacts, and a prepared-by-client index an auditor can sample from. Use for any SOC 2 observation period and for the practice period before it; do not use to reconstruct missing evidence after the fact, and never backdate an artefact.
---

# SOC 2 Evidence Operations Design

## Outcome

Run an evidence operation that survives sampling: every control in the matrix produces dated evidence on a provable cadence, an auditor can find it by criterion without asking the author, and a missing quarter is impossible to hide — because it never happens, not because it was recreated.

## Supporting Skills

Load only what the gap requires:

- [SOC 2 Control Matrix and System Description Design](../soc2-control-matrix-and-system-description-design/SKILL.md) for the matrix the evidence must feed.
- [Audit Log Design](../audit-log-design/SKILL.md) for what to log; this skill adds only the SOC 2 layer: retention period, tamper protection, periodic review evidence, and a named owner per log source.
- [Backup and Disaster Recovery](../backup-disaster-recovery/SKILL.md) for restore testing; this skill adds only the dated restore record an auditor samples.
- [Incident Response](../incident-response/SKILL.md) for the runbook; this skill adds only the incident register, notification decisions, and postmortem linkage.

## Design

1. **Organise evidence by criterion, not by date or by tool.** One folder (or one index) per criterion, containing the evidence for that criterion across the period. An auditor samples by criterion; evidence organised by month forces the auditor to reconstruct the criterion view, and reconstruction finds gaps.
2. **Index everything.** Maintain a prepared-by-client (PBC) index: control → evidence → period → location. If an artefact is not in the index, it does not exist for audit purposes, however real it felt when it was produced.
3. **Set a calendar cadence and keep it.** Quarterly: access reviews, risk reassessment, vendor review checks, restore tests. Monthly: billing reconciliation (where Processing Integrity is elected, or for financial hygiene regardless), log review. Continuously: change history (pull requests, deployment history), incident register entries, secret rotation logs. Put each cadence item on a calendar with a named owner, so a missed item is visible the week it is missed, not at audit time.
4. **Run a practice period before the observation clock.** Before the Type II period starts, run the full cadence once and trace a mock sample end to end: ten changes and one quarter of access reviews, from control to evidence, with no gaps. Fix the cadence, then start the clock. A practice period that finds gaps is a success; an observation period that finds them is an exception.
5. **Timestamp, never backdate.** Evidence carries the date it was produced. A review, a restore test, or a vendor check done late is recorded late, with a note explaining the lateness — or it is recorded as missing, with a remediation note. Backdating is worse than a gap: it undermines the credibility of every other artefact.
6. **Ship logs off short-retention platforms on a schedule.** Hosting and database log retention is plan-limited and short on low tiers; the 2026-11-02 research run did not verify current Vercel or Neon retention windows, so no retention number from memory may be cited. Export or ship logs to durable storage (for example, an append-only database table or a log service) on a schedule, state the retention actually operated, and name an owner per log source. Never log secrets, tokens, stream keys, or full webhook payloads.
7. **Protect evidence from alteration.** Audit logs live in an append-only store with a separate role that cannot update or delete. Review records, restore records, and vendor reviews are versioned (for example, by pull request) so a change leaves a history. If evidence can be silently edited, it is not evidence.

## Guardrails

- Do not assemble evidence at audit time. An auditor samples across the period; a folder created the week before fieldwork is visible as such, and its contents will be treated accordingly.
- Do not recreate a missing quarter. A missing access review, restore test, or vendor review cannot be recreated. Record it as missing, remediate the cadence, and let the auditor judge the exception.
- Do not let a compliance platform's green dashboard substitute for the index. A platform automates collection; the index, the cadence, and the review judgement remain human work.
- Do not store evidence containing secrets or personal data beyond what the auditor needs. Redact tokens and keys from screenshots and exports before filing.
- A readiness firm that is also the auditor creates an independence problem. Readiness and examination must be separate firms or teams.

## Verification

An evidence operation is ready when: every matrix control has at least one dated artefact in the practice period; the PBC index covers every criterion with no orphan artefacts and no missing criteria; a mock sample of ten changes and one quarter of reviews traces end to end without a gap; log retention actually operated matches the stated retention; and a spot check of five artefacts shows dates consistent with their content (no artefact dated before the system it describes existed).
