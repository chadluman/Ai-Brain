---
name: soc2-vendor-and-subservice-review-design
description: Run SOC 2 vendor and subservice management under CC9.2: a vendor register covering every vendor that touches customer data or the production path, risk tiering, assessment before production data flows, and annual dated reviews that record a vendor's SOC 2 report, its exceptions, and the complementary user entity controls implemented in response. Use when adding any vendor, at annual review, and when a vendor's report period ends; do not use "the vendor is SOC 2" as a review, and do not add a vendor to production before its assessment is recorded.
---

# SOC 2 Vendor and Subservice Review Design

## Outcome

Prove, vendor by vendor, that the organisation knows what it relies on, what its vendors actually cover, and what it must do itself: a register, a dated review record per vendor per year, and a complementary-controls map with no vendor missing and no exception ignored.

## Supporting Skills

Load only what the gap requires:

- [SOC 2 Control Matrix and System Description Design](../soc2-control-matrix-and-system-description-design/SKILL.md) for carve-out, complementary controls, and the system description's vendor schedules.
- [Third-Party Service Evaluation](../third-party-service-evaluation/SKILL.md) for evaluating a vendor's fit, security, privacy, and cost; this skill adds only the SOC 2 layer: the dated, exception-aware, complementary-controls-mapped review record, repeated annually.
- [SOC 2 Evidence Operations Design](../soc2-evidence-operations-design/SKILL.md) for filing review records by criterion.

## Design

1. **Inventory every vendor that touches customer data or the production path.** Hosting, database, auth, payments, email, error tracking, analytics, platform APIs, AI providers, support inboxes, and any script or service that sees production data. The analytics script, the support inbox, and the AI API that sees prompts are vendors too; missing one is a scope finding.
2. **Risk-tier each vendor.** Tier by data touched, production-path criticality, and substitutability. A payments provider and an auth provider are top tier; a marketing analytics script is lower tier but still registered. Tiering decides review depth, not whether a review happens.
3. **Assess before production data flows.** A new vendor is assessed and entered in the register before customer data flows to it, not after. The assessment records purpose, data touched, tier, data-processing agreement date, and the security evidence relied upon.
4. **Review annually, with exceptions and complementary controls.** For each vendor, obtain its SOC 2 report (or equivalent evidence where it has none), read it, and record: report period, review date, exceptions noted, and the complementary user entity controls (CUECs) implemented in response. A review that records only "vendor is SOC 2" is not a review. When a vendor's report period ends before the organisation's own period, check its bridge letter and record the gap.
5. **Map the shared-responsibility boundary per vendor, in the vendor's own terms.** For the reference stack, the 2026-11-02 research run found, with the caveats below:
   - **Hosting (Vercel):** the vendor runs code safely — infrastructure patching, physical security, edge protection, deployment pipeline integrity. The organisation owns its code and dependencies, team roles and MFA, secret hygiene, deployment configuration, its own authorisation, logging, and data handling, and its domain and TLS settings. *Caveat: the vendor's current official compliance page was not fetched in that research run, and secondary sources disagree on its ISO version and on report-access plan gates — re-verify on the vendor's Trust Center before citing its report status, plan gates, or log-retention limits.*
   - **Database (Neon):** the vendor stores data safely — storage encryption, infrastructure patching, backups and point-in-time recovery. The organisation owns schema and row-level security and tenancy enforcement, least-privilege database roles, parameterised queries, token and personal-data minimisation, branch-data anonymisation, and restore testing (its own test, not the vendor's backup existence).
   - **Auth (Clerk):** the vendor proves who the user is — authentication, session tokens, brute-force and breached-password protection. The organisation owns enforcing MFA in its app, organisation and role configuration, session and user revocation, protecting its secret keys, authorisation after authentication (identity is not permission), and webhook verification. Clerk's SOC 2 Type 2 report was held since 2022-05-06 in that research run, with report access plan-gated; re-verify at request time.
   - **Payments (Stripe):** the vendor moves money safely — card-data vault, tokenisation, storage encryption, dashboard controls. The organisation owns dashboard access and MFA, restricted keys per purpose and rotation, webhook signature verification, idempotency, and reconciliation of its subscription state against Stripe, its integration choice and resulting PCI scope, and never storing or handling cardholder data itself.
6. **Handle vendors without a SOC 2 report explicitly.** Carve-out leaves a gap that must be filled with other evidence — questionnaire, penetration test, contractual controls — and the gap must be flagged in the review, not hidden. If no credible evidence exists, the vendor's tier and the risk acceptance must be recorded as a decision, not assumed away.
7. **Re-review on change, not only annually.** A vendor acquisition, a major service change, a reported breach, or a new data flow to an existing vendor triggers a review, recorded with its date and outcome, outside the annual cycle.

## Guardrails

- Do not claim vendor inheritance. "We use SOC 2 vendors" with no review record is not a control, and a vendor's report does not cover the organisation's configuration of that vendor.
- Do not review only the vendors that are easy to review. The highest-risk vendor is often the one nobody thought to register.
- Do not accept a vendor report without reading its exceptions. An exception the organisation ignores is an exception it inherits.
- Do not let report access plan gates surprise the timeline. Some vendors gate report access behind paid or business plans; confirm access before the observation period, not during it.
- None of the vendors above prove that the organisation's code authorises the right tenant, that its control actions are authorised, that its tokens are scoped and revocable, or that its changes were reviewed. Those are the organisation's controls, and they are exactly where a livestream control surface's real risk lives.

## Verification

Vendor management is ready when: the register covers every production-path and customer-data vendor with no known omission; every vendor has a dated review within the last year recording report period, exceptions, and complementary controls implemented; every new vendor was assessed before production data flowed; every vendor without a SOC 2 report has a flagged gap with compensating evidence or a recorded risk decision; and a sample of three complementary controls traces from a vendor report, through the review record, to an implemented control in the organisation's own system.
