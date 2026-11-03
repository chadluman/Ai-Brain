---
name: discord-server-design
description: Design a Discord server's channels, roles, permissions, and native moderation so a bot is only added where Discord itself cannot do the job. Use when setting up or restructuring a Discord server, a community, or a support space, or when deciding what a bot should not need to do. Do not use for bot code, API transport, OAuth2, or bot operations — those belong to discord-app-integration and discord-bot-operations.
---

# Discord Server Design

## Outcome

A server whose layout, roles, and native moderation already do most of the work, so any bot added later is small, least-privileged, and easy to explain. A new member can find the right channel, a moderator can act without a custom tool, and nothing in the layout depends on a bot staying online.

## Supporting skills

Load only what the gap requires:

- [Content Moderation Operations](../content-moderation-operations/SKILL.md) for policy, reporting, review, enforcement, and appeals beyond what Discord's settings implement.
- [Discord App Integration](../discord-app-integration/SKILL.md) when the design concludes a bot, webhook, or interaction is actually needed.
- [Discord Bot Operations](../discord-bot-operations/SKILL.md) for running that bot safely once it exists.

## Native-first rule

Decide in this order, and stop at the first step that works:

1. A Discord setting (verification level, channel permission, slow mode, AutoMod rule, forum channel, onboarding).
2. A Discord feature with no code (announcement channel, scheduled event, native poll).
3. A one-way incoming webhook for posting alerts into one channel.
4. A bot — only for what steps 1–3 cannot do, such as graduated warnings with case history, a ticket transcript, or a custom role flow.

Every bot added is a secret to protect, a permission to audit, and a process that can go down. A layout that only works while a bot is running is a fragile layout.

## Channels

Servers are organised into channels grouped under categories. Choose the channel type by the shape of the conversation, not by habit:

- **Text:** persistent chat with history, replies, pins, and reactions. The default for discussion.
- **Voice:** live voice and video, screen share, and Go Live. Set user limits deliberately; do not leave every voice channel unlimited by default.
- **Announcement:** a text channel whose messages can be published and followed into other servers. Use it for release notes and status, not for discussion that belongs elsewhere. A channel can follow up to 10 announcement channels.
- **Forum:** posts are threads, with tags for state or topic. This is the natural native shape for Q&A, feedback, and lightweight ticketing before any bot exists. Do not build a ticket bot on top of plain text channels when a forum channel already gives you threads, tags, and search.
- **Media:** like a forum, but for media posts; treat it as still evolving and check Discord's current docs before designing around undocumented behaviour.
- **Stage:** a speaker-and-audience model for AMAs, town halls, and announcements. Audience and video-seat caps vary by boost level.

**Threads** branch off a channel or a message. They inherit the parent channel's permission overwrites, cap at 1,000 members, and archive by default after 3 days. Use threads for anything that should not dominate the main channel: a support question, a side discussion, a ticket.

**Direct messages** are not a server design tool. Group DMs cap at 10 users, and bots cannot have friends or join group DMs at all. Design support flows in channels or threads, not in DMs a bot cannot reliably enter.

## Roles and permissions

Roles are the permission unit. A member's effective permissions are the union of their roles, modified by channel overwrites (allow or deny per role or per member).

- **Hierarchy matters, not just the permission bit.** A member or bot can only manage roles and members below its own highest role. Place bot and moderator roles deliberately in the hierarchy, and test the placement with a non-admin account before going live.
- **Administrator is the exception.** It bypasses channel overwrites and effectively grants everything else. Never grant it casually to a bot or a human moderator. If a bot's install guide asks for Administrator "just in case," treat that as a reason to choose a different bot or to grant only the permissions it can justify.
- **@everyone is the base role** every member has. Restricting @everyone is the lever for a locked-down server, with narrower roles granting more. Start restrictive, then grant — the reverse order leaks channels.
- **One role per job.** A role named for its purpose ("Moderator," "Ticket Support," "Announcements") is auditable; a role that accumulates unrelated permissions is not. Review roles on a schedule, and remove roles that no longer map to a person or a function.

## Native moderation

