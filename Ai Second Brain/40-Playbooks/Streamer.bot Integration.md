---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [playbook, livestream, streamer-bot, automation, desktop, obs]
sources:
  - https://docs.streamer.bot/api/websocket/guide/client
---

# Streamer.bot Integration

## Scope and Fit

This playbook covers bridging to Streamer.bot, a free, Windows-first local automation app, so StreamControl can trigger automations a streamer already owns instead of rebuilding them. Streamer.bot connects to a broadcaster (Twitch, YouTube, Kick) and to OBS WebSocket v5, and runs Actions (ordered sub-actions) in response to Triggers (chat commands, channel points, follows, subscriptions, and others), with C# sub-actions for custom logic.

Use Streamer.bot as a local automation bridge. Do not use it as the SaaS backend: action logic lives on the streamer's PC, not in the cloud, so state must be synced to StreamControl through its WebSocket API, not assumed to be shared.

## Trust Boundary

```text
streamer PC -> Streamer.bot -> OBS (localhost:4455) + broadcaster platforms
StreamControl (desktop or local bridge) -> Streamer.bot WebSocket (127.0.0.1:8080) -> DoAction / Subscribe
web client -> SaaS backend -> NEVER directly to Streamer.bot
```

Streamer.bot's WebSocket server is local-only in this design. Exposing it beyond the streamer's machine needs the same VPN or tunnel discipline as obs-websocket, and is not the default.

## Prerequisites and Approval Boundaries

- Apply the OBS WebSocket Integration playbook for the OBS side, and the vault's streaming-platform-adapter-design skill for event normalization.
- Accept an ADR covering which Streamer.bot actions StreamControl may trigger, which events it subscribes to, and what happens when Streamer.bot is not running.
- Security-review the exact client library, action ids, and any C# sub-actions before use.
- Enabling Streamer.bot's WebSocket server, and triggering actions that change scenes, sources, or stream state, are R3 in a live context.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `STREAMERBOT_HOST` | Local config only | Usually `127.0.0.1` |
| `STREAMERBOT_PORT` | Local config only | Default 8080 in the research run's account |
| `STREAMERBOT_ACTION_IDS` | Local config, reviewed list | The only actions StreamControl may trigger, by id or name |

Use the `@streamerbot/client` library: create a client to the local host and port, subscribe to the events the product needs, execute actions with `DoAction`, and list actions with `GetActions`.

## Integration Rules

- Subscribe only to the events the product consumes. Events are not sent unless subscribed, and a wildcard subscription floods in production — the Streamer.bot docs warn against wildcard use in production, so do not use it.
- Trigger actions by reviewed id or name only. Do not let an untrusted client name an arbitrary action.
- Treat Streamer.bot as the owner of its actions. StreamControl triggers and observes; it does not edit a streamer's action logic from the cloud.
- Handle the not-running case clearly: if Streamer.bot is not running, report automation as unavailable, and do not silently fall back to a different automation path that the streamer did not choose.
- Reconcile state on reconnect: after a disconnect, re-subscribe, re-list actions, and re-sync the state StreamControl displays, rather than trusting a stale copy.
- Do not duplicate alerts. If Streamer.bot already fires an alert for an event, StreamControl must not fire a second alert for the same event. The same rule applies to StreamElements and Streamlabs alert boxes in the catalog.

## Verification

Before any live use, verify in an isolated setup: connect to a local Streamer.bot instance, list actions, subscribe to one event, trigger one reviewed action and observe its effect in OBS, disconnect and reconnect with state re-synced, and confirm that Streamer.bot not running is reported as unavailable rather than silently ignored.

## Rollback and Recovery

If the bridge misbehaves live, stop triggering actions and let Streamer.bot's own triggers continue. The streamer's automations remain usable by hand. Remove any action from the reviewed trigger list if it ever produces an unwanted live effect, and re-verify before re-adding it.
