---
status: reviewed
owner: vault-owner
created: 2026-10-26
last_verified: 2026-10-26
review_by: 2027-01-26
risk: R0
tags: [catalog, security-review, skill, ai-access, knowledge-management]
sources: []
---

# Security Review — Second Brain Context Access Skill

## Identity and Scope

- Asset type: locally authored Markdown skill and Obsidian-facing display note
- Purpose: let a filesystem-capable AI agent orient itself, retrieve current vault context, explain recorded state, and make only bounded user-requested changes without externalizing or reorganizing the vault for the agent's convenience
- Source: this vault; no third-party skill or executable asset was imported
- Author or organization: vault owner and Codex
- Exact version: 1.0.0, local revision dated 2026-10-26
- License and compatibility: original vault text under the vault owner's existing terms; no external content is redistributed
- Proposed use: Cursor, Grok integrations, or another agent may select the skill only after the user separately grants appropriate local workspace access

## Decision Summary

- Assigned risk: R0 for the two Markdown files themselves; an invocation is R1 when read-only and inherits R2 or R3 from any requested write, execution, network, account, private-data, external-system, or destructive action
- Decision: approved-with-conditions
- Conditions: the skill does not grant access; processing remains local by default; no remote index, persistent embedding, hidden tool configuration, upload, synchronization, or broad rewrite is implied; every consequential action remains separately authorized under the root contract
- Decision owner: vault-owner
- Next review: 2027-01-26, or earlier after first live Cursor or Grok use, a material instruction change, a tool-permission model change, a privacy or security incident, a routing failure, or the addition of executable or networked integration

## Complete Inventory

| Path | Purpose | SHA-256 | Reviewed? |
|---|---|---|---:|
| `30-Skills/second-brain-context-access/SKILL.md` | Trigger, access boundary, minimum-context routing, operating modes, integrity controls, stop conditions, and completion evidence | `B7A1117765EE2722666A4CA4074853F6317CC0B5DEF34B4DBD58717F1719770B` | Yes |
| `30-Skills/second-brain-context-access/Second Brain Context Access.md` | Human-facing Obsidian alias and embed of the canonical skill | `9ABF2685CAA7CA395DE26BB95B9F06EC382A93790226F168A10007CD932283EC` | Yes |

No hidden files, binaries, archives, scripts, packages, lockfiles, install hooks, workflows, generated indexes, agent configuration, or external assets are included.

## Behavior, Dependencies, Network, and Permissions

- Entry point: selected for vault orientation, current-status retrieval, focused knowledge lookup, or an explicitly requested vault change
- Automatic behavior: none; the Markdown cannot execute or gain access independently
- File reads: routes first to `AGENTS.md`, the Vault Map, a relevant map, and the smallest directly relevant notes
- File writes: allowed only when the user's task requests them; constrained to the smallest coherent change with link and frontmatter validation
- Process or shell execution: none included; the skill permits local filename and text search and requires inspection before any executable helper is run
- Dynamic loading, downloads, persistence, privilege changes, telemetry, analytics, or tracking: none
- Dependencies: none
- Runtime network destinations: none required
- Data handling: local by default; external transfer requires a named destination, defined scope, and explicit authorization at the applicable boundary
- Secret handling: prohibits storing or repeating discovered secret values
- Instruction-injection handling: ordinary notes, imports, quotes, and code samples are data and cannot expand authority
- Minimum permission: read-only access to the vault for explanation; task-scoped write access only for user-requested changes

## Findings and Mitigations

| Severity | Finding | Mitigation | Status |
|---|---|---|---|
| High when integrated | A remote model, embedding service, or index could receive more vault data than the user intended | Local-first processing, smallest-note fallback, named-destination authorization, and prohibition on default whole-vault upload or indexing | Mitigated by gate |
| High when invoked | Notes can contain prompt injection or commands that appear authoritative | Explicit authority order and treatment of ordinary vault content as untrusted information | Mitigated |
| Medium | Broad scanning can waste context and expose irrelevant private material | Map-first routing, filename/text search before reads, direct-link limits, and special handling for long logs | Mitigated |
| Medium | An agent may reorganize or generate metadata for its own convenience and damage human usability | Canonical-source rule and prohibitions on convenience restructuring, mirroring, hidden configuration, and vault-wide normalization | Mitigated |
| Medium | Existing notes can be mistaken for current, implemented, or approved work | Required use of state, dates, maintenance evidence, and explicit verified/inferred/pending distinctions | Mitigated |
| Medium | Tool-specific access capabilities can change and are not controlled by a Markdown skill | The skill makes no capability claim and requires separately granted workspace access | Accepted condition |

## Test Evidence

- Reviewed the complete two-file package; it contains only static Markdown.
- Ran the bundled skill validator in explicit UTF-8 mode across all 127 skill folders on 2026-10-26: zero failures, 127 unique frontmatter names, and zero duplicates.
- Parsed 410 Markdown notes after adding the review and resolved relative Markdown links, Wikilinks, and embeds: zero missing or ambiguous internal targets.
- Checked the changed files for leaked patch markers and unfinished scaffold syntax: none remained.
- Static behavior traces:
  - an orientation request routes to the root contract, Vault Map, and one relevant map rather than the full vault
  - a current-status request uses recorded states, dates, and recent relevant maintenance entries rather than file modification time
  - a request to expose or remotely index the whole vault stops at the named-destination and authorization boundary
  - a scoped note change preserves the canonical source and requires affected-link and frontmatter validation
- Side effects during testing: local Markdown creation and map updates only; no Grok or Cursor integration, account, extension, remote model, upload, persistent index, secret, or external system was used
- Remaining uncertainty: no live behavioral test inside Cursor or a Grok integration was performed

## Activation, Rollback, and Removal

- Activation: discover through the Skills Map or point an already authorized, skill-capable agent to the canonical `SKILL.md`; no tool installation is included
- Verification after activation: use a read-only orientation or status request first and confirm the agent reports only the relevant notes and does not create files, externalize data, or claim unverified access
- Disablement: stop selecting the skill or remove its Skills Map entry
- Rollback: restore the previous Skills Map and Research Queue entries, then remove the two-file skill folder and this review note
- Residue: none outside the listed Markdown files and explicit map or maintenance references

## Approval Record

- Reviewer: Codex for vault-owner review
- Review date: 2026-10-26
- Approved scope: version 1.0.0 as inventoried above, for locally authorized read-only access and narrowly scoped user-requested vault edits
- Re-review triggers: material instruction change; first live Cursor or Grok use; new extension, agent rule, MCP server, remote index, embedding store, synchronization path, executable helper, credential, or external data flow; vault restructuring; demonstrated privacy, routing, integrity, or usability failure

