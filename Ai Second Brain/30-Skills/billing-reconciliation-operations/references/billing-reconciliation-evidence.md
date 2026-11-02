# Billing Reconciliation Evidence

Verified: 2026-10-22

## Provider and Government Evidence

- [Stripe balance transactions](https://docs.stripe.com/api/balance/balance_history) exposes transactions that contribute to a Stripe account balance and allows automatic-payout filtering by payout ID. This is provider account activity, not the internal ledger, bank statement, or accounting classification.
- [PayPal Balance Reconciliation report](https://developer.paypal.com/reports/balance) documents transaction-level payments, refunds, disputes, fees, withdrawals, beginning and ending balances, file totals, and reconciliation. PayPal advises integrations to read by column name because reports can gain attributes.
- [PayPal Settlement report](https://developer.paypal.com/reports/settlement/) documents daily settlement detail, per-currency totals, versioned filenames, delivery, retention, and notification contacts. Availability and access depend on merchant approval and SFTP configuration.
- [Apple App Store Server API](https://developer.apple.com/documentation/appstoreserverapi) provides signed transaction, subscription, refund, and notification-history interfaces. Apple states that notification history can recover missed Version 2 notifications for a bounded period; current state can require transaction or subscription-status queries.
- [Apple App Store Server Notifications](https://developer.apple.com/documentation/AppStoreServerNotifications) marks Version 1 deprecated and directs new integrations to Version 2. Notifications cover lifecycle events but the application remains responsible for verification, interpretation, idempotency, and recovery.
- [Google Play backend integration](https://developer.android.com/google/play/billing/backend) documents real-time developer notifications, message deduplication, authoritative API checks, voided purchases, and downloadable reporting data for financial reconciliation.
- [IRS Publication 583](https://www.irs.gov/publications/p583) explains that supporting documents, journals, ledgers, computerized records, and returns must remain legible and reconcilable. Retention and accounting requirements still depend on entity, jurisdiction, and qualified advice.

## Decision Implications

- Webhook delivery, provider transaction status, provider balance movement, payout, bank posting, internal ledger, entitlement, and accounting entry are distinct evidence layers with different timing and failure modes.
- Reconciliation needs both record-level matching and independent aggregate controls. A matching net total can hide missing, duplicated, misclassified, cross-currency, or cross-entity activity.
- Provider report schemas and availability change. Version parsers, retain raw evidence securely, check completeness, and design an export path before relying on a provider.
- Missed-event recovery must use provider history or reports rather than replaying guessed side effects. Any entitlement or value correction should be idempotent and auditable.
- These sources describe provider mechanics and introductory recordkeeping, not project accounting treatment. Qualified finance, tax, and legal owners decide classification, close, retention, and reporting policy.
