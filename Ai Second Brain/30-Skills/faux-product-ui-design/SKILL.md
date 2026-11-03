---
name: faux-product-ui-design
description: Design a faux product UI — a still illustration or a short animated demo with a cursor — that reads as a real product, for a marketing page, feature card, docs hero, or product shot. Use whenever someone wants a mocked or fake UI, a product demo or walkthrough animation, a hero or feature-card illustration of an app, or an animated cursor doing one thing in an interface, even if they never say "faux UI". Do not use for the product itself, for screenshots of real user data, or for anything that must show live state.
---

# Faux Product UI Design

## Outcome

Produce one believable miniature of a product interface — a still, or a short animation in which one thing happens — that a viewer instantly recognises as that product, without it pretending to be a live screenshot, a real account, or real data.

## The one idea

**It reads as a real product, simplified to what the viewer needs, framed with intent, and every motion has a cause.**

That sentence is the whole skill. Every decision below is a way of honouring it: keep what the story needs, cut what it does not, frame the result on purpose, and never move anything without a reason the viewer can follow.

## Relationship to Stageshow

This skill is an original distillation of that idea, written for this vault. It is not a copy of Benji Taylor's Stageshow skill, its kit, or its examples, and it ships no code, no component kit, and no example library. If a project wants Stageshow itself, install it from its own repo (`npx skills add benjitaylor/skills --skill stageshow`) and follow its own licence and notices: the skill code is MIT, but its example app icons and some brand artwork are explicitly not covered by that licence, and product names and marks remain with their owners. Borrow an interaction pattern; never borrow another product's identity, logo, or trade dress.

## Supporting skills

Load only what the gap requires:

- [Interface Quality Review](../interface-quality-review/SKILL.md) for a final pass over functional, state, coherence, and craft defects in the finished frame.
- [Livestream Overlay Transport Design](../livestream-overlay-transport-design/SKILL.md) when the faux UI is illustrating a livestream surface rather than a marketing page — the two are different jobs, and this skill covers only the illustration.

## Use when

- A marketing page, feature card, docs page, or pitch deck needs a picture of the product in use.
- A hero needs a short looping demo of one interaction: one thing happens, one payoff lands.
- A feature needs a still that shows its result at a glance, at the size it will actually be seen.
- A cursor walkthrough would explain the feature faster than words.

## Do not use when

- The picture must show real data, a real account, or live state. Build the real thing, or label the picture clearly as an illustration.
- The brief is a wireframe, a spec, or an accessibility audit. Those need completeness and precision; this skill deliberately trades both away for readability.
- The picture could mislead a viewer into believing a feature, integration, or result exists when it does not. A faux UI illustrates a design; it must never stand in for a shipped capability. For a product still in development, say so beside the illustration, not inside it.

## Five ways it fails

Check the work against these before anything else. Any one of them is enough to send it back.

1. **Overloaded.** Real text in every row, numbers everywhere, everything packed. The more detail, the more it looks generated. Simplify the words, not the context.
2. **Wireframe-thin.** Two grey blobs and a button, built too small or stripped of what made it recognisable. If a viewer cannot name the kind of product, it is not done.
3. **Screenshot-in-a-card.** A whole window shrunk into a card with even margins all round. That is a screenshot pasted in, not a product shot. Crop to the panel where the story happens.
4. **Flat.** Every object the same weight in the same bordered card, so the eye has nowhere to land. One thing leads; everything else quiets down.
5. **Off-brief.** A grey window with a cursor, whatever the brief asked for. The brief's look and energy — a blueprint, glass over colour, a phone island, a mascot — are the point. Build them in full, to these rules.

## Workflow

Most of the quality is decided before any code. Write the plan first: where it sits, the focal object, the action, the payoff, and what can be left out.

### 1. Medium and place

Still or animation (loop, play once in view, or play on hover). The page it sits on, the ground it sits against, and the width it will be seen at. Design at the seen size, never at a comfortable working size and shrunk later: roughly 720 x 340 for a hero beside copy, 900–1100 wide for a full-width hero, about 400 x 300 for a card, shown at 1:1. Never go under about 320 wide for a demo; a bento tile or a small satellite card may be smaller, but only as part of a set planned together.

### 2. Look

Map the product's own tokens first — its colours, type, radii, spacing, icons, and real chrome — and use the product's own components inside the frame when the developer offers them. Otherwise pick a theme (light, dark, blueprint, glass), a palette (one accent, or mono), and a fidelity:

- `minimal`: placeholder bars everywhere, no real words.
- `standard`: real words where they carry meaning, bars elsewhere. The default.
- `realistic`: real content everywhere. Use it at hero scale, for a named real product, or for a still whose subject is a list or a page.

A brief with a style of its own (playful, paper, poster colour) gets that style in full, still built to these rules.

### 3. Story

One shape: how it feels to use, a flow through the app, or what the system does on its own. Three to five beats and a payoff, 10–16 seconds for an animation. No cursor move you cannot explain. Data never rewinds in view without a cause. Between a richer story and a calmer frame, choose the frame.

### 4. Start from a reference

