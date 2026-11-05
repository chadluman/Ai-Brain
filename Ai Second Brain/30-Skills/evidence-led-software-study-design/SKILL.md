---
name: evidence-led-software-study-design
description: Study a target with real inspection tools first, and record every answer as evidence with confidence, coverage, and limits — before any building starts. Use when planning a rebuild, a teardown, or an investigation of existing software, and when deciding what is known, what is guessed, and what is still open.
---

# Evidence-Led Software Study Design

## Outcome

A study that a builder can start from without re-doing the inspection: every claim about the target is tied to recorded evidence, every gap is written down as an open unknown, and nothing is presented as settled until it has been compared against a second source or a live check.

## Supporting skills

Load only what the gap requires:

- [Clean Room Rebuild Design](../clean-room-rebuild-design/SKILL.md) for what the study may and may not look at once a rebuild mode is chosen.
- [Rebuild Verification Design](../rebuild-verification-design/SKILL.md) for how the study's records become the comparison baseline.
- [Interface Pattern Reconstruction](../interface-pattern-reconstruction/SKILL.md) for re-expressing observed behaviour as patterns without copying protected expression.
- [Web App Security Review](../web-app-security-review/SKILL.md) when the study touches authentication, sessions, or other security boundaries.

## Alpha status

The inspection engine this skill describes is early alpha, and its behaviour changes between releases. The research behind this skill was checked 2026-11-05; re-check the source repository before relying on any detail, capability, or limit stated here. Nothing in this skill is a promise that a particular inspection exists, works, or stays the same.

## Triage first: what kind of target is it

Do not start inspecting until the target kind is named, because the kind decides which surfaces are worth looking at and which are a waste of effort:

- **Website:** pages at several widths, visible text, layout, colours, fonts, spacing, menus, forms, links, and page health.
- **Desktop app:** its install folder, what it is built with, what to run next, and — only with permission and in the right mode — a picture of its window and its control tree.
- **Phone app:** its package, classes, resources, components, and, where a device is attached, its installed state, logs, and screenshots.
- **Game:** its engine and version, how its code ships, its scenes, its size, and the libraries its own files name.
- **Single file:** what kind of packed or compiled file it is, and which reader can open it safely.

Record the triage answer before going deeper. If the triage cannot identify the kind, that is an unknown to record, not a reason to guess and proceed.

## Choose the inspection surface per kind

For each kind, pick the narrowest surface that answers the question at hand:

- For a website, capture the pages a visitor actually sees, at desktop, tablet, and phone widths, plus a few linked pages — not the whole site at once.
- For a desktop app, start with a static inventory of the folder and a statement of what it is made with; run it only once, briefly, for a window picture and control outline, and never drive it or watch it over time unless that is the question.
- For a phone app, prefer static reading of the package; device-connected inspection is a separate step with its own setup and its own limits, and much of it is still unverified — treat device results as provisional.
- For a game, identify the engine first; the engine decides the rebuild stack and which files are even readable.
- For a file, route it through the one reader built for its format; do not force a reader meant for another format and treat its output as evidence.

A surface that was not inspected is not "probably fine" — it is uninspected, and the study says so.

## Evidence, findings, and unknowns are three different things

Keep them separate, because mixing them is how a guess becomes a fact in the next step:

- **Evidence record:** what was observed, when, with which tool, and with what confidence, coverage, and limits. A record can be strong, partial, or weak — say which.
- **Finding:** a settled answer built on one or more evidence records, with a link back to each record it rests on. A finding can be corrected, but a correction keeps the same identity and requires valid evidence; it never silently rewrites history.
- **Unknown:** a question the study could not answer, recorded explicitly with what was tried. Open unknowns are reported at the end of a run, not buried.

An uncompared claim is not a fact. A claim that has been observed once, by one tool, with no second look, is at most a provisional finding — label it that way and say what comparison would settle it.

## Summary first, then page through large results

Large results arrive as a summary first. Read the summary, decide which slice matters, and then page through only that slice, narrowed by the fields you care about. Do not re-run an inspection to get a narrower view when the recorded result can be narrowed instead.

When a comparison is too large for one pass, page through it in slices and keep the record of which slices were checked. A check that never reached a slice cannot claim that slice matches.

## What a good study hands over

Before any building starts, the study should be able to answer, from its records:

- What the target is, in kind, and what it is made with.
- Which surfaces were inspected, and which were deliberately left alone.
- What was found, with the evidence behind each finding.
- What is still unknown, and what would answer it.
- What the study could not compare, so the builder knows where confidence is thin.

If any of those answers is missing, the study is not finished — it is paused, and the handover says so.

## Design checklist

Before handing a study to a builder, answer every line:

- [ ] The target kind is named and the inspection surface was chosen for that kind.
- [ ] Every finding links to the evidence records behind it, with confidence, coverage, and limits stated.
- [ ] Every unanswered question is recorded as an open unknown, with what was tried.
- [ ] Large results were read summary-first and paged, with the checked slices recorded.
- [ ] No claim is presented as settled on a single uncompared observation.
- [ ] Surfaces that were not inspected are listed as uninspected, not assumed fine.
- [ ] The handover lists what the study found, what it did not find, and what would settle the open unknowns.

## State

This skill has not yet been exercised on a real study of a target the user owns. Promote it only after one such study — study step only, no build — and revise it from the failures that exercise surfaces.

Draft pending representative validation.
