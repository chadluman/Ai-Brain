---
name: rebuild-verification-design
description: Decide "close enough" with checks, not feelings: three-width website comparison, likeness scores, game self-tests, app runs, and a stopping rule. Use when judging whether a rebuild matches its original, and when deciding whether to refine again or stop.
---

# Rebuild Verification Design

## Outcome

A rebuild judged by checks, not by looking at it and feeling good about it: every comparison is recorded, every failure lists exactly what does not match, and the decision to refine or stop follows a rule agreed in advance.

## Supporting skills

Load only what the gap requires:

- [Evidence-Led Software Study Design](../evidence-led-software-study-design/SKILL.md) for the study records the checks compare against.
- [Clean Room Rebuild Design](../clean-room-rebuild-design/SKILL.md) for the Study, Build, Check, Refine loop these checks sit inside.
- [AI Agent Workflow Design](../ai-agent-workflow-design/SKILL.md) for stopping conditions, state, and human approval in multi-step agent work.

## Alpha status

The checks this skill describes belong to an early-alpha rebuild engine, and their behaviour changes between releases. The research behind this skill was checked 2026-11-05; re-check the source repository before relying on any detail, threshold, or limit stated here. The numbers below are the engine's stated rules as of that check, not measurements of this vault's own.

## Website checks: three widths, layout plus likeness

A website rebuild is served locally and compared with the original at three screen widths — desktop, tablet, and phone — on the start page plus a bounded set of linked pages. For each page and each width, the check compares:

- **Layout likeness:** page width, heading sizes, each section's padding, gap, content column, and items per row.
- **Perceptual likeness:** how alike the rendered pages look, scored as a detail measure and averaged with the layout measure over the pages checked.
- **Content:** the text, page structure, colours, fonts, text sizes, and spacing the build misses.
- **Health:** the errors, failed requests, and accessibility gaps the build adds that the original did not have.
- **Interaction:** the start page's menus, pop-ups, and tabs, opened on the build and compared — the first few only, never menus inside menus or hover-only ones.

Parts of the original that change by themselves are left out of the score, found by photographing the original several times and seeing what moves. A page that scrolls sideways, a heading size that differs, or a section whose padding, items per row, or content column differs is a named failure, not a vague "looks off."

## What a failed check must list

A check that finds a mismatch is not useful unless it says, per page and per width:

- What does not match, and by how much where that can be measured.
- Which widths the mismatch appears at.
- What the build adds that the original did not — errors, failed file loads, new accessibility gaps, a menu that does not open.
- Anything the check could not compare at all.

A check with anything it could not compare, or any claim that fails, is not good enough — it sends the build back for refinement, even if the overall score looks high.

## Game checks: the self-test and its limit

A game rebuild is ready only when its own self-test passes: the build plays its core loop with scripted input and reports whether the player moved, acted, and the heads-up display was drawn.

Know the self-test's limit and say it out loud: **the self-test is the build's own report.** The checker does not yet watch the game play or measure the values itself. A passing self-test means the build claims its loop works; it is not independent observation of play.

In Deep mode, a game's mechanics record is also checked for being readable and sourced, failing while a number found in the original is not used in the code — estimates may stay out. A Deep-mode game using the original's files must carry its credits file and the private-use line in its readme.

## App checks: build, run, compare

An app rebuild is checked by whether it builds, and by a screenshot compared with the pictures supplied by the person — and, when the original was studied while running, with the original's window too. In that case the build is also started normally and its window and labelled controls are compared with the original's.

Behaviour checks for apps and games are only partly built; the build, run, and screenshot checks are what exist today. Console apps are checked by matching the original's runs: same exit code, same output.

## The stopping rule

Refinement is bounded. The loop stops when one of these is true:

- **Likeness target reached:** a website reaches the agreed likeness score — the engine's stated target is 90% — with nothing uncompared and no failed claim.
- **Round limit reached:** the first build plus a bounded number of refinement rounds. The app's default allows more rounds than the command line's default; the request may change the number, but the number is agreed before building, not extended mid-loop on a feeling.
- **No progress:** two consecutive completed builder turns leave the app files unchanged. File contents and executable permissions decide progress — rewriting identical bytes does not reset the count. A successful check may still finish the second unchanged turn.

When the round limit or the no-progress rule stops the loop, the result is reported as stopped at the limit, not as finished. The check list at that point is the honest record of what still does not match.

## Mid-turn self-checks

The builder tests its own build mid-turn, with the same checks, for every target kind. A mid-turn check that fails is a refinement task for the same turn, not a note to revisit later. Do not wait for the end of a round to discover that a build does not run.

## Design checklist

Before accepting a rebuild as close enough, answer every line:

- [ ] Website builds were compared at desktop, tablet, and phone widths, with layout and perceptual likeness recorded per page.
- [ ] Every failed check lists what does not match, at which widths, and what the build adds that the original did not.
- [ ] Nothing was left uncompared without being listed as uncompared.
- [ ] Game builds passed their own self-test, and the self-report limit is stated alongside the pass.
- [ ] App builds were checked by building, running, and comparing screenshots and controls with the original.
- [ ] The stopping rule — likeness target, round limit, and two-unchanged-turns rule — was agreed before building and followed.
- [ ] A loop stopped at its limit is reported as stopped at the limit, with the remaining mismatches listed.

## State

This skill has not yet been exercised on a real rebuild check of a target the user owns. Promote it only after one such exercise, and revise it from the failures that exercise surfaces.

Draft pending representative validation.
