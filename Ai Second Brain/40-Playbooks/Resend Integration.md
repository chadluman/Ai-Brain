---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [playbook, backend, email, notifications, security]
sources: []
---

# Resend Integration

## Scope and Fit

This playbook covers Resend for transactional email — auth, billing, and alert emails — with React Email templates, on a Next.js stack. It is the concrete email choice in the catalog; the vault's email-deliverability-operations skill covers deliverability generically.

Use Resend when the app needs transactional email with a clean Next.js developer experience. Do not use it for marketing campaigns at scale: it has no drag-and-drop campaign builder and no inbound parsing in the research run's secondary accounts.

## Trust Boundary

```text
server (Route Handler or Server Action) -> Resend API (key) -> recipient
untrusted client -> application authentication + authorization -> server only
```

The API key is a server secret. Email sending from the client is a spam and abuse hole, not a shortcut.

## Prerequisites and Approval Boundaries

- Apply the vault's email-deliverability-operations skill for domain authentication, bounce handling, and reputation.
- Accept an ADR covering which emails the app sends, from which domain, with what templates, and with what volume and burst policy (see cost shape below).
- Security-review the exact SDK version, template rendering, and unsubscribe and bounce handling before use.
- Domain verification, production sending, and any change to a billing or auth email template are R3.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `RESEND_API_KEY` | Server secret only | Resend API authentication |
| `RESEND_FROM_DOMAIN` | Server config | Verified sending domain |
| `RESEND_FROM_ADDRESS` | Server config | From address on the verified domain |

Verify the sending domain's DNS: SPF, DKIM, and DMARC. An unverified or misconfigured domain is a deliverability and spoofing risk, not a minor setup detail.

## Integration Rules

- Send only from Route Handlers or Server Actions, never from the client, and only after the application's own authentication and authorization checks.
- Build templates with React Email, and keep every template's text and HTML versions in sync. A template that exists only as HTML is an accessibility and deliverability gap.
- Handle bounces, complaints, and unsubscribes explicitly, and suppress addresses that bounce repeatedly. Continuing to send to bouncing addresses damages the domain's reputation for every other email.
- Respect the free-tier daily cap in planning: the research run's secondary account gives 100 sends per day on free, so a burst of 3,000 emails in one day is not possible on free, even though the monthly total is 3,000. Plan bursts against the daily cap, not the monthly total.
- Log sends by template and recipient domain, without logging email bodies that contain personal data the app does not need to retain.
- Do not use Resend for multi-channel notifications (email plus SMS plus push plus in-app) with preferences and digests. That is Novu's job in the catalog, and only once multi-channel complexity actually exists — Resend alone suffices for email-only.

## Cost Shape

Secondary, corroborated in the 2026-11-02 research run, not vendor-verified there: Free 3,000 emails per month, 100 per day, 1 domain; Pro $20 per month for 50,000, with $0.90 per 1,000 overage. Check resend.com/pricing before budgeting.

## Verification

Before production use, verify in an isolated project: a send from a verified domain arrives with correct SPF, DKIM, and DMARC alignment; a template renders correctly in text and HTML; a bounce is recorded and the address suppressed; a client-side send attempt is rejected; and a burst above the daily cap is handled gracefully rather than silently dropped.

## Rollback and Recovery

If Resend sending breaks, pause non-critical emails and surface the failure to the affected flow (for example, a password reset that cannot be sent must say so, not pretend it succeeded). If the API key is exposed, rotate it immediately and re-verify the domain configuration.
