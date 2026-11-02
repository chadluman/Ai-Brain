---
name: livestream-overlay-transport-design
description: Deliver live state to a browser source in OBS or a similar broadcaster, with a token-scoped overlay URL, fast reconnect, and no secrets in the page, so an overlay stays live through network drops and never leaks another streamer's data. Use when a web app renders alerts, goals, chat, or counters into a broadcast; do not use for controlling OBS itself, which is a separate local integration.
---

# Livestream Overlay Transport Design

## Outcome

Produce an overlay page that renders live state in a broadcaster, reconnects on its own, resynchronizes after a drop, and can be revoked without touching the streamer's account, so a network interruption is a brief gap, not a broken broadcast element.

Use [Realtime Transport Selection](../realtime-transport-selection/SKILL.md) to choose the transport. Use this skill for the overlay-specific parts: the browser-source page, its token, and its behavior when it is hidden, disconnected, or stale.

## Required Inputs

- The overlay's content and layout: what it shows, at what resolution, and how it behaves with no data, with stale data, and with a flood of events.
- The transport and its latency budget: how quickly an event must reach the screen for alerts and counters to feel live.
- The token model: who may view this overlay, how the token is issued and revoked, and what the token may and may not do.
- The broadcaster environment: OBS browser source or an equivalent, its browser version, hardware acceleration, and whether the source is visible, hidden, or in a scene that is not live.

If there is no token model, do not ship the overlay. A public, unguessable URL is not access control, and a user session cookie in a browser source is not an overlay token.

## Workflow

1. Separate the overlay renderer from the control dashboard. The overlay is a read-only, transparent, low-chrome page with no login UI, no navigation, and no controls that could be clicked on air. All control lives in the dashboard.
2. Issue one revocable, read-only overlay token per streamer, scoped to that streamer's overlay data only. The token must be rotatable and revocable without changing the streamer's account password or session, and it must never be a session token, an API key, or a platform OAuth token. Record that a token in a browser-source URL is visible to anyone who can see the broadcaster's scene collection, so its scope must be safe to expose in that setting.
3. Choose a transport that pushes, and plan for its failure. WebSocket or server-sent events are the usual choices; polling is a fallback, not the design. Add a heartbeat so a silent disconnect is detected, reconnect with backoff, and on reconnect send the full current state, not only new deltas, so the overlay cannot stay stuck on pre-drop data.
4. Decide what happens during a disconnect and during a flood. During a disconnect, show the last known state with a stale indicator for the streamer (not the audience, where a stale indicator would itself be broadcast), or hide cleanly, according to the overlay's purpose. During a flood, coalesce and drop stale intermediate states, keeping the latest, rather than queueing minutes of alerts behind a live broadcast.
5. Design for the broadcaster's rendering reality: match the stream's frame rate where it matters, avoid layout thrash and heavy animation on every event, keep fonts and assets self-contained or cached, and test at the actual overlay resolution in OBS, not only in a desktop browser tab. A hidden browser source may be throttled or paused by the broadcaster; the overlay must recover when it becomes visible again.
6. Keep the overlay page free of secrets and other users' data. It receives only the data for its token's streamer, over an encrypted connection, and it logs nothing that would expose that data to a third party.
7. Test the failure matrix: disconnect and reconnect, token revocation mid-stream, token rotation, a hidden source becoming visible, a flood of events, and a page reload mid-broadcast. Each case must end in a defined, non-leaking state.

## Safety and Permission Boundaries

- Never embed a session token, platform token, or provider secret in an overlay URL, page source, or scene collection export. If a token leaks, revoke and rotate it; do not rely on obscurity.
- Never render one streamer's data to another streamer's overlay. The token-to-streamer binding is checked on the server for every connection, not inferred from a URL parameter the client supplies.
- Overlay content is broadcast content. Treat chat, usernames, and donation messages as untrusted input: escape or sanitize before rendering, and respect the streamer's moderation and filtering settings before anything reaches the screen.
- A new realtime library or broadcaster integration still requires the root security-review gate at its exact version. This skill approves no provider or package.

## Outputs and Evidence

- An overlay token model: scope, issuance, rotation, and revocation, with the blast radius if a token leaks.
- A transport, heartbeat, reconnect, and resynchronization design, with disconnect and flood behavior stated.
- A rendering specification: resolution, frame rate, transparency, and behavior when hidden or stale.
- Tests or a test report covering disconnect, reconnect, revocation, rotation, hidden-source recovery, and flood handling.
