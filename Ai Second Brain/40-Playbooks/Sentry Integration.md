---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [playbook, observability, errors, nextjs, security]
sources:
  - https://docs.sentry.io/platforms/javascript/guides/nextjs/
---

# Sentry Integration

## Scope and Fit

This playbook covers Sentry as the concrete error-tracking default for a Next.js app, covering client, server, and edge errors, plus traces and replays. It is a tool choice, not a new observability theory: the vault's observability-slo-design skill covers SLOs and triage generically, and this playbook covers only how Sentry is wired in.

Use Sentry when the product needs production error signal with release tracking and alerts. Do not use it as a log store, a metrics store, or a substitute for uptime monitoring.

## Trust Boundary

```text
client / server / edge -> Sentry SDK (DSN, public-ish identifier) -> Sentry
Sentry -> alerts (Slack, Linear, or email) -> on-call or founder
application code -> scrubbed error payloads only, never raw user data or secrets
```

The DSN is not a secret in the same sense as an API key, but error payloads can contain secrets and personal data if code is careless. Scrubbing is part of the integration, not an optional extra.

## Prerequisites and Approval Boundaries

- Apply the vault's observability-slo-design skill for what counts as an alert, and its privacy-data-governance skill for what may leave the app.
- Accept an ADR covering volume and cost (see below), sampling rates for traces and replays, alert routing, and data retention.
- Security-review the exact SDK version, source-map upload, and scrubbing configuration before use.
- Creating the Sentry project, uploading source maps, enabling production alerts, and changing sampling or retention are R3.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `NEXT_PUBLIC_SENTRY_DSN` | Public, in client bundle | Client error reporting endpoint |
| `SENTRY_DSN` | Server secret, if kept distinct | Server and edge error reporting |
| `SENTRY_AUTH_TOKEN` | CI secret only | Source-map upload and release tracking |
| `SENTRY_ORG` / `SENTRY_PROJECT` | CI config | Release and source-map targeting |

The Next.js wizard (`@sentry/wizard` for Next.js) generates client, server, and edge instrumentation files and source-map upload. Review every generated file before committing it; a wizard is a starting point, not an approval.

## Integration Rules

- Instrument client, server, and edge. An app that only instruments the client is blind to the server errors that actually break a SaaS.
- Upload source maps in CI so stack traces are readable, and tie every release to a deploy so a new error spike can be traced to a specific release and rolled back.
- Scrub personally identifiable information and secrets from error payloads before they leave the app. Do not rely on Sentry's server-side scrubbing alone for data the app should never have sent.
- Set trace and replay sampling deliberately, and lower it before a traffic spike. Pricing scales with volume, so an unbounded sampling rate is a billing risk, not just a performance risk.
- Route alerts to one channel with a triage rule, and require an owner for every alert. An alert nobody owns is noise, and noise trains people to ignore real errors.
- Do not duplicate logs: decide what goes to Sentry (errors and traces) and what goes to a log store (Axiom or Grafana Cloud in the catalog), and write that retention rule down.

## Cost Shape

Secondary, corroborated in the 2026-11-02 research run, not vendor-verified there: Developer free tier 5,000 errors per month, 10,000 performance units, 1 user; Team $26 per month. Check sentry.io/pricing before budgeting.

## Verification

Before production use, verify in an isolated project: a client error, a server error, and an edge error each appear with a readable stack trace and a release tag; a payload containing a test secret is scrubbed; an alert reaches the configured channel; and a release rollback is possible from the deploy that introduced the error.

## Rollback and Recovery

If Sentry volume spikes, lower sampling first, then fix the underlying error. If a secret or personal data reaches Sentry, rotate the secret, request deletion through Sentry's data controls, and record the incident — do not silently leave the data in place.
