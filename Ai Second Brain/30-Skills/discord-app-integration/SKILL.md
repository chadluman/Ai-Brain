---
name: discord-app-integration
description: Choose and implement the right Discord transport — a Gateway bot, an HTTP interactions app, or an incoming webhook — with correct auth, scopes, and intents. Use when building or integrating a Discord app, bot, or webhook, or when deciding how a web app connects to a Discord server. Do not use for server layout or moderation policy (discord-server-design) or for running a bot safely at scale (discord-bot-operations).
---

# Discord App Integration

## Outcome

An app that reaches Discord through the smallest transport that does its job, with the narrowest scopes and intents it needs, and no user-token workaround anywhere in the design. A developer reading this skill can answer, before writing code: Gateway bot, HTTP interactions app, or webhook — and why.

## Supporting skills

Load only what the gap requires:

- [Discord Server Design](../discord-server-design/SKILL.md) for the server, roles, and native moderation the app will live in.
- [Discord Bot Operations](../discord-bot-operations/SKILL.md) for secrets, rate limits, hosting, and sharding once the app exists.
- [External API Integration](../external-api-integration/SKILL.md) for bounded third-party adapter patterns in general.
- [Webhook Integration Design](../webhook-integration-design/SKILL.md) for authenticated, idempotent, recoverable webhook delivery in general — Discord specifics here take precedence where they differ.

## The three transports

Discord is two APIs in one product, plus a third path:

| Transport | What it is | Receives | Sends | Use it for |
|---|---|---|---|---|
| **Gateway bot** | A persistent WebSocket (`wss://gateway.discord.gg`) plus REST | Real-time events: messages, reactions, member joins, presence, threads, interactions | Anything its permissions allow, via REST | Event-driven work: moderation, welcomes, role flows, anything that must react to something happening |
| **HTTP interactions app** | An HTTPS endpoint Discord calls, with Ed25519 signature verification | Interactions only: slash commands, buttons, select menus, modals, context menus | Responses, deferred responses, and follow-ups on those interactions | Commands on serverless or edge hosting, with no persistent connection |
| **Incoming webhook** | A per-channel secret URL | Nothing | One message at a time into one channel, with an optional per-message name and avatar override | CI, deploy, and status alerts — send-only notifications |

The HTTP path and the Gateway path are mutually exclusive for interactions: an interaction arrives either as a Gateway event or as a webhook to the endpoint, never both. The HTTP path can never deliver raw message events, so prefix commands are impossible on it. A Gateway bot that is not running receives nothing — there is no message queue or polling fallback.

Choose in this order: webhook if posting is all you need; HTTP interactions if commands and components are all you need; a Gateway bot only if you must react to events.

## Creating an app and adding it to a server

1. Developer Portal → New Application → name it. The app gets an Application ID (client ID), a client secret, and a public key for interaction signature verification.
2. Bot tab → Add Bot. The bot page is where the token and privileged-intent toggles live.
3. Copy or reset the **bot token**. It is shown once or on reset, and it is the bot's password. It never goes into client-side code, a screenshot, or a public repo — see discord-bot-operations for handling.
4. Installation / OAuth2 → URL Generator → scopes `bot` and `applications.commands` → tick **only** the permissions the bot needs → open the generated URL, pick a server, Authorize. The inviter needs Manage Server in that server.
5. For HTTP interactions: set the Interactions Endpoint URL on General Information and implement Ed25519 verification and PING handling before going live.

## OAuth2 scopes and flows

Flows, from Discord's official OAuth2 docs: authorization code grant (standard user login, with refresh tokens), implicit grant (token in the URI fragment, no refresh token, less secure), client credentials grant (bot-owner testing), plus special bot and webhook flows. Token URL is `https://discord.com/api/oauth2/token`; authorize URL is `https://discord.com/oauth2/authorize`; a revocation endpoint exists. Use `state` for CSRF protection even though it is recommended rather than required. Token endpoints accept only form-encoded bodies, not JSON.

Key scopes:

- `bot` — puts the bot in the user's selected guild. This is the bot-install flow.
- `applications.commands` — adds commands to a guild. Included by default with `bot`.
- `identify` and `email` — read basic profile and email via `/users/@me`.
- `guilds` — a basic list of the user's guilds. `guilds.join` — adds a user to a guild; sensitive and abuse-prone, avoid unless building a verified join flow.
- `guilds.members.read` — the user's own member info in a guild.
- `webhook.incoming` — generates a webhook returned in the token response.
- `dm_channels.read`, `identify.premium`, and several `rpc.*`, `voice`, and `activities.*` scopes are partner-only or not currently available. Requesting an unapproved scope can error or behave in undocumented ways.

