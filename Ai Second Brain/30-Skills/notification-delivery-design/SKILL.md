---
name: notification-delivery-design
description: Design or review transactional, security, product, and marketing notifications across in-app, email, web push, mobile push, SMS, and related channels. Use when delivery reliability, user consent, preferences, retries, privacy, abuse, or provider choice affects a product.
---

# Notification Delivery Design

## Outcome

Choose the smallest channel set and build an auditable notification pipeline that respects purpose, consent, urgency, accessibility, privacy, provider limits, and the reality that provider acceptance is not user delivery.

## Required Inputs

- notification purposes, triggering events, recipients, urgency, and harm from delay or duplication
- supported platforms, regions, languages, accessibility needs, and channel preferences
- consent, legal, marketing, security, quiet-hour, suppression, and retention requirements
- volume, burst rate, latency, ordering, expiry, cost, availability, and provider constraints
- sensitive fields, templates, links, localization, analytics, and operator roles

## Safety and Permission Constraints

- Separate security, transactional, product, and marketing purposes. Do not reuse consent or bypass suppression merely because a channel is available.
- Treat addresses, phone numbers, device tokens, preferences, message content, and delivery metadata as sensitive. Minimize payloads, logs, analytics, and retention.
- Push is a hint, not a durable source of truth. Do not place secrets in notification payloads or make safety-critical state depend on delivery, order, or a single provider.
- Authenticate administrative sends, constrain audiences and rate, preview exact recipient counts, and require approval for broad or externally visible campaigns.
- Sending production notifications, changing DNS authentication, importing recipient lists, or enabling paid providers is R3 and requires immediate authorization, cost bounds, rollback, and evidence.

## Workflow

1. Classify every notification by purpose, urgency, required channel, expiry, preference behavior, and consequence of missing, duplicate, delayed, or reordered delivery.
2. Define a canonical event and message record with idempotency key, recipient, locale, template version, sensitivity, channel attempt state, and expiry. Keep domain truth outside the notification system.
3. Select channels from user value and delivery characteristics. Provide an accessible in-product destination for durable information.
4. Model consent, subscription, topic, quiet-hour, frequency-cap, legal-basis, security override, bounce, complaint, invalid-token, and account-deletion states.
5. Render versioned localized templates with escaped untrusted values, safe links, plain-text alternatives where applicable, and no secret-bearing URLs or unnecessary personal data.
6. Queue asynchronously with bounded retries, jitter, provider-specific idempotency, expiry, circuit breaking, backpressure, and dead-letter inspection. Do not retry permanent failures.
7. For email, establish aligned SPF, DKIM, current DMARC policy, one-click unsubscribe where applicable, bounce and complaint processing, and separate sending identities by risk.
8. For push, handle token rotation, revoked permission, priority, time-to-live, collapse, platform-specific limits, foreground behavior, and server reconciliation after missed messages.
9. Monitor requested, suppressed, accepted, delivered where observable, bounced, complained, opened only with justified analytics, latency, cost, and provider health. Do not mislabel acceptance as delivery.
10. Test duplicates, reordering, expiry, revoked consent, invalid addresses and tokens, provider outage, template injection, link safety, localization, accessibility, account deletion, and failover.

## Required Output

- message taxonomy and channel matrix
- consent, preference, suppression, and override policy
- event, template, queue, provider, and state-transition design
- privacy, authentication, anti-abuse, accessibility, and cost controls
- reliability model, reconciliation path, metrics, tests, and runbooks
- provider exit, DNS rollback, and migration plan

## Completion Gate

Do not call notifications ready until preference and suppression rules are enforced server-side, broad sends have approval controls, provider acceptance is distinguished from delivery, retries cannot create uncontrolled duplicates, and critical state remains recoverable without the notification.

## Conditional Reference

Read [Notification Evidence](references/notification-evidence.md) when choosing email or push behavior, authentication, delivery semantics, or unsubscribe controls.