Start from the closest finished example you already have — your own, or a gold example from a library you are licensed to use — and copy its structure: stage size, crop and bleed, row and type sizes, spacing, and the script's beats. Do not rewrite it from a glance. Then replace its look and content with the brief's product. A copy that only changes the name is not done: it should read as the brief's product, not the reference's. If no reference tells your story, choose in two parts: the layout first, from a layout you have already validated, then borrow the motion for your beats from the reference whose story is closest, and build what neither has in the same style.

### 5. The screen

Count the real strings, usually 3–7. That is a budget for words, not for elements. Build a full, structured screen in quiet greys, with real words only on what the story is about and placeholder lines for the rest. Fit every control's text before it moves. Mark what the cursor touches, and measure where it lands — never hard-code a position that a layout change will break.

### 6. Choreograph

Animate the relationship, not just the object: a new row carries the rows below it; a surface that resizes never stretches its text; a card that moves keeps its contents with it. Keep what appears mounted and toggle it, so exits animate instead of popping. Beats overlap, groups stagger, the payoff holds, and the loop ends where it began — or resets with a visible cause, never a silent jump.

### 7. Rehearse

Set the poster frame first: most people see only that frame (a thumbnail, reduced motion, a screenshot), so it must be the beat that tells the story on its own, never one caught mid-change, with the result left on screen rather than tidied away. Then watch the whole loop, not just a still: step through every press, menu, morph, and the loop seam, at the shown width and at phone width. Read every frame, fix the largest visible fault first (framing, then hierarchy, then motion, then polish), and re-check. Then hold it next to the closest reference and ask: what does the eye land on first, and is it the result? Is one window, tile, or device clearly leading? Any "no" is the largest fault. Finish with a short handover note beside the component: the reference you started from, what you changed, and what you did not check.

## Framing rules

- One gutter, a full one or well past it; only filler bleeds off an edge.
- What opens stays in frame; windows keep their shape.
- The page is the ground: no plate under a hero on a white or dark page, and no window whole with air on four sides.
- The window or phone fills at least two thirds of the stage and runs off an edge where the story needs it; a phone in a column is a redesign at the column's width, not a squeeze.
- No dead corners, no empty bands, no cut controls, no shadows that belong to nothing.
- A satellite — a smaller second object, a receipt, a phone, or a detail card straddling the hero's edge — is allowed one per composition, and it must earn its place by carrying part of the story.

## Motion rules

- The cursor moves like a hand: shallow arcs timed by distance, with presses you can see. One cursor style for a whole site.
- The cursor changes shape as it crosses into an element, the way a real one would: an I-beam over search, a hand over a button, a grip while dragging.
- Nothing swaps in place when it should move; nothing pops when it should arrive. A value that changes rolls only the digits that changed.
- Long holds and resets with no cause are faults, not pauses. A loop that ends somewhere other than where it began needs a visible reason to return.
- A selection is only ever under the I-beam; a drag keeps its grab offset and snaps to a slot that is visible before the drop.

## Still-frame craft

- Restraint: real words only where the story is; filler belongs at the edges, never where the eye lands.
- Type and spacing: one hierarchy, generous insets, rows spread to fill a pane rather than clustered at the top. An empty corner or a void under a list reads as unfinished, not calm.
- Chrome and devices: never draw a window, device, or bubble by hand when the product's real geometry is available. A status bar or home indicator drawn by hand is a fault; the device frame supplies both.
- Icons and logos: no stock sparkles, no purple glow, no letter in a coloured square standing in for a logo. Use the product's real icons, or plain shapes that claim nothing.
- Colour: one lit colour at most in a dark frame; the accent carries the story, never the decoration.

## Rehearsal checklist

Before handing over, answer every line honestly:

- [ ] The poster frame tells the story alone, with the result on screen.
- [ ] The eye lands first on the result, and one object clearly leads.
- [ ] No more than 7 real strings, and none of them is filler pretending to be content.
- [ ] Nothing is cut, nothing floats with air on four sides, no dead corners.
- [ ] Every motion has a cause; the loop seam is invisible or visibly caused.
- [ ] The work reads as the brief's product, not the reference's.
- [ ] Nothing in the picture claims a feature, integration, or result that does not exist.
- [ ] No other product's logo, icon, or identity appears, except as a clearly labelled reference the brief asked for.

## Worked sketch: a fictional task board

One interaction, one size, one payoff. In a fictional task board (no real product, no real account), a task card is dragged to the Done column: the card lifts, the other cards make room, the progress bar rolls up by one task, and the payoff frame holds on the new completion count. Real words only on the moved task and the progress total; placeholder lines for the rest of the board. The board fills the stage and runs off one edge; no plate behind it. The loop returns to the pre-move state with the board visibly refreshing — the cause for the reset — rather than jumping. This sketch is a design for a marketing illustration of a made-up product; it is not evidence that any feature behind it is live.

## State

Draft pending representative validation. This skill has not yet been exercised on a real marketing page, feature card, or hero. Promote it only after one such exercise, and revise it from the failures that exercise surfaces.
