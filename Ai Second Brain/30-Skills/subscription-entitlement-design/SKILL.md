---
name: subscription-entitlement-design
description: Turn a paid subscription into feature access that is granted, changed, and revoked reliably, with your own entitlement record as the source of truth, so a payment event never silently leaves a user with the wrong access. Use when a product sells tiers or features by subscription; do not use for payment processing alone, which is covered by Payments and Ledger Design.
---

# Subscription Entitlement Design

## Outcome

Produce an entitlement record the application actually checks at request time, kept in agreement with the payment provider by verified events and periodic reconciliation, so granting, upgrading, downgrading, failing to pay, and cancelling each have exactly one defined access outcome.

Use [Payments and Ledger Design](../payments-ledger-design/SKILL.md) for money movement and ledger integrity. Use this skill for the next step: what that money buys, who holds it, and when it ends.

## Required Inputs

- The feature catalogue: every gated feature, named once, independent of any plan name or price.
- The plan-to-feature mapping: which plans include which features, and whether features are cumulative across tiers.
- The account model: whether entitlements belong to a user, an organization, or a tenant, and who may use them. See [Authorization and Tenancy Design](../authorization-tenancy-design/SKILL.md).
- The lifecycle policy for each transition: upgrade, downgrade, failed payment, cancellation, refund, and manual support grant, including any grace period.
- The provider's event model: which events grant, change, or revoke access, and how the provider's own entitlement summary, if any, is read.

If there is no feature catalogue, create one before wiring a provider. Mapping plans directly to scattered `if plan == "pro"` checks in UI code guarantees drift.

## Workflow

1. Name features, not plans, in code. A plan is a bundle of features at a point in time; a feature is the thing a request checks. When a plan changes, only the mapping changes.
2. Keep your own entitlement record as the source of truth for access checks. Record account, feature, source (provider subscription, trial, or manual grant), status, valid-from, valid-to, and the provider event that last changed it. Read that record at request time; do not call the payment provider on every request, and never trust a client claim about a plan.
3. Grant access only on a verified paid event, never on a checkout redirect or a client-side success page. A checkout completion can precede a failed or pending payment. Wait for the provider's paid or entitlement-summary event, verify its signature, and then provision.
4. Make every event handler idempotent and ordered. Deduplicate by provider event id, and resolve out-of-order events by event timestamp, not arrival order, so a delayed cancellation cannot resurrect access after a newer renewal.
5. Define each transition before building it:
   - Upgrade: immediate, or at the next billing period, stated in the product, not decided per ticket.
   - Downgrade: usually at the next billing period, with the old features available until then and a clear in-product notice.
   - Failed payment: a stated grace period with reminders and a path to update payment, then revocation. Do not cut access instantly unless the policy explicitly says so, and do not leave it open indefinitely.
   - Cancellation: access until the end of the paid period unless a refund policy says otherwise, then revocation.
   - Refund: revoke, downgrade, or keep access according to the refund policy, recorded as its own transition, not as a side effect of a payment reversal.
6. Reconcile on a schedule, not only on events. Webhooks are at-least-once in practice and can be missed. A periodic reconciliation job that compares your entitlement record with the provider's current subscription and entitlement state, and reports every mismatch, is the backstop. See [Billing Reconciliation Operations](../billing-reconciliation-operations/SKILL.md).
7. Handle manual grants as first-class records: who granted, why, which feature, and when it expires. A support grant with no expiry is a permanent entitlement created by accident.
8. Test the full matrix, not just the happy path: subscribe, upgrade, downgrade, failed payment through grace to revocation, cancel at period end, refund, duplicate event delivery, out-of-order events, and a missed webhook followed by reconciliation.

## Safety and Permission Boundaries

- Treat payment-provider data as untrusted until its signature is verified and its account is matched to your account. Never grant access from an unverified event or an unmatched customer id.
- Never put provider secret keys, webhook secrets, or other accounts' entitlement data into client code, logs, or exports.
- Entitlement changes are consequential: a grant or revocation changes what a paying customer can do. Require authorization at the R2/R3 boundary that applies, and record every change in an [Audit Log](../audit-log-design/SKILL.md).
- A new payment or entitlement library, and any change to the lifecycle policy, still requires the root security-review gate at its exact version. This skill approves no provider or package.

## Outputs and Evidence

- A feature catalogue and plan-to-feature mapping, with an owner per feature.
- An entitlement record schema, the event handlers that change it, and the reconciliation job that checks it.
- A lifecycle policy covering upgrade, downgrade, failed payment, cancellation, refund, and manual grants, with grace periods stated.
- Tests or a test report covering the full lifecycle matrix, including duplicate, out-of-order, and missed events.
