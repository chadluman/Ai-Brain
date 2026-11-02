---
name: monetization-model-design
description: Select and validate a fair monetization model, packaging, pricing metric, entitlement lifecycle, channel policy, and economic controls. Use when choosing free, paid, freemium, subscription, usage, transaction, marketplace, advertising, or hybrid revenue models for web or mobile products.
---

# Monetization Model Design

## Outcome

Recommend a monetization model that aligns the value users receive with understandable charges and sustainable delivery economics, then define the product, policy, entitlement, measurement, and exit requirements needed to test it safely.

## Required Inputs

- user, buyer, payer, beneficiary, value delivered, alternatives, and buying process
- product stage, channels, countries, age groups, customer type, and distribution platforms
- recurring and marginal costs, support load, capacity limits, desired margin or funding model
- candidate packages, price metric, billing period, usage measurement, trial, discount, and refund assumptions
- payment providers, app stores, tax or marketplace roles, currency, and jurisdiction constraints
- entitlement, account, cancellation, retention, fraud, privacy, analytics, and reconciliation needs

## Safety and Permission Constraints

- Do not use hidden terms, preselected paid options, obstructive cancellation, misleading scarcity, disguised advertising, confusing trials, or other manipulative patterns. Material price, renewal, usage, refund, and cancellation terms must be clear before consent.
- Do not claim current app-store, payment, tax, consumer, advertising, children's, gambling, credit, or marketplace rules from memory. Recheck official rules for the target channel, storefront, product, and date, then obtain qualified review where required.
- A price or model test must not expose a customer to an undisclosed charge or create a promise the product cannot honor. Contact, publishing, payment activation, store submission, and real-money experiments require authorization.
- Keep payment state, entitlement state, usage records, invoices, refunds, disputes, and an auditable ledger distinct. Never implement credits or balances as an informal mutable number.
- Minimize billing and behavioral data, define retention, restrict access, and never place secret keys or real customer data in the vault.

## Workflow

1. Define the customer and value event. Separate who uses, benefits, decides, pays, administers, and supports the product.
2. Establish nonnegotiable constraints: accessibility, trust, recurring value, cost drivers, cash timing, regulation, platform distribution, sales motion, and operational capacity.
3. Compare viable models such as free, sponsorship, paid download, one-time purchase, freemium, subscription, per-seat, usage, tiered, transaction fee, marketplace, advertising, or hybrid. Include the no-charge or cost-recovery option where relevant.
4. Choose a pricing metric that users can understand and influence and that correlates with value and cost. Analyze gaming, bill shock, seasonality, shared accounts, idle use, and accessibility or inclusion effects.
5. Design packages and boundaries from distinct customer needs rather than artificial feature withholding. State included value, limits, overage, upgrade, downgrade, proration, trial, renewal, grace, refund, dispute, and cancellation behavior.
6. Model low/base/high acquisition, conversion, retention, support, payment failure, refunds, fraud, taxes, platform fees, and marginal service cost. Identify the assumptions that can make the model unsustainable.
7. Map every distribution channel to its current payment and disclosure rules. Document eligible exceptions and regional programs rather than assuming web, Apple, and Google permit the same flow.
8. Define catalog, price-version, purchase, usage, invoice, payment, entitlement, notification, reconciliation, and support states. Use the [Payments and Ledger Design](../payments-ledger-design/SKILL.md) skill for money movement and balances.
9. Plan the smallest ethical validation: price interviews, package comprehension, prototype testing, authorized offer tests, or cohort analysis. Predeclare decision and guardrail thresholds and measure cancellation and harm as well as conversion.
10. Record the decision, rejected options, policy evidence date, implementation dependencies, monitoring, rollback, price migration, export, and re-evaluation triggers in an ADR.

## Required Output

- customer, payer, value event, channel, region, and constraint statement
- model and package comparison with user, economic, operational, and policy tradeoffs
- price metric, packages, lifecycle rules, disclosures, and entitlement model
- low/base/high economic model with sensitivity and bill-shock analysis
- current official platform and provider evidence with verification dates
- validation plan, trust and harm guardrails, approval boundaries, and success or stop criteria
- ADR recommendation with rollback, migration, and re-review triggers

## Completion Gate

Do not call the model ready until the charge is understandable before consent, recurring charges provide recurring value, cancellation and failure paths are defined, entitlements reconcile from authoritative events, economics survive plausible scenarios, and target-channel rules have been checked for the intended launch date and region.

## Conditional Reference

Read [Monetization Evidence](references/monetization-evidence.md) when comparing revenue models, defining subscription or usage behavior, or mapping mobile distribution constraints.
