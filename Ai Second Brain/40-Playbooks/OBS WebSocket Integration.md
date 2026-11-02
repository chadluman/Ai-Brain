---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [playbook, livestream, obs, websocket, desktop, security]
sources:
  - https://docs.streamer.bot/api/websocket/guide/client
---

# OBS WebSocket Integration

## Scope and Fit

This playbook covers controlling a local OBS Studio instance from a desktop app or local bridge using obs-websocket, which is built into OBS 28 and later. It is StreamControl's control plane: scene, source, filter, audio, stream, and recording control, plus events for scene changes.

Use obs-websocket when the control surface runs on the streamer's machine, or talks to a local bridge on that machine. Do not use it as a cloud-to-OBS protocol, and do not expose it directly to web clients.

Verify the current protocol, opcodes, and authentication on the official obs-websocket repository and obsproject.com before implementing. The 2026-11-02 research run used a DeepWiki mirror of the repo, not obsproject.com itself, so auth and opcode details in this playbook are flagged for re-verification, not treated as primary-source verified.

## Trust Boundary

```text
streamer (local) -> desktop app or local bridge -> obs-websocket (localhost:4455, password)
web client -> SaaS backend -> NEVER directly to obs-websocket
```

Any holder of the obs-websocket password controls OBS: scenes, sources, stream start and stop, and recording. There is no built-in multi-user permission model. A leaked password is a full-control leak, not a read-only leak.

## Prerequisites and Approval Boundaries

- Apply the vault's streaming-platform-adapter-design and livestream-overlay-transport-design skills for transport, deduplication, and overlay separation.
- Accept an ADR covering the local bridge design, reconnect and queueing behaviour, scene-change debouncing, and the remote-access plan (VPN or TLS tunnel only, if remote access is needed at all).
- Security-review the exact websocket client library, bridge code, and any tunnel or VPN configuration before use.
- Enabling the websocket server, setting or rotating its password, and any remote-access configuration are R3. Production stream control, stream start and stop, and recording control are R3 in a live context.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `OBS_WEBSOCKET_HOST` | Local config only | Usually `localhost`; never a public host in the default design |
| `OBS_WEBSOCKET_PORT` | Local config only | Default 4455 |
| `OBS_WEBSOCKET_PASSWORD` | Local secret, never in client code or logs | Authentication for the websocket server |
| `OBS_BRIDGE_TOKEN` | Local secret, if the bridge exposes an API | Authentication between the desktop app and the local bridge, distinct from the OBS password |

In OBS: Tools → WebSocket Server Settings → Enable, set the port and password, and use Show Connect Info to confirm. The client uses the `obswebsocket.json` subprotocol, then Hello (op 0) → Identify (op 1, SHA256 auth) → Request (op 6), Event (op 5), and Batch (op 8), with an event-subscription bitmask.

## Integration Rules

- Proxy every web-client request through the desktop app or local bridge. The browser never connects to port 4455.
- Own reconnect, backoff, and queueing in the bridge or app code. A websocket client library does not supply a product-grade reconnect policy on its own.
- Debounce scene changes. Do not call OBS on every UI render.
- Use the requests the product actually needs first: `GetVersion`, `SetCurrentProgramScene`, `SetInputMute`, `GetStreamStatus`, `TriggerHotkeyByName`, `CreateInput`, `StartStream`, and `StopStream`. Add further requests only with a reviewed need.
- Subscribe only to the events the product consumes, via the event-subscription bitmask. Do not subscribe to everything and filter later.
- Handle the version 4 versus 5 protocol break explicitly: check `GetVersion` and fail clearly on an unsupported protocol version, rather than sending version 5 requests to a version 4 server.
- Log scene changes and stream state transitions without logging the password, tokens, or scene contents that are private to the streamer.

## Verification

Before any live use, verify in an isolated OBS instance: connect with the password, read version and stream status, change program scene, mute and unmute an input, receive a scene-change event, survive a disconnect and reconnect, and confirm that a wrong password is rejected. Test the bridge's behaviour when OBS is not running: it must report unavailable, not queue an unbounded backlog of scene changes.

## Rollback and Recovery

If the bridge misbehaves live, stop the bridge, not OBS. The streamer's OBS remains usable by hand. Rotate the websocket password if it was ever exposed in logs, screenshots, or a shared configuration, and re-verify the local-only binding after any network change.
