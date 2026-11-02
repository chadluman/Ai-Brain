---
name: billing-reconciliation-operations
description: Design or operate reconciliation across orders, invoices, payments, refunds, disputes, provider balances, ledgers, payouts, bank deposits, taxes, and entitlements. Use when commerce records can diverge across systems or a close process needs controls; do not use it to change live financial records without authorization.
---

# Billing Reconciliation Operations

## Outcome

Produce a reproducible control process that proves how commercial events move across application, provider, ledger, settlement, bank, tax, and entitlement systems and routes every unexplained difference to an owned exception.

## Required Inputs

- legal entities, providers, merchant accounts, bank accounts, currencies, time zones, settlement calendars, accounting periods, and materiality thresholds
- order, invoice, payment, refund, dispute, credit, fee, tax, entitlement, ledger, payout, and bank data sources
- provider identifiers, idempotency keys, report schemas, API and webhook contracts, retention, backfill limits, and export methods
- close cadence, owners, approvers, segregation of duties, exception queues, support paths, and audit requirements
- known gaps, outages, migrations, historical adjustments, and expected timing differences

## Safety and Permission Constraints

- Treat notifications and webhooks as timely hints, not a complete settlement record. Reconcile against provider transaction history, balance or settlement reports, the internal ledger, and bank evidence.
- Preserve source evidence, ingestion checkpoints, schema versions, control totals, matching decisions, operator actions, and corrections. Never erase a discrepancy by editing or netting records without an auditable reason.
- Reconciliation automation may propose matches or adjustments but must not issue charges, refunds, transfers, payouts, ledger postings, entitlement changes, or accounting entries without the authorized workflow.
- Keep provider, accounting, bank, tax, and customer data at least privilege. Do not place report files, credentials, tax identifiers, or real customer records in the vault.
- Live backfills, production corrections, period reopening, payout changes, provider report access, and bank-data connections are R3 actions requiring authorization, scoped credentials, dry-run evidence, approval, and rollback or compensating entries.

## Workflow

1. Define the reconciliation boundary by legal entity, merchant account, provider, currency, channel, time zone, settlement date, and accounting period. State which differences are expected timing and which are exceptions.
2. Name the authoritative source for each fact: commercial intent, invoice, payment status, provider balance movement, internal obligation, entitlement, payout, bank receipt, tax amount, and accounting classification.
3. Create a canonical crosswalk linking internal event and ledger IDs to provider objects, idempotency keys, payout or settlement IDs, bank references, invoices, refunds, disputes, and corrections. Preserve one-to-many and many-to-one relationships.
4. Ingest complete provider history and reports with immutable raw evidence, schema/version checks, row and amount control totals, file or page checkpoints, overlap, deduplication, and late-arrival handling. Parse evolving reports by stable field name rather than column position when the provider supports it.
5. Reconcile in stages: order to invoice; invoice to payment; payment and refund to provider balance; provider balance to ledger; payout to bank; tax to return; and authoritative purchase state to entitlement. Do not skip a stage by comparing only net totals.
6. Match deterministically first by stable identifiers and currency. Then use bounded composite matching for documented timing or aggregation behavior. Never merge across legal entity or currency, and never let a fuzzy match silently post value.
7. Calculate independent control totals: opening balance plus debits and credits equals closing balance; provider payout components equal payout total; ledger postings balance; and matched plus exceptions equals ingested population.
8. Route differences by reason and age: timing, missing event, duplicate, amount or currency mismatch, fee, foreign exchange, tax, refund, dispute, reserve, payout failure, bank return, unknown, or suspected defect. Assign owner, severity, evidence, due date, and escalation.
9. Close with review and sign-off. Freeze the evidence set, retain unresolved items with aging, record approved adjustments as linked postings, and prevent later data from silently changing a closed result.
10. Test duplicates, out-of-order events, missed webhooks, paginated history, partial files, schema additions, daylight-saving and cutoff changes, multi-currency, partial refund, dispute, reserve, failed payout, bank reversal, provider outage, replay, and historical backfill using synthetic data.

## Required Output

- reconciliation boundary, source-of-truth matrix, identifiers, cutoffs, and timing assumptions
- staged data-flow and crosswalk from commercial event through entitlement and bank settlement
- ingestion, completeness, matching, control-total, exception, close, and approval design
- exception taxonomy, ownership, aging, customer-impact, and escalation rules
- dry-run and failure-test evidence plus dashboards and alerts
- correction, backfill, period-reopen, provider-migration, export, and recovery procedures

## Completion Gate

Do not call reconciliation operational until every population has completeness controls, each matched amount traces to immutable evidence, opening-to-closing balances prove by entity and currency, unmatched items are owned and aged, corrections require approval and linked postings, and an isolated replay recovers from missed or duplicated input without changing settled value.

## Conditional Reference

Read [Billing Reconciliation Evidence](references/billing-reconciliation-evidence.md) when defining provider reports, transaction history, missed-notification recovery, or settlement controls.
