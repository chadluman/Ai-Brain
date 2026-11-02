# Payments and Ledger Evidence

Verified: 2026-10-21

## Standards and Provider Evidence

- [PCI SSC Document Library](https://www.pcisecuritystandards.org/document_library/) lists PCI DSS v4.0.1, published June 2024, as the current PCI DSS standard at verification. PCI scope and validation eligibility require the acquiring or qualified compliance parties.
- [Stripe idempotent requests](https://docs.stripe.com/api/idempotent_requests) documents a provider-specific contract for safely retrying supported API operations. Other providers differ.
- [PayPal idempotency guidance](https://developer.paypal.com/api/rest/reference/idempotency/) documents the `PayPal-Request-Id` contract for supported calls. Recheck endpoint-specific behavior before implementation.
- [Square Books](https://developer.squareup.com/blog/books-an-immutable-double-entry-accounting-database-service/) is an industry implementation report describing balanced journal entries, immutable corrections, consistency, multitenancy, and scale. It is not a standard or a reusable package approval.
- [TigerBeetle repository](https://github.com/tigerbeetle/tigerbeetle) is the canonical source for an open financial-transaction database emphasizing debit-credit transfers, idempotency, consistency, and durability. It is R0 research evidence only; installation requires a full exact-version R2 review and workload proof.

## Interpretation Boundaries

- Payment-provider status, bank settlement, product entitlement, and general accounting are related but distinct records. Reconcile them explicitly.
- Double entry detects and constrains classes of imbalance; it does not prove the business event was legitimate, correctly classified, or legally permitted.
- Provider-hosted collection can reduce card-data exposure but does not automatically eliminate all PCI, privacy, fraud, tax, accessibility, or consumer-protection duties.
- Promotional credits and stored value can have very different legal, accounting, expiry, refund, and escheatment treatment. Do not infer one from the user-interface label.
