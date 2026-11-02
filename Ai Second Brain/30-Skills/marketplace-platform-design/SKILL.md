---
name: marketplace-platform-design
description: Design or review a multi-party marketplace's commercial roles, seller onboarding, listings, payments, payouts, disputes, trust, compliance boundaries, and exit path. Use when a platform connects third-party buyers and sellers or allocates transaction value; do not use it for a single-merchant store or as legal approval to hold or transmit funds.
---

# Marketplace Platform Design

## Outcome

Produce a role-accurate marketplace architecture that makes seller, buyer, platform, provider, tax, payment, data, content, support, and regulatory responsibilities explicit before implementation.

## Required Inputs

- marketplace category, products or services, buyer and seller types, countries, age groups, channels, and launch stage
- contracting seller, merchant of record, platform fee, funds flow, payout timing, currencies, reserves, refunds, disputes, taxes, and insurance
- seller onboarding, identity or business verification, listings, fulfillment, reviews, moderation, complaints, recalls, suspension, and appeals
- payment, identity, tax, shipping, messaging, analytics, support, and marketplace-provider candidates
- data sensitivity, retention, residency, portability, service levels, operating capacity, and qualified-review owners

## Safety and Permission Constraints

- Marketplace, payment-processor, money-transmission, tax-facilitator, employment, agency, consumer, product-safety, content, sanctions, identity-verification, and reporting status are fact- and jurisdiction-specific. Do not infer them from product labels or provider marketing.
- Do not hold, pool, route, advance, reserve, convert, or release real funds; onboard real sellers; request identity documents; run sanctions checks; or change production payout rules without explicit authorization, qualified review, provider approval, tested limits, and a recovery plan.
- Minimize seller and buyer identity, bank, tax, location, communications, and dispute data. Separate verification evidence from ordinary product access and document the processor, destination, retention, disclosure, and deletion rules.
- Never treat a payment provider's onboarding as transferring all platform duties. The platform remains responsible for its contracts, product behavior, listings, support, moderation, disclosures, data use, and applicable laws.
- Keep payment, payout, platform fee, tax, reserve, refund, dispute, entitlement, and ledger records distinct and auditable by legal entity and currency.

## Workflow

1. Map every party and contract: buyer, seller or service provider, platform entities, merchant of record, payment service, bank, fulfiller, tax filer, insurer, app store, support operator, and regulator. State who promises what to whom.
2. Compare viable topologies: directory or lead generation, direct seller checkout, platform-facilitated payment, managed marketplace accounts, merchant of record, or inventory-owning retailer. Evaluate control, user experience, regulatory exposure, cost, disputes, portability, and operational burden.
3. Draw funds and obligation flows from order through authorization, capture, fee, tax, reserve, refund, dispute, payout, bank settlement, and negative balance. Apply [Payments and Ledger Design](../payments-ledger-design/SKILL.md) to every owed, held, or allocated amount.
4. Build a dated applicability matrix for each launch jurisdiction and product category. Route money-services, tax, seller verification, consumer, product-safety, content, labor, licensing, and reporting questions to qualified owners before architecture commitment.
5. Define staged seller onboarding with least data: eligibility, contract acceptance, business and beneficial-owner evidence when required, payout readiness, listing permissions, risk tier, periodic refresh, rejection reason, appeal, suspension, and offboarding.
6. Define listing and transaction trust controls: category rules, prohibited items or services, provenance, pricing and fee disclosures, availability, fulfillment evidence, buyer reporting, moderation, recall or takedown, review integrity, complaint handling, and accessibility.
7. Design authorization and tenant isolation across seller, staff, support, finance, moderation, and provider roles. Require step-up and dual control for payout destination, reserve, refund, identity, or suspension changes.
8. Define failure states for provider outage, delayed verification, partial fulfillment, seller non-response, dispute, negative balance, failed payout, account closure, data correction, regulatory request, and platform exit.
9. Preserve portability: stable internal party and transaction IDs, provider adapters, exportable contracts and evidence, complete ledger crosswalks, migration rules, seller and buyer notice, and a tested wind-down plan.
10. Validate a thin synthetic vertical slice across onboarding, listing, purchase, fee, refund, dispute, payout, reconciliation, moderation, support, offboarding, and recovery before any real seller or money flow.

## Required Output

- party, contract, responsibility, data, funds, and obligation maps
- topology comparison and ADR with dated legal and provider assumptions
- seller onboarding, verification, listing, moderation, dispute, payout, suspension, appeal, and offboarding state machines
- ledger, authorization, tenancy, privacy, support, reconciliation, and operational controls
- provider comparison with permissions, costs, data destinations, failure behavior, export, and exit
- isolated test evidence, unresolved qualified-review questions, approval boundaries, and launch stop conditions

## Completion Gate

Do not call the design ready until contractual and economic roles match the product behavior, no unreviewed funds or identity flow remains, seller and buyer protections are operationally owned, value reconciles by entity and currency, provider exit is feasible, and qualified reviewers have accepted the applicable regulated boundaries.

## Conditional Reference

Read [Marketplace Platform Evidence](references/marketplace-platform-evidence.md) when evaluating payment roles, seller traceability, marketplace duties, or provider fund-flow models.
