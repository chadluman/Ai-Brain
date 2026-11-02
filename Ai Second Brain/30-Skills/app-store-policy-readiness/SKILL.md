---
name: app-store-policy-readiness
description: Map an Apple App Store or Google Play product to current submission, metadata, privacy, account, payment, content, SDK, target-platform, reviewer-access, and maintenance requirements. Use before mobile architecture commitments, beta distribution, store submission, or a material policy-sensitive release.
---

# App Store Policy Readiness

## Outcome

Produce a dated, product-specific store-readiness matrix that connects current official rules to application behavior, evidence, ownership, and release gates without treating prior approval as permanent compliance.

## Required Inputs

- target stores, platforms, storefronts, countries, user ages, and release date
- product journeys, accounts, user-generated content, communication, AI, health, finance, children, regulated features, and physical or digital goods
- data inventory, third-party SDKs, permissions, tracking, privacy policy, retention, export, and deletion behavior
- payment, subscription, entitlement, advertising, promotions, and external-link behavior
- minimum and target OS or SDK, build toolchain, signing, encryption, device requirements, and distribution tracks
- listing text, screenshots, previews, ratings, accessibility claims, support contacts, review access, and backend dependencies

## Safety and Permission Constraints

- Store rules, deadlines, regional programs, and legal obligations change. Verify official live sources for the exact store, region, product, and submission date; do not rely on this skill or a previous approval as legal advice.
- Do not create developer accounts, accept agreements, enter tax or banking data, upload builds, invite testers, provide credentials, submit declarations, or publish without explicit authorization at the consequential step.
- Never store production, reviewer, signing, banking, tax, or account secret values in the vault. Use a secret manager and a least-privilege, monitored demo environment.
- Declarations must describe the actual application and every included SDK. Do not hide collection, manipulate consent, misstate accessibility, disguise payments, or create temporary review-only behavior.
- Store approval is not proof of security, privacy, accessibility, legal compliance, reliability, or honest product behavior.

## Workflow

1. Freeze the release candidate, store, storefronts, intended submission date, app and account identifiers, build toolchain, target SDK, and feature set.
2. Build a policy applicability map across safety, completeness, content, accounts, user-generated content, payments, subscriptions, advertising, privacy, permissions, children, regulated domains, AI, and external services.
3. Trace every data type and SDK from collection through use, sharing, retention, deletion, and user control. Reconcile application behavior, privacy policy, Apple privacy details, Google Data safety, permission prompts, and account deletion.
4. Verify current toolchain, target API or OS, binary, signing, encryption, device-capability, architecture, and upload deadlines from official sources.
5. Compare the complete purchase and entitlement journey with current store rules by product type and region. Record enrolled alternative programs and conditions rather than assuming an exception.
6. Audit listing metadata, screenshots, previews, ratings, accessibility claims, support and policy URLs, pricing, localized disclosures, and release notes against the actual build.
7. Prepare reviewer access using a least-privilege synthetic account or approved demo mode, stable backend, seeded non-sensitive state, test instructions, and support ownership. Keep secret values outside the vault.
8. Run on-device functional, accessibility, privacy, security, performance, and failure checks. Treat automated pre-launch or store review as additional evidence only.
9. Record every rule with source URL, verification date, evidence, owner, status, exception, and remediation. Stop submission on material contradictions or missing declarations.
10. Define monitoring for policy notices, SDK changes, target deadlines, broken backends, stale metadata, privacy drift, removed features, and continuing support after release.

## Required Output

- dated store, region, product, and release applicability matrix
- feature, data, SDK, permission, payment, and account evidence map
- toolchain, target platform, signing, encryption, and upload requirement check
- listing, rating, accessibility, privacy, support, and reviewer-access checklist
- gaps, owners, remediation, exceptions, and submission stop conditions
- post-release policy monitoring and re-review triggers

## Completion Gate

Do not call the release store-ready until the exact candidate matches its declarations and listing, current target and toolchain requirements are met, reviewer access uses safe synthetic state, payment and deletion paths are testable, every material policy has dated evidence and an owner, and consequential submission remains explicitly authorized.

## Conditional Reference

Read [App Store Policy Evidence](references/app-store-policy-evidence.md) when establishing current Apple or Google submission, privacy, testing, target-platform, and review boundaries.
