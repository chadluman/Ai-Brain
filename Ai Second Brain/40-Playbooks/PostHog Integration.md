---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [playbook, analytics, experiments, feature-flags, privacy]
sources:
  - https://posthog.com/docs/feature-flags/start-here.md
---

# PostHog Integration

## Scope and Fit

This playbook covers PostHog as the consolidated analytics, feature-flag, experiment, survey, and session-replay choice for a Next.js app: one event model instead of three or four vendors. It is a tool choice, not a new analytics or flag theory: the vault's feature-flag-rollout-design skill covers flag rollout generically, and its analytics and SEO skills cover measurement generically.

Use PostHog when the product needs product analytics, flags, A/B tests, and replay in one SDK, and when its free tier fits (see cost shape). Do not use it as marketing-site analytics alone if privacy positioning matters — Plausible or Umami in the catalog are the cookieless marketing-site choice, and duplicating PostHog events into a second analytics tool is waste.

## Trust Boundary

```text
client / server -> PostHog SDK (project key, public-ish) -> PostHog
PostHog -> flags, experiments, replay, surveys -> product decisions
application code -> scrubbed events only, never raw user data or secrets
```

The project key is not a secret in the same sense as an API key, but events can contain personal data if code is careless. Event design is a privacy decision, not just a tracking decision.

## Prerequisites and Approval Boundaries

- Apply the vault's feature-flag-rollout-design skill for rollout, and its privacy-data-governance skill for what may be tracked.
- Accept an ADR covering the event taxonomy, flag naming, experiment design, replay sampling, and cost (see below).
- Security-review the exact SDK version, event taxonomy, and replay masking configuration before use.
- Enabling production analytics, flags that gate paid features, experiments that change pricing or overlay behaviour, and session replay are R3.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `NEXT_PUBLIC_POSTHOG_KEY` | Public, in client bundle | PostHog project identification |
| `NEXT_PUBLIC_POSTHOG_HOST` | Public config | PostHog host, defaulting to the vendor's cloud |
| `POSTHOG_PERSONAL_API_KEY` | Server secret, if used | Server-side API access, never in the client |

Use the JS snippet or Next.js SDK, autocapture plus custom events, the feature-flag SDK, an experiment as a flag plus a goal metric, and session replay with masking.

## Integration Rules

- Design the event taxonomy before instrumenting: one event per meaningful action, with a stable name and a small set of properties. An event added casually in three places with three names is three events, not one.
- Gate paid features with server-side flag checks, not client-side checks alone. A client-side flag that gates a paid feature is a suggestion, not a gate.
- Run experiments as a flag plus a goal metric, and pre-register the goal and the sample size before launching. An experiment whose goal is chosen after seeing the data is a story, not a test.
- Mask sensitive fields in session replay, and sample replay deliberately. Unmasked replay of a dashboard that shows revenue, emails, or tokens is a data leak.
- Keep marketing-site analytics separate: use Plausible or Umami for the marketing site, and PostHog for the product. Do not duplicate the same events into both.
- Note the vendor-docs limits from the research run: experiments are code-only with no visual editor, and A/B features are not in the open-source release. Do not promise a visual experiment editor to a non-technical user.
- Self-hosting PostHog is heavy in the research run's account. Do not self-host unless there is a specific data-residency or compliance reason, and then budget the operations work explicitly.

## Cost Shape

Verified (vendor docs) in the 2026-11-02 research run: Free 1M events, 1M flag requests, and 5,000 web replays per month; then $0.00005 per event, $0.0001 per flag request, and $0.005 per replay. Check posthog.com pricing before budgeting, as usage beyond free scales with volume.

## Verification

Before production use, verify in an isolated project: a custom event arrives with the designed name and properties; a flag gates a feature server-side and client-side consistently; an experiment reports its goal metric; a replay masks a sensitive field; and an event containing a test secret is scrubbed before it leaves the app.

## Rollback and Recovery

If analytics volume spikes, lower replay sampling and autocapture scope first, then fix the underlying event spam. If personal data reaches PostHog, use its deletion controls, record the incident, and fix the event taxonomy — do not silently leave the data in place. A flag that gates a paid feature can be rolled back by turning the flag off, but only if the server-side check is the real gate.
