---
status: reviewed
owner: vault-owner
created: 2026-10-21
last_verified: 2026-10-21
review_by: 2027-01-21
risk: R0
tags: [catalog, security-review, obsidian, skill]
sources:
  - https://obsidian.md/help/
  - https://obsidian.md/changelog/2026-10-05-desktop-v1.14.4/
  - https://docs.obsidian.md/community-directory/developer-policies
  - https://obsidian.md/license
  - https://obsidian.md/privacy
  - https://obsidian.md/security
---

# Security Review — Obsidian Vault Practices Skill

## Identity and Scope

- Asset type: locally authored Markdown skill and references
- Purpose: answer Obsidian questions and guide safe, portable vault design, operation, troubleshooting, and extension decisions
- Source: this vault; research derived from linked official Obsidian sources
- Author or organization: vault owner and Codex
- Exact version: 1.0.0, local revision dated 2026-10-21
- Research baseline: Obsidian desktop 1.14.4 and official living documentation verified 2026-10-21
- License and compatibility: original vault text; external documentation is summarized and linked, not redistributed
- Proposed project use: automatic routing for Obsidian questions and requested vault work

## Decision Summary

- Assigned risk: R0 for the skill files themselves
- Decision: approved-with-conditions
- Conditions: re-verify version-sensitive facts; treat community plugins, extensions, automation, Sync, Publish, sharing, payment, and destructive changes under their actual R2 or R3 risk; do not infer authorization from the skill
- Decision owner: vault-owner
- Next review: 2027-01-21, or earlier for a major Obsidian release, security or privacy change, cited-page change, new executable integration, or observed skill failure

## Complete Inventory

| Path | Purpose | SHA-256 | Reviewed? |
|---|---|---|---:|
| `30-Skills/obsidian-vault-practices/SKILL.md` | Trigger, routing, decisions, permissions, and completion evidence | `DD490590561EBC41B5FDE443726D1B97152699EA548468DC30BF23B16F73A156` | Yes |
| `references/capability-map.md` | Current capability and feature-selection map | `622798C58BB0F336364D4A39F403436BD4B6757B80695E22CEB833511474EAF8` | Yes |
| `references/vault-design-practices.md` | Portable information architecture and workflow guidance | `542C41F8632DFFEE2D683DDF322CD47498C65EEB8F8CF1386788D257C5FCF0D4` | Yes |
| `references/safety-and-operations.md` | Plugins, imports, Sync, backup, Publish, automation, and troubleshooting | `FA7CA8EA2D676540E2FBF3F76ED3DF266D134468631E5B29B8355E684AB01E4A` | Yes |
| `references/official-sources.md` | Primary-source roles, links, dates, and evidence boundaries | `665FEC2720B9AF1369FCF57DDC59965D63A56158F9E06A94C4448E4A50A2D537` | Yes |

No hidden files, binaries, archives, scripts, packages, lockfiles, install hooks, workflows, or generated assets are included.

## Behavior, Dependencies, Network, and Permissions

- Entry point: loaded only when selected for an Obsidian-related request
- Automatic behavior: none; Markdown instructions cannot execute independently
- File access: directs read-only inspection to the smallest relevant vault scope and requires authorization for writes
- Process or shell execution: none included
- Dynamic code, downloads, persistence, privilege changes, telemetry, analytics, or tracking: none
- Dependencies: none
- Runtime network destinations: none; the skill routes research to official HTTPS sources when current verification is needed
- Secret handling: explicitly prohibits secrets in notes, commands, logs, or committed configuration
- Instruction-injection risk: imported or shared content is explicitly treated as untrusted and cannot override higher-priority instructions

## Findings and Mitigations

| Severity | Finding | Mitigation | Status |
|---|---|---|---|
| Medium | Obsidian features and service terms change over time | Dated baseline, official-source routing, and re-review triggers | Mitigated |
| High when invoked | Plugins inherit broad application permissions | Native-first rule and exact-version security review before activation | Mitigated by gate |
| High when invoked | Sync, sharing, Publish, and accounts transmit or expose data | R3 classification and explicit authorization at the consequential boundary | Mitigated by gate |
| Medium | Obsidian-specific Markdown can reduce portability | Plain-file source-of-truth rule and explicit portability tradeoff | Mitigated |
| Medium | Broad trigger could encourage loading excess context | Four focused references with task-specific routing | Mitigated |

## Test Evidence

- Format validation: passed the bundled skill validator on 2026-10-21
- Source review: official capability, storage, plugin-security, Sync, backup, collaboration, Publish, privacy, security, CLI, and release sources checked on 2026-10-21
- Static forward-test scenarios:
  - tag versus property question routes to vault design and preserves a minimal schema
  - plugin installation request stops at exact-version review and activation authorization
  - Sync setup separates backup from sync and stops before account, payment, encryption, or remote-vault changes
  - Bases question keeps Markdown properties as source data rather than creating a duplicate database
- Side effects during testing: none; no plugin, extension, account, service, or external system was activated
- Remaining uncertainty: no independent agent forward-test and no live Obsidian UI test were performed

## Activation, Rollback, and Removal

- Activation: link from `30-Skills/Skills Map.md`; no application installation required
- Verification after activation: use on a real Obsidian question, inspect whether it loads only the relevant reference, and record any routing or safety failure
- Disablement: remove the Skills Map link or stop selecting the skill
- Rollback: restore the prior map and source-registry revisions, then archive or remove the skill folder and this review note
- Residue: none outside the listed Markdown files

## Approval Record

- Reviewer: Codex for vault-owner review
- Review date: 2026-10-21
- Approved scope: version 1.0.0 as inventoried above, for advisory and user-authorized vault work
- Re-review triggers: material file change, major Obsidian release, official documentation or policy change, security advisory, new integration, or demonstrated skill failure
