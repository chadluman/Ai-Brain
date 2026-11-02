---
name: payment-fraud-abuse-controls
description: Design or review layered controls for account takeover, card testing, stolen instruments, promotion abuse, refund abuse, chargebacks, and marketplace payment abuse. Use when a commerce flow needs risk signals, challenge policy, manual review, monitoring, and false-positive safeguards; do not use it to conduct investigations or make legal compliance claims.
---

# Payment Fraud and Abuse Controls

## Outcome

Produce a measurable, privacy-conscious fraud-control system that limits loss and abuse without treating a provider score, authentication result, or opaque automated decision as proof of legitimacy.

## Required Inputs

- checkout, account, subscription, refund, credit, payout, seller, and support journeys
- payment methods, providers, countries, currencies, channels, transaction volumes, loss and dispute history, and acceptable latency
- assets at risk, likely abuse cases, attack costs, loss owners, customer-harm limits, and decision or appeal owners
- available identity, device, network, behavioral, transaction, fulfillment, and provider signals with provenance and retention
- challenge, hold, manual-review, decline, refund, dispute, and recovery capabilities

## Safety and Permission Constraints

- Minimize payment-data scope. Never store card verification codes, raw credentials, or unnecessary full instrument data; use reviewed provider-hosted or tokenized collection where it fits.
- Fraud prevention does not authorize broad tracking, fingerprinting, undisclosed profiling, or indefinite retention. Document purpose, necessity, accuracy, access, location, sharing, retention, and user rights for every signal.
- Do not use protected characteristics or unexplained proxies as risk shortcuts. Measure false positives and accessibility effects across relevant user groups, devices, networks, and regions; provide review or recovery for consequential decisions.
- A successful login, 3-D Secure result, authorization, risk score, address match, or provider approval is one signal, not proof that the customer or business event is legitimate.
- Production rule changes, account restrictions, fund holds, payout delays, evidence submissions, or automated adverse decisions are consequential actions and require authorization, monitoring, safe rollback, and the applicable legal or policy review.

## Workflow

1. Threat-model each commercial journey using the [Application Threat Modeling](../application-threat-modeling/SKILL.md) skill. Include account takeover, synthetic or stolen identity, card testing, triangulation, reshipping, promotion and referral abuse, refund or friendly fraud, bot activity, seller collusion, payout diversion, and support-channel abuse as applicable.
2. Define measurable outcomes: prevented loss, confirmed fraud, dispute rate, card-testing volume, review yield, customer abandonment, false-positive rate, recovery time, and operational load. Separate labels by confidence and delay.
3. Reduce the attack surface before scoring. Protect accounts and recovery, bind sensitive changes, rate-limit attempts, isolate payment pages, inventory scripts, validate server-side state, protect webhooks, and restrict privileged support actions.
4. Map each candidate signal to source, freshness, manipulability, missing behavior, privacy cost, bias risk, and failure mode. Prefer signals tied directly to the transaction and authenticated history over invasive or weakly correlated proxies.
5. Design a response ladder: allow, observe, limit, require stronger authentication, delay fulfillment, request safe evidence, route to review, decline, suspend, or recover. Apply the least harmful response that meaningfully changes risk.
6. Place EMV 3-D Secure, strong customer authentication, or provider challenges within a jurisdiction- and provider-specific policy. Define exemptions, unavailable paths, challenge failures, accessibility, liability implications, and fallback; do not hard-code a timeless version assumption.
7. Make automated decisions traceable. Record rule or model version, input provenance, reason codes, decision, operator override, outcome, and expiry without retaining prohibited payment data.
8. Establish manual-review and appeal controls: least privilege, dual control for sensitive actions, evidence minimization, time limits, consistent decision guidance, queue capacity, escalation, and audit history.
9. Test adversarial sequences, duplicates, concurrency, low-and-slow attempts, device and network changes, provider outage, unavailable authentication, compromised accounts, refund timing, false positives, and recovery. Use synthetic data in an isolated environment.
10. Monitor drift, attack displacement, approval and loss by segment, challenge rate, review backlog, customer harm, and provider changes. Retire ineffective signals and rules rather than accumulating them.

## Required Output

- journey-specific fraud and abuse threat model with loss and harm owners
- signal inventory with provenance, privacy, quality, bias, retention, and failure analysis
- layered controls and response matrix with reason codes, review, appeal, and recovery
- payment-page, identity, provider, webhook, ledger, fulfillment, and support boundaries
- test and monitoring plan with loss, false-positive, accessibility, and operational metrics
- rollout, rollback, incident, rule-retirement, and re-review triggers

## Completion Gate

Do not call the controls ready until high-impact threats have layered mitigations, prohibited payment data is excluded, decisions are traceable, false positives and accessibility have explicit limits, operators can recover legitimate users, provider and regulatory assumptions are current, and an isolated test shows safe failure and rollback.

## Conditional Reference

Read [Payment Fraud and Abuse Evidence](references/payment-fraud-evidence.md) when defining payment-page controls, authentication, identity signals, or jurisdiction-specific challenge boundaries.
