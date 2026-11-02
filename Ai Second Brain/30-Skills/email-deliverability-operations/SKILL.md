---
name: email-deliverability-operations
description: Design or troubleshoot an outbound-email program across sending identities, SPF, DKIM, DMARC, DNS, consent, suppression, bounce and complaint handling, reputation, and provider migration. Use when transactional, security, or marketing email must reach recipients reliably; do not use for writing an individual message or sending a campaign without authorization.
---

# Email Deliverability Operations

## Outcome

Produce an authenticated, consent-aware email system with separated risk domains, durable suppression, observable delivery stages, and a tested recovery and provider-exit path.

## Required Inputs

- message purposes, recipients, countries, products, brands, From domains, volumes, bursts, latency, expiry, and harm from delay or loss
- transactional, security, product, lifecycle, and marketing classifications plus consent and unsubscribe rules
- sending providers, IP model, DNS control, return path, bounce domain, link domain, DKIM ownership, DMARC policy, and existing reputation
- list provenance, address lifecycle, suppression sources, complaints, forwarding, aliases, account deletion, and support workflows
- sensitive content, tracking, retention, accessibility, localization, cost, failover, and operational owners

## Safety and Permission Constraints

- Use [Notification Delivery Design](../notification-delivery-design/SKILL.md) for the shared event, preference, queue, template, privacy, and cross-channel model. This skill owns email-specific delivery operations.
- Do not purchase, scrape, rent, or silently repurpose recipient lists. Separate marketing permission from transactional necessity and preserve suppression after ordinary account or list changes where required.
- Treat addresses, message content, delivery events, engagement, DMARC reports, complaints, and support evidence as potentially personal data. Minimize tracking and never put secrets, passwords, full tokens, or sensitive account state in email.
- Provider acceptance, a `250` SMTP response, or a delivered webhook does not prove inbox placement, reading, or user action. Do not use opens as a sole business or security fact.
- Production DNS changes, broad sends, domain warm-up, recipient import, tracking enablement, provider activation, or failover are R3 actions requiring authorization, staged rollout, cost bounds, and rollback.

## Workflow

1. Classify every stream by purpose, permission, urgency, content sensitivity, expected volume, unsubscribe behavior, complaint risk, and failure consequence. Keep security, transactional, and marketing rules explicit.
2. Design sending identities and isolation. Choose stable organizational and From domains, subdomains, return paths, link domains, DKIM selectors, and IP pools so a high-risk stream cannot unnecessarily damage critical account mail.
3. Inventory every authorized sender before changing policy. Align SPF and DKIM with visible From domains and implement current DMARC semantics from RFC 9989. Stage policy from observation to enforcement only after reports and real traffic show legitimate sources are aligned.
4. Establish correct forward and reverse DNS where applicable, TLS transport, RFC-conformant message construction, key rotation, provider ownership, and documented DNS time-to-live and rollback.
5. Build a consent and address-lifecycle system: source, purpose, capture evidence, confirmation where appropriate, preference, global and stream suppression, hard and soft bounce, complaint, role-address policy, inactive recipient, and account closure.
6. Implement RFC 8058 one-click unsubscribe for applicable list mail, a visible accessible in-message option, authenticated opaque unsubscribe identifiers, prompt suppression, and no login or additional consent barrier.
7. Render safe multipart templates. Escape untrusted values, preserve plain text and accessible structure, keep security actions on the trusted product origin, use short-lived single-purpose tokens, and prevent tracking or link rewriting from breaking critical flows.
8. Queue with stable message IDs, expiry, bounded retries, provider-specific classification, rate and concurrency controls, domain-aware backpressure, and no retries for permanent address or policy failures.
9. Process feedback into one authoritative suppression and diagnostics path. Correlate requested, suppressed, accepted, deferred, bounced, complained, unsubscribed, and provider-rejected states without storing unnecessary message content.
10. Launch gradually and measure by stream, domain, provider, and cohort. Watch complaint, bounce, deferral, authentication, block, latency, and cost signals; pause on threshold breach and keep a tested in-product recovery path for missed critical mail.
11. Rehearse provider outage, DNS error, DKIM rotation, DMARC policy rollback, shared-IP reputation event, complaint spike, forwarding breakage, suppressed critical recipient, duplicate event, and migration using synthetic addresses and non-production domains.

## Required Output

- message-stream and permission matrix with delivery and harm requirements
- domain, DNS, SPF, DKIM, DMARC, return-path, link, selector, and IP design
- address, consent, suppression, bounce, complaint, and unsubscribe state model
- queue, retry, expiry, template, link, feedback, and recovery controls
- staged rollout, deliverability metrics, alert thresholds, runbooks, and cost controls
- provider comparison, DNS rollback, export, migration, and exit plan

## Completion Gate

Do not call email ready until all legitimate senders authenticate and align, unauthorized sources are discoverable, list provenance and suppression are enforced server-side, critical mail has a non-email recovery path, reports and feedback are privacy-controlled, and a staged test proves rollback from DNS, provider, and reputation failures.

## Conditional Reference

Read [Email Deliverability Evidence](references/email-deliverability-evidence.md) when configuring authentication, receiver requirements, DMARC reporting, or one-click unsubscribe.