Installation contexts: guild install (0) and user install (1), relevant only when `applications.commands` is in scope, and the app must be configured in the portal for the requested context. Interaction contexts separately include guild (0), bot DM (1), and private channel (2).

**Linking a web app to a server:** use authorization-code OAuth2 with `identify` (plus `guilds` to list servers the user can manage) to prove who the user is and which servers they administer, then use the bot — installed separately via the `bot` scope — to act in the server. A user bearer <redacted> alone does not give the web app the bot's channel powers, and a bot token must never be handed to the browser.

## Intents — the gate that matters most

An app only receives the event families it requests. If you do not request an intent, you do not receive its events. Non-privileged examples: `GUILDS`, `GUILD_MESSAGES`, `GUILD_MESSAGE_REACTIONS`, `DIRECT_MESSAGES`.

The three privileged intents, from Discord's official privileged-intent guide:

| Intent | Bit | Grants |
|---|---|---|
| `GUILD_MEMBERS` | 1 << 1 | Member join, leave, and update events; listing all members |
| `GUILD_PRESENCES` | 1 << 8 | Online and offline status, activities, platform info |
| `MESSAGE_CONTENT` | 1 << 15 | The `content`, `embeds`, `attachments`, `components`, and `poll` fields on messages |

Without `MESSAGE_CONTENT`, an app still receives message-create events, but those fields arrive empty — with exceptions for its own messages, direct messages to it, and messages that mention it. The official guide's recommended migration is prefix commands to slash commands, which need no privileged intent.

**Approval process, current as of the guide's 2026-10-30 update (changed 2026-06-10):**

1. Under **10,000 unique users** who can see the app across all installed servers: toggle intents on in Developer Portal → Bot → Privileged Gateway Intents. No application needed — but only enable what the app actually needs.
2. At or over 10,000 users: Discord notifies the owner in the portal; the owner has **90 days** to apply, describing a specific, compliant use case per intent, data handling and retention, and why interactions cannot replace it. The app keeps working and can keep joining servers while under review.
3. Approved apps must **reapply annually** (a 90-day window after notice; access is removed if they do not, but they may reapply at any time).
4. **App Verification is a separate process** from privileged-intent review. Verification is the gate for growing past 100 servers. Do not conflate the two: the old "100 servers means intent review" rule is obsolete for intents.

**Misconfiguration symptoms:** an intent requested in code but not enabled in the portal, or vice versa, yields a `DisallowedIntents` error. Portal changes need a new Gateway connection — restart after changing them. A single source of truth for intents, shared by code and portal documentation, prevents the most common "my bot stopped seeing messages" failure.

## Interactions

An interaction is delivered when a user uses an application command or a message component. Types: PING (1), APPLICATION_COMMAND (2), MESSAGE_COMPONENT (3), APPLICATION_COMMAND_AUTOCOMPLETE (4), MODAL_SUBMIT (5). Slash commands carry typed options; user commands and message commands carry the resolved target; components carry a `custom_id` plus selected values for selects; modals carry submitted text or file inputs.

Commands can be registered globally (propagates to all installed servers, slower) or per guild (fast, for testing). Command-count limits and option limits are widely reported but were **not** verified on an official page in the research behind this skill — verify before publishing them.

**Response windows — secondary, not officially verified in this research run:** acknowledge within 3 seconds or Discord shows "application did not respond" and the token is invalidated; use a deferred response, then edit or follow up. The interaction token remains usable for follow-ups for 15 minutes. Treat both numbers as widely corroborated but re-checkable, not as official figures. Interaction endpoints are exempt from the bot global rate limit (official rate-limits page).

Components include buttons, string, user, role, mentionable, and channel selects, text inputs in modals, and newer Components V2 elements. A message with the Components V2 flag cannot have that flag removed.

## Embeds and messages

Embed limits are official (message resource, "Embed Limits" table):

- At most 10 embeds per message, including interaction responses.
- Embed title and author name: 256 characters each.
- Embed description: 4,096 characters.
- At most 25 fields; field name 256 characters, field value 1,024 characters.
- Embed footer text: 2,048 characters.
- **All embed text combined, per message: at most 6,000 characters** (title, description, field names and values, footer, and author across all embeds).

Message content caps are official (support caps page): 2,000 characters for free and Basic users, 4,000 with Nitro. Attachments per message are widely reported as 10, but that figure was not in the message-resource excerpt opened in this research run.

## File uploads — a live conflict, handle with care

Discord's own pages currently disagree, and this skill must not pick a winner:

- **Official support caps page, opened 2026-11-03:** base 10 MB, Nitro Basic 50 MB, Nitro 500 MB; server boost Level 1 same as base, Level 2 50 MB for all members, Level 3 100 MB for all members. The effective limit is the higher of the user's personal cap and the server's boost cap, not the sum.
- **October 2026 secondary reporting:** free limit raised from 10 MB to 20 MB, full Nitro up to 1 GB, with an API change dated 2026-09-03 — and the note that Nitro does **not** raise a bot's limit; a bot's limit follows the server's boost tier.

**Documentation rule:** quote the caps-page figures as "official support page, possibly stale" and flag the 20 MB and 1 GB figures as "reported in October 2026 secondary coverage, awaiting an official-page update." Never present 500 MB and 1 GB as simultaneously current. For bots and webhooks, design for the lower bound (10–20 MB per file) and read the attachment size limit on interactions where available rather than hard-coding a number.

## Webhooks, precisely

A channel webhook is a secret URL that posts a message into one channel. Creating one needs Manage Webhooks permission on that channel. It is send-only: it cannot read messages, react to events, or receive components. Treat the URL as a credential — anyone with it can post as that webhook — and rotate or delete it if leaked. Do not confuse a channel webhook with an interaction follow-up, which is also webhook-shaped under the hood but uses the interaction token, not a channel webhook URL.

## Bots, apps, webhooks, and user accounts

| Entity | What it is | Can it do |
|---|---|---|
| **App** | The Developer Portal object: ID, secret, public key, install settings, commands | Own a bot user, webhooks, and interactions; it is not itself a chat participant |
| **Bot user** | The app's automated user, added via the `bot` scope | Join servers, send and read per permissions and intents, use Gateway and REST, hold roles. Cannot accept normal invites, have friends, or join group DMs |
| **Incoming webhook** | A per-channel secret URL | Post messages into one channel only. Cannot read, listen, or respond to components |
| **User account** | A human's account | Everything a human can do — but automating it is forbidden (below) |

**Self-bots are against the rules.** Discord's Community Guidelines, rule 14, effective 2025-09-29: "Do not use self-bots or user-bots. Each account must be associated with a human, not a bot." Document this as a hard prohibition, not a grey area: no user-token scraping, no user-token direct-message automation, no logging in as a user to read a server the bot is not in.

## Libraries

Discord.js (JavaScript and TypeScript, Node) and discord.py (Python) are the two dominant libraries in every hosting and library survey in this research run, at discord.js v14 and discord.py 2.x in secondary sources, both with slash-command support. Others by ecosystem: nextcord and py-cord (Python forks with an interactions focus), interactions.py, JDA, Discord4J, and Javacord (Java and Kotlin), discordgo, disgo, and arikawa (Go), serenity (Rust), and Discord.Net and Disqord (.NET). Libraries generally handle Gateway reconnect, sharding helpers, and REST rate-limit bucketing — but the app owner still owns intent selection, permission scope, and secret handling. A library does not fix an over-privileged invite. Do not present library popularity as an official Discord endorsement; Discord does not endorse a single library.

## What bots cannot do

Document these as hard limits, not bugs:

- Read direct messages they are not part of, read any channel they cannot view, or read message content without `MESSAGE_CONTENT` (subject to the exceptions above).
- Bypass permissions or hierarchy: a bot cannot grant itself a permission it lacks, manage a role at or above its own highest role, edit other users' messages (it can delete with Manage Messages and pin with Pin Messages), or bypass channel overwrites without Administrator.
- Accept normal invites, have friends, or join group DMs.
- Create servers (reported as removed for bots in a single secondary source in this research run — verify before publishing).
- Bulk-delete messages older than 14 days via the bulk endpoint (widely reported, not opened on an official page in this research run).
- Evade rate limits by retrying faster, or use a user token to do any of the above.

## Integration checklist

Before handing over an integration design, answer every line:

- [ ] Transport chosen by need: webhook, HTTP interactions, or Gateway bot — with the reason written down.
- [ ] Scopes are the minimum for the job; `guilds.join` and partner-only scopes are absent unless a reviewed need justifies them.
- [ ] Intents are the minimum for the job; privileged intents are justified in writing, with a retention story, before the 10,000-user threshold is reached.
- [ ] Portal toggles and code requests for intents match exactly, from a single source of truth.
- [ ] Interaction signature verification (Ed25519) is implemented for the HTTP path, and OAuth2 `state` is validated.
- [ ] No bot token reaches the browser, a public repo, a screenshot, or client-side code.
- [ ] Embed and message limits are respected by construction, not by hoping content stays short.
- [ ] File-size handling designs for 10–20 MB and reads the interaction attachment limit where available.
- [ ] No user-token flow exists anywhere in the design.

## State

Draft pending representative validation. This skill has not yet been exercised on a real Discord app, bot, or webhook integration. Promote it only after one such exercise, and revise it from the failures that exercise surfaces.
