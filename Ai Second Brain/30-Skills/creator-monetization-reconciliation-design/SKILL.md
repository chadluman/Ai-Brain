---
name: creator-monetization-reconciliation-design
description: Design how a creator-facing product reconciles money and engagement across Twitch native monetization and external creator platforms (tips, memberships, merch) into one dashboard without double-counting, without promising a single payout feed the platforms do not provide, and without building billing on top of platform revenue it does not control. Use when a product surfaces creator earnings, tips, memberships, or merch alongside platform events; do not use for the product's own subscription billing, which belongs to payments and entitlement design.
---

# Creator Monetization Reconciliation Design

## Outcome

Design a creator earnings view that is honest about where each dollar came from, when it is actually paid out, and what is still only an estimate — so a creator never sees the same tip counted twice, a Twitch sub counted as a Patreon membership, or a pending payout presented as cash in hand.

## Supporting Skills

Load only what the gap requires:

- [Streaming Platform Adapter Design](../streaming-platform-adapter-design/SKILL.md) for authorized platform events, normalization, and deduplication by provider event id.
- [Subscription Entitlement Design](../subscription-entitlement-design/SKILL.md) for granting only on verified paid events, and for the product's own billing, which is separate from creator platform revenue.
- [Payments Ledger Design](../payments-ledger-design/SKILL.md) for ledger discipline, if the product records any money movement of its own.
- [User Data Export Design](../user-data-export-design/SKILL.md) for letting a creator export their own earnings data.

## Principles

- **One event, one record, one source.** Every earnings record carries its source platform, its source event id, and its source amount and currency. A record without a source is a guess, not an earning.
- **Platform revenue is not product billing.** Twitch Bits, Subs, Hype Train, Ads, and Channel Points are governed by Twitch Affiliate and Partner terms, payout thresholds, and revenue shares. The product surfaces them; it does not bill on top of them, and it does not present them as its own revenue.
- **External platforms are separate payouts.** Ko-fi tips, Patreon memberships, Fourthwall merch, Buy Me a Coffee tips, and Gumroad sales each pay out on their own schedule, with their own fees, and through their own processors (often Stripe or PayPal). A single dashboard total that adds them without showing the split is a misleading total.
- **Pending is not paid.** A tip, sub, or merch order is pending until its platform's payout rules say it is paid. Show pending, available, and paid as three different states, never as one number.
- **Reconcile, do not trust the sum.** Scheduled reconciliation compares the product's earnings records against each platform's own reports, and surfaces mismatches for review instead of silently correcting them.

## Design

1. **Source map.** For each platform the product surfaces, record: what events it provides, how they are received (EventSub, webhook, API poll, or manual import), what identifier deduplicates them, what fees apply, and what payout schedule and threshold apply. If any of those are unknown for a platform, mark that platform's figures as unverified, not as complete.
2. **Normalized earning record.** Every record, regardless of source, has: source platform, source event id, creator, amount, currency, fee, net amount, event time, payout state (pending, available, paid, refunded, or disputed), and a link back to the source report. Records are immutable; corrections are new records that reference the original, not edits to it.
3. **Deduplication.** Deduplicate by source event id on ingest, exactly as the adapter skill requires. A Twitch cheer that arrives via EventSub and again via a manual import is one earning, not two. A StreamElements alert and a Twitch event for the same cheer are one earning, not two — the alert is a presentation of the event, not a second event.
4. **No double-counting across layers.** An alert, an overlay, a chat message, and a dashboard row are presentations of one event. Counting each presentation as revenue is the most common reconciliation bug in creator tooling, and it must be designed out, not caught later.
5. **Fee and payout transparency.** Show gross, fee, and net per record, and show each platform's payout schedule and threshold alongside its totals. A creator who sees only a gross total will misunderstand their cash position, and a product that hides fees will be blamed for them.
6. **Reconciliation job.** On a schedule (daily is a reasonable default), compare the product's records against each platform's own reports or APIs, and produce a mismatch list: records the product has that the platform does not, records the platform has that the product does not, and amount differences. A mismatch is a review task, not an automatic correction.
7. **Export.** A creator can export their own earnings records (provided-data scope only, per the user-data-export skill) in a documented JSON or CSV schema, with source, fee, net, and payout state per row, so they can reconcile in their own accounting tool.

## Guardrails

- Do not promise a single monetization feed, a single payout, or parity across platforms. YouTube chat is polling plus quota, Kick's API coverage is thinner, and external platforms pay out separately — say so.
- Do not scrape SullyGnome, TwitchTracker, or Social Blade into a product feed without checking their terms of service. They are manual research tools in the catalog, not data feeds.
- Do not build the product's own subscription billing on top of Bits, Subs, or tips without reading the platform's Affiliate and Partner terms first.
- Do not present estimates (for example, a merch order's expected margin, or a sub's expected payout before the platform's revenue share and threshold) as actual earnings. Label estimates as estimates, with the assumption stated.
- Do not mix the product's own revenue (its subscriptions, via Stripe) with creator platform revenue in one total. They are different money, owed to different people, on different schedules.

## Verification

A design is ready when: every earnings record can be traced to a source event id and a source report; a duplicate event ingested twice produces one record; a refund or dispute changes payout state through a new record, not an edit; a reconciliation run produces a mismatch list rather than a silent correction; and a creator can explain, from the dashboard alone, why a total is what it is, what is pending, and what has actually been paid.
