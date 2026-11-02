---
name: payments-ledger-design
description: Design or review payment, subscription, entitlement, refund, dispute, credit, wallet, marketplace, and internal ledger flows with idempotency, reconciliation, immutable postings, and provider boundaries. Use when money or stored value changes rights or obligations; do not execute real transactions or replace accounting, legal, tax, fraud, or compliance specialists.
---

# Payments and Ledger Design

## Outcome

Produce an auditable money-flow architecture in which provider events, product entitlements, and internal obligations reconcile without mutable informal balances or duplicate side effects.

## Required Inputs

- products, prices, currencies, taxes, discounts, trials, credits, and refund rules
- parties, merchant or marketplace roles, countries, payout flows, and ownership of funds
- payment methods, authorization, capture, settlement, failure, dispute, and chargeback behavior
- subscription lifecycle and entitlement invariants
- whether credits are promotional, purchased, transferable, redeemable, expiring, or withdrawable
- accounting, tax, legal, fraud, support, PCI, privacy, and recovery owners
- provider contract, webhook behavior, reconciliation APIs, fees, reserves, limits, regions, and export path

Stored value, money transmission, marketplace payouts, lending, securities, gambling, and tax handling can create regulated obligations. Stop for qualified review before architecture commitment.

## Safety and Permission Constraints

- Minimize payment-data scope by using provider-hosted or tokenized collection when product requirements permit. Never store card verification codes or raw payment credentials.
- Treat browser redirects and client success screens as user experience, not proof of settlement or entitlement.
- Use idempotency at API, webhook, ledger, and fulfillment boundaries. Reconciliation is required even when webhooks are healthy.
- Represent value changes as append-only balanced postings with explicit currency or unit, source, reason, actor, and effective time. Correct mistakes through linked reversals or adjustments, not silent edits.
- Never use floating-point values for money. Define integer minor units or an exact decimal and rounding policy per currency or asset.
- Real charges, refunds, transfers, payouts, balance adjustments, provider activation, or production ledger migration are R3 and require immediate authorization, qualified review, sandbox evidence, limits, and rollback or compensation.

## Workflow

1. Map the end-to-end commercial journey and identify the legal and economic parties, source of funds, obligations, fees, taxes, settlement, and user-facing state.
2. Define state machines for order, payment, subscription, entitlement, refund, dispute, and payout. State which events are authoritative and which are advisory.
3. Compare payment providers on supported markets and methods, hosted collection, fraud controls, webhook and idempotency contracts, subscription or marketplace features, reports, export, support, pricing, and lock-in.
4. Keep provider tokens and identifiers at a replaceable boundary. Verify high-impact state server-side and process signed events through the webhook skill.
5. Define a ledger when the system owes, holds, allocates, or tracks value. Model accounts and balanced transactions; separate pending from posted; enforce currency or asset isolation; and make entries immutable.
6. Link each business event, provider object, idempotency key, and ledger transaction. Enforce unique posting and legal state transitions under concurrency.
7. Derive balances and entitlements from authoritative state. Do not let a mutable balance column or client claim be the sole record.
8. Reconcile provider reports and bank settlement to internal orders and ledger postings. Route mismatches to owned exception handling without auto-erasing evidence.
9. Define refunds, partial refunds, disputes, negative balances, expired credits, failed payouts, provider outages, migration, and account closure.
10. Test duplicate requests and webhooks, out-of-order events, timeout after provider success, currency rounding, concurrent spend, insufficient funds, reversal, dispute, reconciliation mismatch, and restore.

## Required Output

- money and obligation flow map
- provider comparison and PCI-scope strategy
- state machines and entitlement invariants
- chart of accounts or ledger model with balanced posting rules
- idempotency, webhook, fulfillment, and reconciliation design
- fraud, privacy, tax, accounting, and regulatory review boundaries
- failure-focused test evidence and operational controls
- migration, export, rollback or compensation, and provider-exit plan

## Completion Gate

Do not call the design ready until duplicate and crash-window tests preserve value, every posted transaction balances, provider and internal records reconcile in a sandbox, refunds and disputes are exercised, and qualified reviewers accept the applicable accounting and regulatory boundaries.

## Conditional Reference

Read [Payments and Ledger Evidence](references/payments-ledger-evidence.md) when defining scope, idempotency, immutable postings, or reconciliation.
