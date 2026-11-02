---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [playbook, payments, billing, stripe, checkout, webhooks, security]
sources:
  - https://docs.stripe.com/payments/checkout/build-subscriptions
---

# Stripe Integration

## Scope and Fit

This playbook covers Stripe Checkout for fixed-price subscriptions, the Customer Portal for self-service billing management, and webhook-driven provisioning and entitlements in a web application. It does not cover custom payment forms, usage-based billing, multi-currency pricing design, tax automation, or marketplace payouts unless those are separately designed and approved.

Use Stripe Checkout when a hosted, Stripe-maintained payment page fits the product and you do not need a fully custom payment form. Do not collect, store, or transmit card details through your own server or client. Do not trust a client-side success redirect as proof of payment.

Verify the current [subscriptions with Checkout guide](https://docs.stripe.com/payments/checkout/build-subscriptions) before use. That guide was checked for this playbook on 2026-11-02. In particular, recheck the API version note for flexible billing mode, the minimum webhook events, and the Customer Portal setup steps, as Stripe updates them.

## Trust Boundary

```text
untrusted client -> server creates Checkout Session (server-chosen Price, never client-chosen amount)
client -> Stripe-hosted Checkout -> Stripe
Stripe -> signed webhook (raw body) -> server verifies signature -> idempotent ledger/entitlement update -> application data
authenticated user -> server creates Customer Portal session -> Stripe-hosted portal
```

The browser never decides the price, the plan, or the entitlement. The server chooses the Price ID from its own plan catalog, creates the session, and provisions access only from verified webhook events and, where a decision depends on it, a fresh Stripe API read.

## Prerequisites and Approval Boundaries

- Accept an ADR covering products and prices, billing mode, trials, taxes, discounts, refunds, proration, dunning, and the entitlement model.
- Apply [Payments and Ledger Design](../30-Skills/payments-ledger-design/SKILL.md), [Billing Reconciliation Operations](../30-Skills/billing-reconciliation-operations/SKILL.md), and [Payment Fraud and Abuse Controls](../30-Skills/payment-fraud-abuse-controls/SKILL.md). This playbook does not replace them.
- Security-review the exact Stripe server SDK version, the Stripe CLI version if used, and any Stripe-related dependency before use.
- Creating live products and prices, enabling live mode, changing webhook endpoints, changing portal permissions, issuing refunds, and deleting Stripe data are R3.
- Start in a dedicated Stripe sandbox/test mode. Do not test with live keys, live prices, or real payment methods.

## Configuration Inventory

| Name | Exposure | Purpose |
|---|---|---|
| `STRIPE_SECRET_KEY` | Server secret only, never `NEXT_PUBLIC_` | Server-side Stripe API key. Prefer a least-privilege restricted key (`rk_test_` / `rk_live_`) over a full secret key where the operation allows it |
| `STRIPE_WEBHOOK_SECRET` | Server secret only, per webhook endpoint | Signing secret used to verify webhook signatures for that endpoint |
| `STRIPE_PRICE_<PLAN>_<INTERVAL>` | Server configuration, not a secret, but server-chosen | Price IDs created in the Stripe Dashboard, one per plan and billing interval. The browser selects only a plan and interval; the server maps that selection to a Price ID |
| `STRIPE_BILLING_MODE` | Server configuration | Explicit billing gate, for example `disabled`, `test`, or `live`. Billing stays disabled unless this is explicitly set. Do not enable billing merely because keys are present |

Use separate test and live Price IDs, and separate test and live webhook endpoints and secrets. Never reuse a test Price ID in live mode, and never copy a product from test to live without verifying that its prices, intervals, and metadata match the approved plan catalog. The Dashboard's copy-to-live function exists for this purpose; verify its result, do not assume it.

## Products, Prices, and Checkout Sessions

1. Create one Product per plan, and one recurring Price per plan and interval, in the Dashboard or via the Stripe CLI in test mode first. Record each Price ID in server configuration, not in client code.
2. Create the Checkout Session on the server only, with `mode: "subscription"`, the server-chosen Price ID, a `success_url`, and a cancel URL. Append the session id to the success URL only where the success page needs it, and do not provision access from the success page alone.
3. For flexible billing mode, the Stripe guide checked for this playbook states that API version `2025-06-30.basil` or later is required. Recheck that version requirement before using flexible billing mode, and pin the API version explicitly so an account default change does not alter response shapes.
4. The Stripe server SDK is server-only. Never import it into a Client Component, and never put a secret or restricted key in client code, in a URL, or in a log.

A server-side session shape, to be checked against the current Stripe docs before use, is:

```ts
import Stripe from "stripe";

const stripe = new Stripe(process.env.STRIPE_SECRET_KEY as string, {
  // Pin the API version explicitly; recheck the current version before use.
});

export async function createCheckoutSession(priceId: string, customerId?: string) {
  // priceId must come from the server plan catalog, not from the client request.
  const session = await stripe.checkout.sessions.create({
    mode: "subscription",
    line_items: [{ price: priceId, quantity: 1 }],
    success_url: "https://example.com/success?session_id={CHECKOUT_SESSION_ID}",
    cancel_url: "https://example.com/pricing",
    customer: customerId,
  });
  return session.url;
}
```

## Customers, Entitlements, and the Ledger

- Create one durable Stripe Customer per application user and environment, created with an idempotency key and reused by Checkout. Do not create a new Customer on every checkout, and do not share one Customer across environments or users.
- Store the Stripe Customer ID, Subscription ID, Price ID, and subscription status in your own database, in a ledger-style record that is updated only by verified webhook events and reconciled against Stripe reports.
- Read access rights from your own database, updated by webhooks, and re-fetch the subscription from Stripe when a decision depends on it. Do not read entitlements directly from a client-sent claim, a success redirect, or a cached Stripe response that may be stale.
- Handle upgrades, downgrades, cancellations, trials, and proration through the ledger and through Stripe's subscription state, not through ad-hoc flags. Record every change with its Stripe event id, so a duplicate or out-of-order event can be detected and reconciled.

## Webhooks: Signature, Idempotency, and Minimum Events

Webhooks are the only reliable provisioning path. A customer may close the browser before reaching the success page, so the success redirect must never be the provisioning trigger.

- **Raw body only.** Read the request as raw text/bytes for signature verification. Do not parse JSON first, and do not let body-parsing middleware alter the bytes. Verify with the Stripe SDK's signature construction function and the endpoint's `STRIPE_WEBHOOK_SECRET`, and return an error for an invalid signature.
- **Idempotent processing.** Store processed event IDs and ignore duplicates. Stripe may redeliver events, and a duplicate must not double-provision, double-charge, or double-apply an entitlement.
- **Minimum events, to be rechecked against the current Stripe guide:** `checkout.session.completed`, `customer.subscription.created`, `customer.subscription.updated`, `customer.subscription.deleted`, `invoice.paid`, and `invoice.payment_failed`. The Stripe guide checked for this playbook lists `checkout.session.completed`, `invoice.paid`, and `invoice.payment_failed` as the minimum to monitor, and portal actions such as cancellation require monitoring additional events.
- **Failure handling.** On `invoice.payment_failed`, notify the customer and send them to the Customer Portal to update their payment method; the subscription becomes past-due, and access should follow the ledger state and the approved dunning policy, not a single failed event in isolation.
- **Testing.** Use the Stripe CLI for local webhook forwarding and test mode, and test cards and scenarios from the current Stripe docs in test mode only. Do not use real cards in test mode, and do not use test cards in live mode.

A webhook handler shape, to be checked against the current Stripe docs and the framework's raw-body handling before use, is:

```ts
import Stripe from "stripe";

const stripe = new Stripe(process.env.STRIPE_SECRET_KEY as string);

export async function handleStripeWebhook(req: Request) {
  const body = await req.text(); // raw body, do not use req.json() here
  const signature = req.headers.get("stripe-signature") as string;
  const event = stripe.webhooks.constructEvent(
    body,
    signature,
    process.env.STRIPE_WEBHOOK_SECRET as string,
  );
  // Dispatch by event.type, with idempotent processing per event.id.
  // Return 200 only after the event has been durably recorded and processed,
  // or after it has been explicitly ignored as a duplicate or unknown type.
  return event;
}
```

## Customer Portal

Configure the Customer Portal in the Dashboard before relying on it. At a minimum, configure it so customers can update their payment methods. If the portal is allowed to cancel subscriptions, change plans, or update billing details, monitor the additional events those actions produce.

Create the portal session on the server only, using the Stripe Customer ID saved while processing `checkout.session.completed`, and pass a `return_url` for the page the customer returns to after managing billing. Do not create a portal session from a client-sent customer id, and do not expose another customer's portal session.

## Verification

- Checkout, portal, and webhook flows work end to end in test mode, with separate test products, prices, and webhook secrets, before any live activation.
- A success redirect alone does not provision access; access appears only after a verified webhook, and survives a browser close before the redirect.
- Duplicate webhook deliveries do not double-provision or double-charge, and out-of-order subscription events reconcile to the correct ledger state.
- Invalid webhook signatures are rejected, and secret and restricted keys do not appear in client code, logs, or committed files.
- Past-due, cancelled, and trialing states produce the correct access and user messaging, and a failed payment sends the customer to the portal as designed.
- Billing remains disabled unless the billing mode flag is explicitly set to test or live, and live activation requires a separate, explicit approval step.

## Operations, Cost, and Exit

Monitor webhook delivery failures, signature failures, past-due subscriptions, failed payments, refund volume, and reconciliation breaks between Stripe reports and the ledger. Alert on webhook delivery failure and on any ledger/Stripe mismatch, and reconcile daily or per billing cycle as the ADR requires.

Recheck Stripe pricing, fees, and plan limits for the selected account, currency, and payment methods before an ADR is accepted. Do not quote a fee from this playbook; fees and pricing change, and they depend on the account and payment method.

For exit, inventory products, prices, customers, subscriptions, portal configuration, webhook endpoints, and API keys. Do not delete Stripe data to "clean up" a test account without checking Stripe's data retention and deletion rules for that mode, and do not cancel live subscriptions as a migration step without a customer communication and refund plan. Revoke keys only after the replacement billing system is verified and a rollback is no longer needed.

## Re-Review Triggers

- Stripe API major version, SDK major version, Checkout, Portal, or webhook event change
- Product, price, trial, tax, discount, proration, or dunning policy change
- Webhook endpoint, signing secret, or portal permission change
- Ledger/Stripe reconciliation break, duplicate provisioning, failed payment spike, or refund anomaly
- Pricing, fee, or account terms change
