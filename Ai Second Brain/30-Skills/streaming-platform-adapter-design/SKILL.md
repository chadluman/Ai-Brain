---
name: streaming-platform-adapter-design
description: Ingest live events from a streaming platform through its authorized API only, normalizing them into one internal event shape, so adding a platform does not rewrite alerts, overlays, or dashboards. Use when a product reads chat, follows, subscriptions, donations, or stream status from a platform the user authorized; do not use for scraping, screen capture, or unauthenticated polling of a platform, which this skill forbids.
---

# Streaming Platform Adapter Design

## Outcome

Produce one adapter per platform that turns that platform's authorized events into one internal event shape, with deduplication, reconnection, and per-platform health visible, so alerts, overlays, and dashboards consume events, not platform APIs.

Use [External API Integration](../external-api-integration/SKILL.md) for general third-party adapter discipline. Use this skill for the streaming-specific parts: authorization scopes, live-event transports, and normalization across platforms whose event models differ.

## Required Inputs

- The platforms in scope, and for each, the exact events needed: chat, follow, subscription, donation or cheer, raid, stream online and offline, and viewer counts.
- The authorization model per platform: who authorizes, which scopes each event requires, and what happens when a scope is missing or revoked.
- The transport per platform: webhook or event subscription, persistent WebSocket, or polling, and the platform's rate limits, quotas, and subscription lifecycle.
- The internal event shape: provider, event type, actor, target, timestamp, and a provider event id, agreed before the first adapter is built.
- The failure policy: what the product shows when a platform disconnects, and how it recovers without duplicating alerts.

If a platform offers no authorized API for an event, do not build a workaround that scrapes its pages, captures its rendered output, or uses another user's credentials. Record the event as unavailable for that platform.

## Workflow

1. Build one adapter per platform behind one internal interface. The adapter owns authentication, transport, subscription management, and translation to the internal shape. Nothing downstream imports a platform SDK or parses a platform payload directly.
2. Request only the scopes each event actually needs, and explain each scope to the user at authorization time. A scope that is never used is a trust and policy risk, and a missing scope must produce a clear re-authorization path, not a silent gap in events. See [OAuth and OIDC Integration Security](../oauth-oidc-integration-security/SKILL.md).
3. Store tokens server-side, encrypted, with refresh handling and expiry tracking. User access tokens are short-lived on most platforms; an adapter that cannot refresh, detect expiry, and re-authenticate cleanly will silently stop receiving events.
4. Choose the transport deliberately, per platform:
   - Webhook or event subscription where the platform supports it, with signature verification and a timestamp window for replay protection.
   - Persistent WebSocket where the product runs locally or cannot receive public webhooks, with heartbeat, reconnect with backoff, and resubscription on reconnect.
   - Polling only as a fallback, with a quota budget, a poll interval that respects rate limits, and a stated accuracy limit. Polling is not a substitute for an event subscription the platform offers.
5. Normalize at the adapter boundary. Map each platform's event to the internal shape, and keep platform-specific fields in a separate, clearly marked extension, never as fields downstream code must special-case. A follow, a subscription, and a donation are different internal types even when one platform reports them together.
6. Deduplicate by provider event id. Live-event delivery is at-least-once on the platforms that matter: the same event can arrive twice, over two transports, or after a reconnect. Downstream alerts must never fire twice for one provider event.
7. Handle the live lifecycle explicitly: subscription creation, renewal, and revocation; token revocation by the user; platform outages; and rate-limit responses. Each adapter reports its own health (connected, degraded, disconnected, unauthorized) so the product can show it instead of presenting silence as "nothing happened."
8. Test without a production stream: use the platform's test, mock, or event-simulation tooling where it exists, and otherwise use recorded, anonymized payloads in an isolated environment. Never test against a real creator's live audience without that creator's authorization.

## Safety and Permission Boundaries

- Never read, send, or act on a platform account without that account owner's authorization, with the exact scopes the action requires. An adapter that reads chat is not authorized to send chat, moderate, or spend channel points.
- Never store stream keys, OAuth secrets, or tokens in client code, overlay URLs, logs, or exports. Tokens belong server-side, or in a local store the user controls, never in a page a broadcaster shares.
- Platform terms and developer policies are part of the design input, not an afterthought. A feature that violates a platform's terms is not a feature, even if the API technically allows it.
- A new platform SDK, adapter library, or event library still requires the root security-review gate at its exact version. This skill approves no provider or package.

## Outputs and Evidence

- An internal event schema, with one adapter per platform translating to it.
- Per-platform authorization, scope, transport, rate-limit, and subscription-lifecycle notes.
- A deduplication, reconnection, and health-reporting design, with the user-visible state for each failure mode.
- Tests or a test report using simulated or recorded events, covering duplicate delivery, reconnect, token expiry, scope loss, and revocation.
