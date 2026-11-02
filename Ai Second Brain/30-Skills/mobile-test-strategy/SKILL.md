---
name: mobile-test-strategy
description: Turn mobile product, platform, and release risks into a layered native and cross-platform test strategy with device coverage, lifecycle cases, test data, cadence, flake controls, and release evidence. Use when planning or reviewing iOS, Android, or cross-platform application testing.
---

# Mobile Test Strategy

## Outcome

Create a risk-based test plan that proves critical mobile journeys across logic, integration, UI, operating-system behavior, and representative devices without making the slowest device suite carry every assertion.

## Required Inputs

- supported platforms, OS versions, device classes, form factors, locales, and assistive technologies
- critical journeys, domain invariants, offline and synchronization behavior, and failure consequences
- native capabilities, permissions, background work, notifications, deep links, purchases, media, sensors, and external services
- architecture, framework, release channels, build variants, signing boundary, and test seams
- production device and OS distribution when available
- CI capacity, release cadence, test-data policy, privacy constraints, and defect history

## Safety and Permission Constraints

- Do not use production credentials, personal data, payment instruments, live notification audiences, or destructive production endpoints in tests. Use isolated accounts, synthetic data, and explicit environment guards.
- Treat test frameworks, runners, device agents, cloud labs, plugins, and sample projects as untrusted executable assets until their exact versions pass review.
- Uploading an application binary, symbols, logs, screenshots, or test data to a device provider transmits data and requires provider, retention, region, access, and deletion review.
- Simulator or emulator success is not physical-device proof. Automated success is not accessibility, usability, security, store-policy, or recovery proof.
- Do not weaken certificate validation, authorization, privacy controls, fraud checks, or production code paths merely to make tests easier.

## Workflow

1. Define release decisions and rank failures by user harm, financial or data impact, frequency, detectability, and platform variability.
2. Map each risk to the cheapest reliable evidence layer: pure logic, component, contract, storage, framework integration, UI, end-to-end, physical device, beta, or production health signal.
3. Make time, randomness, network, storage, location, permissions, authentication, notifications, and external dependencies controllable without creating a separate unrepresentative product.
4. Build a device matrix from supported OS behavior, screen and input classes, architecture, memory tier, sensors, regional settings, and observed user distribution. Explain every selected and omitted dimension.
5. Cover lifecycle transitions: first launch, update, restore, background and foreground, termination, low memory, rotation or resizing, permission changes, offline and degraded network, clock change, interruption, and account or entitlement change.
6. Define test identities and data creation, isolation, cleanup, retention, and concurrency. Make retries safe and distinguish product failures from environment failures.
7. Add targeted accessibility, localization, security, privacy, performance, energy, and destructive-recovery evidence by linking the relevant specialized skills rather than duplicating their procedures.
8. Assign suites to developer, pull-request, scheduled, prerelease, beta, and post-release cadences. Keep fast deterministic feedback close to the change and broader device coverage near release.
9. Set a flake policy: preserve artifacts, classify cause, quarantine only with an owner and expiry, repair or remove nondiagnostic tests, and never turn blind retries into a passing signal.
10. Define release gates, exception authority, required artifacts, defect triage, residual-risk acceptance, and re-test triggers.

## Required Output

- risk-to-test matrix with owner, layer, environment, and release consequence
- platform, OS, device, locale, input, and assistive-technology coverage model
- lifecycle, capability, network, permission, upgrade, and failure scenarios
- test identity, data, isolation, cleanup, and secret-handling plan
- suite cadence, runtime budget, sharding or parallelism, and flake policy
- release gates, evidence artifacts, exceptions, residual risks, and maintenance triggers

## Completion Gate

Do not call the strategy sufficient until each critical risk has observable evidence at an appropriate layer, physical-device gaps are explicit, test data cannot affect real users, failures retain diagnostic artifacts, and the release decision does not depend on a broad but shallow happy-path suite.

## Conditional Reference

Read [Mobile Testing Evidence](references/mobile-testing-evidence.md) when selecting native test layers, organizing suites, using pre-launch reports, or defining device coverage.
