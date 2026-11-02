---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [playbook, livestream, twitch, eventsub, webhook, security]
sources: []
---

# Twitch EventSub Integration

## Scope and Fit

This playbook covers receiving real Twitch platform events — follows, subscriptions, cheers and bits, raids, hype trains, polls, predictions, goals, channel-point redemptions, and stream online and offline — via EventSub, for a SaaS backend or a desktop app.

Use EventSub when the product needs platform events. Do not use IRC as the event feed: IRC is a chat firehose in secondary accounts, but follows are not in IRC, so IRC alone misses follows. Do not use Kraken v5 or Webhooks v1; both are deprecated or removed in secondary accounts.

Verify scopes, rate limits, and EventSub subscription limits on dev.twitch.tv/docs before building. The 2026-11-02 research run used secondary summaries citing dev.twitch.tv, not dev.twitch.tv itself, so scope and limit details here are flagged for re-verification.

## Trust Boundary

```text
Twitch -> EventSub (webhook with HMAC signature, or WebSocket) -> SaaS backend or desktop app
SaaS backend -> verified, deduplicated, ordered event -> entitlement, alert, or overlay record
untrusted client -> application authentication + authorization -> server only
```

EventSub webhooks must be verified, deduplicated, and retried safely. An unverified webhook endpoint is an open door to forged follows, subs, and cheers.

## Prerequisites and Approval Boundaries

- Apply the vault's streaming-platform-adapter-design skill: authorized API only, narrow OAuth scopes, normalization to one internal event shape, deduplication by provider event id, and per-platform health.
- Accept an ADR covering transport choice (webhook for SaaS, WebSocket for desktop), scope list, subscription lifecycle, and retry and dedupe behaviour.
- Security-review the exact OAuth flow, token storage, HMAC verification, and webhook endpoint before use.
- OAuth authorization, token storage, webhook endpoint creation, and production subscription creation are R3.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `TWITCH_CLIENT_ID` | Public-ish client identifier, not a secret | OAuth and Helix client identification |
| `TWITCH_CLIENT_SECRET` | Server secret only | OAuth token exchange |
| `TWITCH_EVENTSUB_SECRET` | Server secret only | HMAC verification of webhook payloads |
| `TWITCH_ACCESS_TOKEN` | Server secret, per broadcaster, scoped | Helix calls and EventSub subscription management |
| `TWITCH_REFRESH_TOKEN` | Server secret, per broadcaster | Token renewal |

Request only the scopes each subscribed topic needs. For example, channel follow events need `moderator:read:followers` in the research run's account. Requesting every scope at once is scope creep and a trust cost with the broadcaster.

## Transport Choice

- **SaaS backend:** EventSub webhooks to a public HTTPS endpoint. Verify the HMAC signature on every request, dedupe by the EventSub message id, and return quickly while processing asynchronously, so Twitch retries do not duplicate work.
- **Desktop app with no public URL:** EventSub WebSocket at `wss://eventsub.wss.twitch.tv/ws`. This is preferred for desktop in the research run's account, because it needs no public endpoint.
- **Helix REST** (`api.twitch.tv/helix/*`) is for queries and actions — streams, users, clips, polls, predictions, channel points, moderation, and chat send — not for the event feed itself.

## Integration Rules

- Normalize every EventSub topic to one internal event shape before it reaches alerts, overlays, or entitlements. Do not let Twitch topic shapes leak into product code.
- Deduplicate by provider event id. EventSub delivery is at-least-once in the vault's adapter skill, so a duplicate follow must not double-fire an alert or double-count revenue.
- Make every handler idempotent and ordered where order matters (for example, a subscription before its follow, or a hype train's levels in sequence).
- Handle retries explicitly: a handler that fails must be safe to re-run, and a handler that succeeds must not be re-run as a new event.
- Track subscription health per broadcaster and per topic. A silently expired or revoked subscription is a silently dead alert feed; surface it.
- Never promise parity across platforms. YouTube chat is polling plus quota, and Kick's API coverage is thinner — both are flagged in the catalog, not assumed equal to Twitch.

## Verification

Before any live use, verify in an isolated test: OAuth with the minimum scopes, one subscription per topic the product uses, a signed webhook or WebSocket event received and verified, a duplicate message id dropped, a failed handler retried without double-firing, and a revoked token surfaced as unhealthy rather than silently ignored.

## Rollback and Recovery

If EventSub delivery breaks, pause alert firing for the affected topics and show the outage to the streamer, rather than firing stale or duplicate alerts. Revoke and re-create subscriptions only through the reviewed flow, and rotate the EventSub secret if it was ever exposed.
