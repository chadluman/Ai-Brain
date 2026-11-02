---
name: mobile-release-operations
description: Plan and review iOS and Android signing, store accounts, build identity, test tracks, review materials, staged rollout, crash monitoring, rollback, policy, privacy, and update continuity. Use after a mobile stack is selected and before distributing any build.
---

# Mobile Release Operations

## Outcome

Create a reproducible, least-privilege mobile release path that protects long-lived signing and account identity, tests the actual release artifact, satisfies current store requirements, stages exposure, and preserves the ability to update or recover the app.

## Required Inputs

- platforms, distribution channels, app identifiers, regions, audience, and release owner
- developer organization, legal entity, store accounts, roles, billing, tax, and recovery contacts
- signing model, certificates, keys, profiles, secrets, CI, and artifact provenance
- supported OS and devices, permissions, privacy declarations, content, commerce, and age needs
- test cohorts, review credentials, rollout stages, health signals, support, and incident plan

## Safety and Permission Constraints

- Treat signing keys, store ownership, bundle or package identifiers, and application transfer as long-lived critical assets. Store no private keys or secret values in the vault.
- Use organization-owned accounts, phishing-resistant MFA where available, role separation, protected recovery, audited CI, and the minimum store permissions.
- Verify current Apple and Google requirements immediately before every submission; policies, declarations, SDK deadlines, commerce, privacy, and regional rules change.
- Store account creation, agreement acceptance, payment, signing-key change, production upload, review submission, public release, transfer, or app deletion is R3 and requires immediate authorization and verified recovery.
- Test the signed release artifact and production-like backend, not only a debug build. Do not expose real user data to testers without an approved plan.

## Workflow

1. Inventory organization ownership, account roles, identifiers, signing assets, environments, service endpoints, entitlements, permissions, and third-party SDK declarations.
2. Define signing and key custody for each channel, including creation, CI access, backup or provider custody, rotation or reset, compromise response, and update continuity.
3. Pin the build environment and produce a traceable versioned release artifact with source revision, dependency lock, configuration identity, symbols, checksums, and SBOM where useful.
4. Review current store policy, privacy and data declarations, permissions, commerce, content rating, age, export, region, accessibility, screenshots, metadata, support, and account-deletion requirements.
5. Test install, upgrade from supported versions, fresh state, migration, offline behavior, denied permissions, deep links, notifications, background work, account recovery, deletion, and uninstall or reinstall on representative devices.
6. Use internal and closed tracks first. Provide reviewers complete access instructions and safe test accounts without hidden production privilege.
7. Predefine staged exposure, crash and hang thresholds, backend compatibility, support coverage, pause, halt, and remediation. Store rollback often means stopping rollout and shipping a corrected version, not instant binary reversal.
8. Submit only with authorization, monitor review communications, preserve the submitted artifact and metadata, then verify listing, install, sign-in, purchase if used, links, and production service health after release.
9. Protect update continuity, monitor policy and SDK deadlines, rehearse compromised upload credentials, maintain reviewer and support contacts, and retire old backend contracts only after supported app adoption allows it.

## Required Output

- account, role, identifier, signing, recovery, and ownership inventory
- reproducible build and artifact-provenance record
- current platform-policy and declaration checklist with verification dates
- device, upgrade, permission, integration, accessibility, and failure test evidence
- test-track, review, staged-rollout, monitoring, pause, and remediation plan
- support, incident, backend-compatibility, key-compromise, and continuity runbooks

## Completion Gate

Do not call a mobile release ready until account recovery and signing continuity are verified, the exact signed artifact passes representative upgrade and critical-journey tests, current declarations match observed behavior, and staged rollout has accountable stop and remediation paths.

## Conditional Reference

Read [Mobile Release Evidence](references/mobile-release-evidence.md) when preparing Apple or Google signing, review, test tracks, or staged distribution.
