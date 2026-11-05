---
name: clean-room-rebuild-design
description: Rebuild software from observable behaviour only, choosing Clean room or Deep mode deliberately and recording what each mode refuses. Use when recreating a website, app, or game you own or are allowed to examine, and when deciding how much of the original the rebuild may look at.
---

# Clean Room Rebuild Design

## Outcome

A rebuild whose method is chosen on purpose, not by accident: the mode is named, what it may and may not use is written down, anything it refuses is recorded, and the result recreates layout, style, and behaviour from evidence without copying protected expression.

## Supporting skills

Load only what the gap requires:

- [Interface Pattern Reconstruction](../interface-pattern-reconstruction/SKILL.md) — the closest existing skill. Study authorized product behaviour there and re-express useful patterns; this skill builds on it and does not restate it.
- [Evidence-Led Software Study Design](../evidence-led-software-study-design/SKILL.md) for the study step that comes before any building.
- [Rebuild Verification Design](../rebuild-verification-design/SKILL.md) for deciding when the rebuild is close enough.
- [Faux Product UI Design](../faux-product-ui-design/SKILL.md) for the honesty boundary: a rebuild or a demo must never stand in for a shipped capability or a live state, and must not borrow another product's identity or logo.
- [Open Source License Review](../open-source-license-review/SKILL.md) for licence evidence, obligations, and compatibility before reusing anything.

## Alpha status

The rebuild engine this skill describes is early alpha, and its behaviour changes between releases. The research behind this skill was checked 2026-11-05; re-check the source repository before relying on any detail, capability, or limit stated here. No live Clean room build has been reported as run yet — do not present a Clean room build as proven.

## The loop: Study, Build, Check, Refine

A rebuild runs in four steps, in order, and repeats the last three until the stopping rule is met:

1. **Study:** inspect the original and record evidence, findings, and open unknowns.
2. **Build:** a coding agent builds a new project in the language, framework, or engine the request names, or a sensible default for the target kind.
3. **Check:** compare the build with the original and list what does not match yet.
4. **Refine:** change the build from the check's list, then check again.

The builder leads the loop: it studies, asks follow-up questions of the inspection tools, records what it cannot find out as unknowns, and tests its own build mid-turn with the same checks. A turn cut off by a time limit, crash, or dropped connection can resume a bounded number of times; beyond that, stop and ask a person.

## Choose the mode deliberately

Record the mode before the study starts, and record every refusal the mode produces:

- **Clean room (the default):** nothing inside the original is read — not its code, files, or page source. The rebuild works from what a visitor can see: pictures supplied by the person, the website as a visitor sees it (screenshots, visible text, measured layout, colours, fonts, spacing, menus opened), and, when allowed, a picture of the app's window. Tools that would look inside are refused, and the refusal says how to turn on Deep mode. A new inspection tool is Deep-only until it is explicitly listed as Clean room safe, and may only be listed if it touches no target or watches from outside, as a visitor or user would.
- **Deep:** every inspection tool is used, for private use. A program's code and files are read with the built-in engines (and an external decompiler when installed), a website's scripts are read and its start page watched, and the builder may use all of them.

The mode is a rule about what the engine offers and refuses. It is not an operating-system sandbox: it does not isolate the computer. A coding agent still acts with its own permissions, and what it can read, write, or run depends on those permissions. How far the mode's refusals reach into an agent's own tools differs by agent — check the operations skill before assuming a refusal holds everywhere.

## Only software you own or are allowed to examine

Use a rebuild workflow only on software you own or are allowed to examine. It never bypasses digital locks, logins, or anti-cheat measures. If the only way to see something is to defeat a protection, a login, or an anti-cheat check, that something is out of scope — record it as an unknown and move on.

## Do not copy protected expression

The builder is told not to copy logos, photos, or text unless the person confirms they own them or have permission. Rebuilds recreate layout, style, and behaviour from evidence; they do not reproduce the original's protected expression.

- In Clean room, no file from the original is copied at all.
- In Deep mode, readable files from the original may be reused only for private use — never by decrypting anything — and only when generated pictures and models replace the original art where that option is turned on. Anything reused this way is listed with credits, and the private-use line is stated in the rebuilt project's own readme.
- Never copy code, scripts, schemas, names, assets, or wording from another project into the vault, the docs, or the rebuild unless ownership or permission is confirmed.

## Record what each mode refuses

Every refusal is part of the design record, not an error to hide:

- Which tools were refused, and in which mode.
- What the study could not see because of the refusal.
- Whether switching modes would answer it, and why the switch was or was not made.

A rebuild that cannot say what it was refused cannot say what it actually knows about the original.

## Design checklist

Before starting a rebuild, answer every line:

- [ ] The target is software you own or are allowed to examine, and that permission is recorded.
- [ ] The mode (Clean room or Deep) is chosen deliberately and written down before the study starts.
- [ ] What each mode may use — and what it refuses — is recorded, including every refusal encountered.
- [ ] No step depends on bypassing a digital lock, a login, or an anti-cheat measure.
- [ ] No logo, photo, text, file, or piece of code is copied without confirmed ownership or permission.
- [ ] Any original material reused in Deep mode is private-use only, credited, and stated as such in the rebuilt project's readme.
- [ ] The rebuild does not present itself as the original, borrow the original's identity or logo, or stand in for a shipped capability or live state.
- [ ] The Study, Build, Check, Refine loop and its stopping rule are agreed before building starts.

## State

This skill has not yet been exercised on a real rebuild of a target the user owns. Promote it only after one such exercise, and revise it from the failures that exercise surfaces.

Draft pending representative validation.
