---
name: sms-messaging-readiness
description: Design or review application-to-person SMS and MMS messaging across consent, sender registration, carrier rules, opt-out, quiet hours, segmentation, delivery, security, abuse, cost, and fallback. Use when a product plans notifications, marketing, support, or verification by text; do not use it as legal approval or to send production messages.
---

# SMS Messaging Readiness

## Outcome

Produce a country-, purpose-, and sender-specific messaging design that sends only expected texts, honors revocation reliably, withstands carrier and provider failure, and never treats a phone number or delivery receipt as durable identity proof.

## Required Inputs

- countries, recipient types, ages, message purposes, urgency, content, languages, accessibility, volumes, bursts, and expected replies
- marketing, transactional, security, verification, support, emergency, and user-to-user classifications
- consent source, sender identity, phone-number collection and verification, preference, opt-out, quiet-hour, retention, and complaint rules
- long code, toll-free, short code, alphanumeric, RCS, MMS, or other sender candidates plus provider, carrier, registration, throughput, price, and regional support
- account recovery, authentication assurance, fraud, number reassignment, SIM change, portability, and alternate-channel requirements

## Safety and Permission Constraints

- Treat phone numbers, message content, delivery metadata, consent evidence, and carrier registration data as sensitive. Never put passwords, full authentication secrets, health details, payment credentials, or unnecessary private content in a text.
- A phone number can be shared, ported, reassigned, forwarded, intercepted, or controlled after a SIM swap. Do not use it as sole proof of personhood, account ownership, or continuing authorization.
- NIST SP 800-63B-4 treats PSTN out-of-band authentication as restricted and requires alternatives. Use stronger phishing-resistant authenticators for high-risk access when feasible and keep SMS recovery from weakening the primary method.
- Do not register a brand or campaign, purchase a number, upload recipients, transmit identity or tax data, enable a paid provider, or send production traffic without explicit authorization, current regional and carrier review, cost bounds, and rollback.
- Consent, revocation, quiet hours, prohibited content, sender registration, retention, and disclosure rules vary by jurisdiction, carrier, route, provider, and purpose. Record dated evidence and obtain qualified review rather than generalizing a provider guide.

## Workflow

1. Classify each message stream by purpose, legal or contractual basis, urgency, consent, expected replies, expiry, sensitivity, and harm from missed, delayed, duplicated, or misdirected delivery.
2. Build a destination matrix by country and carrier route. Record allowed sender types, registration, identity disclosures, throughput, length and encoding, MMS support, content restrictions, quiet hours, opt-out vocabulary, fees, and fallback.
3. Design consent as an auditable state machine: exact sender and purpose, disclosure version, capture method and time, confirmation, renewal where required, transfer prohibition, preference, revocation by every reasonable supported route, suppression, and complaint.
4. Choose the smallest sender and provider footprint that meets geography and volume. Compare data destinations, subprocessors, carrier dependencies, registration, queue behavior, delivery receipts, inbound handling, number ownership, portability, support, cost, export, and exit.
5. Calculate segmentation and cost before send. Account for GSM-7 versus Unicode, concatenation, media, locale, link length, carrier fees, retries, and failover so a content change cannot silently multiply spend.
6. Enforce sender identification, HELP and support behavior, STOP and equivalent opt-outs, one minimal confirmation where permitted, immediate suppression, cross-provider consistency, and quiet-hour scheduling at the recipient's relevant local time.
7. Queue with an idempotency key, purpose, consent version, recipient, sender, template version, segments, price estimate, expiry, and attempt state. Bound retries and never retry a permanent opt-out, invalid number, prohibited route, or expired message.
8. Process inbound messages and status callbacks as untrusted, duplicated, delayed, and reorderable input. Authenticate provider callbacks, deduplicate events, sanitize content, rate-limit abuse, and distinguish provider acceptance from handset delivery.
9. For verification codes, use short expiry, single purpose, limited attempts, rate and velocity controls, no code echo in logs, safe number-change recovery, SIM or porting risk where available, and a non-PSTN alternative.
10. Test opt-out across keywords and free text, number reassignment, wrong recipient, Unicode segmentation, daylight-saving boundaries, carrier filtering, provider outage, duplicate callback, delayed delivery, inbound abuse, cost cap, and accessible fallback using synthetic numbers.

## Required Output

- message-purpose, destination, sender, consent, and fallback matrix
- dated regional, carrier, provider, registration, and qualified-review evidence
- consent, preference, opt-out, suppression, number-change, and complaint state model
- segmentation, encoding, routing, queue, callback, retry, security, and cost design
- staged test, monitoring, alert, support, incident, and cost-control plan
- number ownership, provider export, migration, disconnection, and recovery path

## Completion Gate

Do not call SMS ready until every route has current evidence, consent and suppression are enforced centrally, STOP and reasonable revocation paths work during failure, costs are bounded by actual segments, sensitive messages have safer alternatives, callbacks are authenticated and idempotent, and an isolated test covers carrier filtering, reassignment, outage, and rollback.

## Conditional Reference

Read [SMS Messaging Evidence](references/sms-messaging-evidence.md) when evaluating United States consent changes, carrier registration, industry practices, or SMS authentication risk.
