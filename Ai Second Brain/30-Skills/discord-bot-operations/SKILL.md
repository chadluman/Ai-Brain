---
name: discord-bot-operations
description: Run a Discord bot reliably and safely at scale without getting rate-limited, banned, or leaked. Use when a Discord bot is already designed and needs hosting, secret handling, rate-limit handling, sharding, logging, or failure runbooks. Do not use for server layout or moderation policy (discord-server-design) or for choosing a transport, scopes, or intents (discord-app-integration).
---

# Discord Bot Operations

## Outcome

A bot that stays up, stays within its permissions, and fails in ways an operator can diagnose and fix — without leaking a secret, burning a rate-limit budget, or taking a server down with it. Reliability here is an operations discipline, not a library feature.

## Supporting skills

Load only what the gap requires:

- [Discord Server Design](../discord-server-design/SKILL.md) for the server, roles, and hierarchy the bot operates in.
- [Discord App Integration](../discord-app-integration/SKILL.md) for transport, scopes, intents, and what the bot is allowed to do in the first place.
- [API Abuse and Resource Controls](../api-abuse-resource-controls/SKILL.md) for bounding API work, cost, and automation in general.
- [Privacy and Data Governance](../privacy-data-governance/SKILL.md) for mapping and minimising personal-data flows and retention.

## Secrets: the one rule that admits no exception

- **Bot token and client secret are secrets.** The public key is public (it verifies interaction signatures); the other two are not. Keep them in environment variables or a secret manager only — never in code, a public repo, a screenshot, client-side code, or a shared document.
- **If leaked, regenerate immediately** in the Developer Portal. The old token stops working on regeneration; that is the fix, not a reason to delay it. Rotate webhook URLs the same way if leaked: delete and recreate, do not keep using a known URL.
- **Bot owners need two-factor authentication** for certain actions and permissions in servers with server-wide two-factor authentication enabled. Set it up before it blocks an incident response.
- **Scan before you ship.** A pre-commit secret scan and a repo scan after any incident are cheap; a leaked token discovered by someone else is not.

## Least privilege, in operations

Least privilege is not a one-time install choice. It is a recurring audit:

- **Administrator never by default.** No bot needs it to post, react, manage roles below its own, or run commands. If a bot stops working without Administrator, find the specific permission it actually needs and grant that one.
- **One role per bot,** placed deliberately in the role hierarchy, with only the permissions its features justify. A bot that can manage roles can only manage roles below its own highest role — test that boundary with a non-admin account.
- **No `guilds.join`, `dm_channels.read`, or user-token flows** without a reviewed, written need. These are the scopes and patterns most likely to fail a review or an abuse report.
- **Permission audits on a schedule.** Every added feature re-opens the question: does this bot still need every permission it has? Remove what it no longer uses, and record the change.

## Rate limits: parse headers, do not hard-code

Rate-limit figures from Discord's official rate-limits page (updated 2026-02-06):

