---
name: tax-invoicing-readiness
description: Map transaction-tax, registration, price-display, invoice, credit-note, evidence, retention, and filing-system requirements for a web or mobile product. Use when sales tax, VAT, GST, digital-service tax, or marketplace tax roles can affect commerce design; do not use it to make legal determinations or file returns.
---

# Tax and Invoicing Readiness

## Outcome

Produce a dated, jurisdiction-aware implementation boundary that identifies who sells, who may owe or collect tax, what evidence is needed, how invoices and corrections behave, and which decisions require a qualified tax adviser.

## Required Inputs

- selling entities, merchant-of-record and platform roles, launch date, countries, states or provinces, currencies, and sales channels
- customer types, seller and customer locations, products or services, delivery method, exemptions, refunds, discounts, credits, and bundles
- current registrations, thresholds, certificates, tax identifiers, filing owners, accounting basis, and record-retention obligations
- catalog, checkout, invoice, credit-note, payment, ledger, marketplace, reporting, and provider boundaries
- required price display, language, numbering, currency conversion, and business-customer behavior

## Safety and Permission Constraints

- Treat product classification, nexus or establishment, place of supply, exemptions, tax rate, registration, invoicing, filing, and retention as jurisdiction- and fact-specific. Record evidence and obtain qualified review; do not infer a legal conclusion from provider software.
- Do not activate collection, register an entity, submit a return, accept provider terms, transmit taxpayer data, or change production invoices without explicit authorization and a reviewed rollback or correction plan.
- Minimize addresses, tax identifiers, exemption evidence, and invoice recipient data. Define purpose, access, retention, export, correction, and deletion constraints before collection.
- Preserve finalized commercial and tax records. Correct with versioned credit notes, cancellations, or adjustments required by the applicable system; never silently rewrite issued evidence.
- Keep catalog price, taxable basis, calculated tax, customer-facing invoice, provider transaction, ledger posting, filed return, and remittance as linked but distinct records.

## Workflow

1. Draw the transaction and responsibility map. Identify contractual seller, merchant of record, platform, payment processor, supplier, customer, filer, and cash recipient for each channel.
2. Build a jurisdiction matrix by entity, customer type, product class, delivery location, currency, and effective date. Mark each classification or threshold as verified, adviser-confirmed, assumed, or unresolved.
3. Determine the evidence required before a decision: customer location, seller establishment, product tax code, business status, exemption certificate, tax identifier, exchange rate, or marketplace statement. Collect only evidence with a defined purpose.
4. Define registration and collection states separately. Include threshold monitoring, effective dates, pending registration, deregistration, rate changes, tax-inclusive or exclusive display, and behavior when evidence or calculation is unavailable.
5. Define invoice and credit-note requirements for each target jurisdiction and customer type: issuer and recipient identity, unique numbering, issue and supply dates, line descriptions, currency, taxable basis, rates, tax amounts, exemptions, reverse-charge text, and correction linkage where applicable.
6. Design immutable, versioned tax decisions. Store the input facts, rule or provider version, result, reason, currency and rounding policy, source transaction, and later adjustment without storing unnecessary sensitive data.
7. Compare tax services only after the responsibility model is known. Check supported jurisdictions and products, registration assumptions, evidence rules, invoicing, refunds, reports, retention, audit export, price, limits, data destinations, failure behavior, and exit path.
8. Connect tax events to the [Payments and Ledger Design](../payments-ledger-design/SKILL.md) boundary. Reconcile order, invoice, payment, refund, provider report, ledger, filed return, and remittance without treating any one provider record as universal truth.
9. Test boundary cases: registration effective-date changes, B2B and B2C, conflicting location evidence, invalid identifiers, inclusive pricing, mixed-rate bundles, discounts, partial refunds, currency conversion, rounding, provider outage, duplicated events, and historical correction.
10. Record the qualified-review owner, implementation assumptions, unresolved jurisdictions, evidence date, monitoring, export, rollback or correction path, and re-review triggers in the project decision record.

## Required Output

- party, channel, money-flow, and tax-responsibility map
- dated jurisdiction and product matrix with evidence status and qualified-review questions
- registration, collection, price-display, invoice, credit-note, refund, filing, and retention state model
- data schema and lineage from checkout facts through invoice, ledger, return, and remittance
- provider comparison, failure behavior, audit export, and exit plan when automation is proposed
- test matrix, reconciliation controls, operational owners, and change-monitoring triggers

## Completion Gate

Do not call the design ready until the seller and filing roles are explicit, material classifications have current authoritative evidence or qualified confirmation, invoices and corrections are reproducible, tax records reconcile to payments and the ledger, sensitive evidence is governed, and every unresolved jurisdiction has an owner and safe launch decision.

## Conditional Reference

Read [Tax and Invoicing Evidence](references/tax-invoicing-evidence.md) when defining cross-border principles, invoice controls, recordkeeping, or provider limitations.