- **Verification levels:** None (no restriction), Low (verified email), Medium (verified email plus an account at least 5 minutes old), High (plus at least 10 minutes of server membership), Highest (verified phone number). Raise the level when raids or spam start, and lower it again when the wave passes — a permanently maximal level also locks out legitimate new members.
- **AutoMod:** built-in keyword and pattern filtering, a managed commonly-flagged-words preset, and spam and mention-raid presets, with actions to block, alert moderators, or time out. It lives in Server Settings for Community servers. Re-check the current preset list in Safety Setup before documenting it, because presets change.
- **Timeouts, kicks, bans:** a timeout temporarily blocks sending, reacting, and joining voice; a kick removes a member who can be re-invited; a ban removes and blocks rejoining. Only members with the relevant permission can apply or lift them.
- **Explicit content filter:** scan nothing, scan members without a role, or scan all members. Age-restricted channels are exempt by design — do not rely on the filter inside them.
- **Server-wide 2FA:** requires moderators and admins to have two-factor authentication to take moderation actions, and the owner must have it to enable the setting. Enable it for any server with more than one moderator.
- **Audit log:** entries remain 45 days and viewing requires View Audit Log permission. The native log expires and is not an export or archive — if a durable moderation record matters, that is a bot's job (see discord-bot-operations), not something to assume the audit log provides.

## Community, discovery, and gating

Server types, in increasing openness:

- **Friend:** invite-only, small groups.
- **Community:** invite-only, plus Insights, Raid Protection, Rules, and Onboarding (rules acceptance and role or channel choices for new members).
- **Discoverable:** Community plus eligibility — including 1,000 or more members, activity, safety checks, and moderator two-factor authentication — listed in Server Discovery. Discovery is opt-in and gated, not automatic. Turning off Community also turns off Discoverability.

Do not promise discoverability as a growth lever for a new server. Design onboarding for the server you actually have, and treat discovery as a later milestone with its own checklist.

## Caps that constrain layout

These figures are from Discord's official support caps page, read 2026-11-03. Re-check them before publishing, because Discord's own pages currently disagree on file-upload limits (see discord-app-integration).

- 500 channels per server, counting text, voice, and categories combined.
- 50 categories per server, with at most 50 channels per category.
- 250 roles per server, regardless of boost level. Role names cap at 100 characters.
- 25,000,000 members per server.
- 999 unique invite codes per server.
- A user can join 100 servers, or 200 with Nitro.
- Stage audience up to 10,000 without streaming or video; video seats 50, 50, 150, then 300 across boost levels.
- Emoji, sticker, and soundboard slots grow with boost level (50 to 250, 5 to 60, and 8 to 48 respectively). Boost thresholds are 2, 7, and 14 boosts for Levels 1, 2, and 3.

Design inside these caps from the start. A layout that needs a 501st channel or a 251st role is not a layout problem — it is a sign the server needs fewer, better channels and roles.

## Mobile and desktop caveats

The desktop app is essentially the web client; mobile is a separate touch client with the same servers and channels but different navigation and smaller targets, and its screen-reader coverage has historically lagged desktop. Do not assume a channel design, a button flow, or an admin setting is equally usable on mobile. Keep button labels short, avoid reaction-only flows, and provide a slash-command alternative to any button-only flow. Do not claim feature parity or a specific accessibility conformance level for Discord — neither was verified on an official page in the research behind this skill.

## Design checklist

Before handing over a server design, answer every line:

- [ ] Every channel has a purpose a new member can tell from its name and topic, and no channel exists "just in case."
- [ ] Forum channels are used for Q&A, feedback, and lightweight ticketing before any ticket bot is proposed.
- [ ] @everyone is restrictive by default; narrower roles grant more, and no role grants Administrator without a written justification.
- [ ] Bot and moderator roles sit deliberately in the hierarchy, tested with a non-admin account.
- [ ] Verification level, AutoMod, explicit content filter, and server-wide 2FA are set to match the server's current threat level, not its maximum.
- [ ] Moderators know the audit log expires in 45 days and where the durable record lives, if one is needed.
- [ ] Community and Discovery are only claimed when their eligibility is actually met.
- [ ] The layout fits the caps: 500 channels, 50 categories, 250 roles.
- [ ] Anything a bot does is listed separately, with the native alternative it beat and why.

## State

Draft pending representative validation. This skill has not yet been exercised on a real server setup or restructure. Promote it only after one such exercise, and revise it from the failures that exercise surfaces.