- **Global:** all bots at most **50 requests per second**. Unauthenticated requests are limited per IP. Interaction endpoints are **not** bound to the global limit.
- **Per-route:** buckets keyed by route plus top-level resource (channel, guild, or webhook ID). Headers on most responses: `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `X-RateLimit-Reset` (epoch), `X-RateLimit-Reset-After` (seconds), `X-RateLimit-Bucket`, and on 429 responses `X-RateLimit-Global` and `X-RateLimit-Scope` (`user`, `global`, or `shared`).
- **On 429:** HTTP 429 with a JSON body carrying `retry_after` in seconds (possibly fractional), a global flag, and sometimes a code. The app **must honour `retry_after`** before retrying.
- **Invalid-request ban:** **10,000 invalid requests per 10 minutes** (401, 403, or 429) per IP leads to a temporary API restriction. 429s with a shared scope do not count. Repeatedly retrying a 403 — a permission the bot will never have — is how bots get banned. **Retry only 429 and 5xx responses.**

Per-route numbers often quoted in guides (such as a messages-per-seconds figure per channel) were **not** in the official rate-limits page opened in the research behind this skill. They vary by route. Docs and code should say "parse headers, do not hard-code" rather than listing them as official.

**Operating practices that follow from those rules:**

- Queue work per bucket; do not burst welcomes, role edits, or bulk messages from a single loop.
- Back off, do not restart faster. A crash loop that burns Gateway identifies can lock the bot out until its session budget resets.
- Make handlers idempotent, so a retried action does not double-post, double-assign, or double-ban.
- Log invalid-request rates as a metric, with an alert before they approach the ban threshold — not after.
- Batch and digest alerts to webhooks instead of posting at high frequency to one channel. Use `?wait=true` during development to surface errors, delete dead webhooks, and cap alert frequency.
- **Do not reuse a 404 webhook.** Discord's official guidance is explicit: a webhook that returns 404 is dead, and retrying it forever is a failure mode, not persistence.

## Hosting patterns

- **Always-on VPS or container** for Gateway bots. The process must stay connected; a Gateway bot that is not running receives nothing, and there is no message queue or polling fallback.
- **Serverless or edge** (for example Cloudflare Workers, for which Discord publishes an official tutorial) for HTTP-interactions apps. No persistent socket is needed, which is the whole point of that transport.
- **Hybrid:** a small always-on Gateway worker forwards events to serverless handlers. Use it when event-driven work must scale without keeping all logic in one long-lived process.

Choose hosting by transport, not by fashion. A serverless Gateway bot is not a design; it is a bot that is down between invocations.

## Sharding

Sharding splits a bot's guilds across multiple Gateway connections. The formula reported in secondary sources is `shard_id = (guild_id >> 22) % num_shards`. Treat the numbers below as secondary-corroborated, not officially verified in this research run, except where noted:

- **Mandatory at 2,500 or more guilds; at most 2,500 guilds per shard; about 1,000 guilds per shard recommended.**
- `GET /gateway/bot` returns the recommended shard count and `max_concurrency` (how many shards may identify per 5-second window). The recommended count is not guaranteed stable — read it at startup, do not hard-code it.
- Standard session-start budget: 1,000 Gateway session starts per day. A crash loop that burns identifies can lock the bot out until reset.
- Auto-sharding helpers exist in discord.js (`ShardingManager`) and discord.py (`AutoShardedClient`), but they do not remove the operator's job: monitoring shard health, session starts, and per-shard rate-limit behaviour.

App Verification, required to grow past 100 servers, is a separate process from privileged-intent review — see discord-app-integration. Do not plan sharding and verification as one milestone.

## Logging and retention

- **Keep your own durable moderation and action log.** Discord's native audit log expires in 45 days and is not an export or archive. Log who did what and when for role changes, bans, kicks, and configuration changes, in an append-only store the bot operator controls.
- **Minimise message content in logs.** Do not log every message "for moderation" with no expiry. Prefer in-memory processing where possible, state a retention policy in the app's privacy documentation, and enforce expiry. A privileged-intent application will ask for exactly this retention story — adopt it as a general guardrail even below the review threshold.
- **Prefer ephemeral interaction replies for sensitive output.** Ephemeral replies are visible only to the invoker. They are the default for anything that should not persist in a channel.
- **Do not design cross-server user tracking,** and do not use presence data for surveillance-style features. It will fail an intent review, and it is the wrong product to build.

## Failure runbooks

| Symptom | Likely cause | First action |
|---|---|---|
| `DisallowedIntents` on connect, or prefix commands silently dead | Portal toggle and code request for an intent do not match | Compare portal and code from a single source of truth, fix the mismatch, restart — portal changes need a new Gateway connection |
| Message fields arrive empty | `MESSAGE_CONTENT` not enabled or not requested | Check the intent in both places; migrate prefix commands to slash commands where possible |
| Join events missing | `GUILD_MEMBERS` not enabled or not requested | Same check as above; do not work around it with polling |
| "Application did not respond," dead interaction token | Slow handler without a defer, or a follow-up after the token window | Defer first, work second, edit or follow up within the token window (3-second acknowledgement and 15-minute token figures are secondary-corroborated — re-check them on Discord's official pages) |
| Webhook posts fail with 404, forever | Webhook was deleted | Delete the dead webhook from your configuration; do not retry it |
| Sudden 429s, then API restriction | Ignored `retry_after`, retried 403s, or a burst loop | Stop the loop, honour headers, queue per bucket, check the invalid-request rate before resuming |
| Bot offline after a deploy, no events at all | Process not running, or session budget burned by a crash loop | Check the process and the session-start count; fix the crash before restarting, not after the fifth restart |
| A bot action affects the wrong role or member | Role hierarchy placement wrong | Check the bot role's position against the target role, with a non-admin test account |

## Self-bot prohibition, again, because operations is where it gets violated

Automating a normal user account — a user token in a script, a scraper logged in as a user, a "bot" that is really a human account — is prohibited by Discord's Community Guidelines, rule 14, effective 2025-09-29. It is not a fallback when the bot API lacks a feature, and it is not a testing shortcut. Test with a bot in a test server, with test accounts that are genuinely human-operated, or not at all.

## Operations checklist

Before a bot goes live, and again on every significant change, answer every line:

- [ ] Token and client secret are in a secret manager only; a leak drill (regenerate, rotate, scan) has been rehearsed, not just documented.
- [ ] Permissions are least-privilege, audited, and recorded; Administrator is absent unless justified in writing.
- [ ] Rate-limit handling parses headers, honours `retry_after`, retries only 429 and 5xx, and alerts on invalid-request rate.
- [ ] Hosting matches transport: always-on for Gateway, serverless for HTTP interactions, hybrid only by design.
- [ ] Sharding is planned before 2,500 guilds, with shard count read at startup.
- [ ] A durable action log exists, with a stated retention policy and expiry enforced.
- [ ] Failure runbooks exist for intent mismatch, dead tokens, dead webhooks, 429 bans, and crash loops.
- [ ] No user-token flow exists in production, staging, or test tooling.

## State

Draft pending representative validation. This skill has not yet been exercised on a real running bot. Promote it only after one such exercise, and revise it from the failures that exercise surfaces.
