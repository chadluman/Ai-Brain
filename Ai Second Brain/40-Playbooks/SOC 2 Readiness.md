---
status: draft
owner: vault-owner
created: 2026-11-02
last_verified: 2026-11-02
review_by: 2027-02-02
risk: R3
tags: [playbook, soc2, compliance, audit, security]
sources:
  - https://www.aicpa-cima.com/resources/landing/system-and-organization-controls-soc-suite-of-services
  - https://secureframe.com/hub/soc-2/common-criteria
  - https://clerk.com/security
  - https://docs.stripe.com/security?locale=en-GB
  - https://neon.com/guides/hipaa-compliant-applications
---

# SOC 2 Readiness

## Scope and Fit

This playbook orders the vault's SOC 2 skills into a delivery path for a solo or small-team SaaS heading toward a SOC 2 report. It does not, by itself, make an organisation SOC 2 compliant, and it does not issue a report. Only a licensed CPA firm can issue a SOC 2 report.

Use this playbook when a SOC 2 effort is being planned, when a customer asks for a report or a completed questionnaire, or when the team wants to know what "ready" actually means before spending money. Do not use it to claim a report, certification, or compliance status the organisation does not hold, and do not start an observation period before the readiness stages below are complete.

Verify the current Trust Services Criteria reading, vendor report access, and cost quotes with the engaged auditor and the vendors' own pages at engagement time. The 2026-11-02 research run behind this playbook used index fetches for official vendor pages, not a live browser window, and did not fetch Vercel's current official compliance page at all — so Vercel report status, plan gates, and retention limits in this playbook are flagged for re-verification, not treated as primary-source verified.

## Trust Boundary

```text
organisation -> control matrix + system description -> controls + evidence -> auditor (licensed CPA firm) -> report
organisation -> vendors (carve-out) -> vendor reports + dated reviews + complementary controls
customers -> report under NDA + trust pack (SOC 3 summary, never the full report publicly)
```

The auditor is independent. A readiness firm, a compliance platform, or a consultant that prepares the organisation must not also examine it for the same engagement.

## Prerequisites and Approval Boundaries

- Load the SOC 2 skills in order (see Stages below), plus the existing generic skills each stage names — audit log design, incident response, backup and disaster recovery, privacy and data governance, authorization and tenancy design, third-party service evaluation, and privileged access operations. Where a SOC 2 skill says "annex", add only the SOC 2 delta (dated evidence, retention, complementary-controls mapping, restore records) to the generic skill; do not create a second generic skill.
- Accept an ADR covering scope election (which Trust Services Categories, and why), system boundary, carve-out list, auditor tier (boutique versus Big 4, matched to buyer requirements, not prestige), and cost discipline (quotes, not third-party ranges).
- Security-review every configuration change this playbook touches (access, secrets, change control, logging) before it reaches production.
- Engaging an auditor, sharing customer data with a compliance platform, publishing any compliance claim, and changing production access or secret handling are R3.

## Stages

### Stage 1 — Scope and matrix

Load the trust-services-criteria skill and the control-matrix-and-system-description skill. Elect categories by commitment, build the criterion-by-criterion matrix (criterion → control → owner → evidence source), write the system description, choose carve-out for hosted vendors, and reconcile marketing, terms, and the data-processing agreement to the elected scope. Freeze scope at the end of this stage.

### Stage 2 — Vendor reviews

Load the vendor-and-subservice-review skill. Register every vendor that touches customer data or the production path, risk-tier each one, assess new vendors before production data flows, and record a dated review per vendor with report period, exceptions, and complementary controls implemented. Confirm report access plan gates (for example, Clerk Business plan and above, Neon paid customers, Vercel Pro or Enterprise settings) before the observation period, not during it.

### Stage 3 — Controls and cadence

Load the change-control skill and the evidence-operations skill, plus the generic skills they annex: protected main with pull-request-only deploys and ticketed console changes; named accounts with enforced MFA and a break-glass procedure; quarterly diff-based access reviews including API keys, deploy keys, and desktop tokens; secret inventory, scanning, and rotation; append-only audit logging with shipped logs and stated retention; quarterly restore tests to a separate environment with dated records; incident register with notification decisions and postmortems; risk register with owners and reassessment dates; and a truthful, versioned policy pack describing actual practice.

### Stage 4 — Practice period

Run the full cadence once, before the clock starts. Trace a mock sample end to end: ten changes and one quarter of access reviews, from control to evidence, with no gaps. Fix the cadence, then start the observation period. A practice period that finds gaps is a success; an observation period that finds them is an exception.

### Stage 5 — Auditor engagement and observation

Load the auditor-readiness-journey skill. Interview two or three licensed CPA firms, obtain fixed-fee proposals by criteria scope, confirm the observation period with the chosen firm (the "3-month minimum" is unverified industry guidance, not a confirmed rule), and run the observation period with the evidence index maintained continuously. Do not backfill missing evidence, and do not backdate artefacts.

### Stage 6 — Report, trust pack, and maintenance

Share the report under NDA, answer questionnaires from it, and publish only a SOC 3 or trust-centre summary publicly. Issue management bridge letters between reports where needed, and maintain the annual cycle: reviews, risk reassessment, vendor re-reviews, penetration testing where buyers require it, restore tests, and policy re-attestation. Build and maintain the customer trust pack (complementary controls, data-processing agreement, subprocessor list, security page, questionnaire library) without over-claiming at any stage.

## Cost discipline

No AICPA price list exists, and no credible one-person SOC 2 price was found in the research run behind this playbook. Third-party ranges for small-to-mid SaaS (first-year all-in around $20k–$80k in one analysis; boutique auditor fees $10k–$35k versus Big 4 $60k–$150k+; platforms starting around $7k–$12k per year before audit fees) are planning ranges only, for 20–150-person companies, and conflict across sources. Replace every range with two or three fixed auditor quotes before any budget decision. Do not buy a compliance platform before the decision triggers in the catalog shortlist are met, and record any deferral as a dated decision note.

## Verification

Before an auditor engagement, verify: the matrix covers every in-scope criterion with a control, an owner, and an evidence source; the system description matches marketing, terms, and the data-processing agreement; every vendor has a dated review with exceptions and complementary controls; the practice period traced without gaps; and no public or questionnaire language claims a report, certification, or vendor inheritance that does not exist. After the report, verify: the report type, period, scope, and opinion are quoted accurately everywhere they appear, and the next Type II period's cadence is already running.
