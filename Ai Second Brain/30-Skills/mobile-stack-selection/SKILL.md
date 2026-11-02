---
name: mobile-stack-selection
description: Select or review native iOS and Android, shared-logic, or cross-platform mobile architecture based on product journeys, platform APIs, offline behavior, performance, accessibility, team skills, testing, lifecycle, and store delivery. Use before choosing SwiftUI, Android native, Kotlin Multiplatform, React Native, Flutter, or a web-based wrapper.
---

# Mobile Stack Selection

## Outcome

Choose a mobile architecture and code-sharing boundary that meets platform experience and lifecycle requirements without hiding unsupported native work or multiplying long-term maintenance risk.

## Required Inputs

- target platforms, minimum OS versions, devices, form factors, countries, and store distribution
- critical journeys, performance, startup, animation, accessibility, and design-system expectations
- camera, media, maps, location, Bluetooth, biometrics, payments, background, notifications, widgets, and deep-link needs
- offline, synchronization, conflict, local-encryption, and account-recovery requirements
- team languages and platform expertise, schedule, budget, expected lifespan, and release capacity
- existing web or native code, required SDKs, library support, and portability goals

## Safety and Permission Constraints

- Treat framework packages, native modules, plugins, templates, build tools, signing tools, and third-party SDKs as executable assets requiring exact-version review.
- Do not assume shared UI means identical behavior is appropriate. Preserve platform navigation, accessibility, permissions, privacy, and lifecycle expectations.
- Mobile processes can be suspended or killed; background work and notifications are constrained and not guaranteed. Persist recoverable state deliberately.
- Minimize device permissions and data collection. Explain requests in context and handle denial or revocation gracefully.
- Signing, store accounts, certificates, device registration, production push credentials, beta distribution, and store submission are R3 and require immediate authorization.

## Workflow

1. Build a capability matrix for every target: platform API, lifecycle, background, offline, UI, accessibility, performance, SDK, and store requirement.
2. Compare the smallest credible options:
   - separate native apps for deepest platform fit and independent evolution;
   - shared business logic with native UI when domain reuse is high but platform experience differs;
   - cross-platform UI when journeys and required integrations are well supported;
   - responsive web or PWA when install and native capability requirements are modest.
3. Score exact current candidates on coverage, native escape hatches, library health, build and debugging, update cadence, performance, binary size, accessibility, automated testing, team fit, security, and exit cost.
4. Mark every platform-specific component and ownership boundary. Verify critical third-party SDK support for the exact framework and architecture versions.
5. Design state and data layers for process death, intermittent networks, retries, conflicts, schema migration, logout, revocation, and device loss.
6. Define navigation, deep links, permissions, notifications, background tasks, lifecycle, app updates, and backward-compatible server contracts per platform.
7. Build a thin proof of concept through the hardest native integration and a representative journey on real low-end and current devices, including accessibility and offline failure.
8. Define unit, integration, UI, device, performance, accessibility, network, upgrade, and store-release testing.
9. Record the decision and migration boundary in an ADR, including how shared modules or screens can be replaced by native code.

## Required Output

- platform capability and constraint matrix
- native and cross-platform candidate comparison with dated versions
- selected code-sharing boundary and platform-specific ownership
- lifecycle, offline, permission, notification, deep-link, and update design
- proof-of-concept results on representative devices
- build, signing, testing, release, rollback, and store-review plan
- migration and framework-exit strategy

## Completion Gate

Do not call the stack selected until the hardest native capability, process-death recovery, offline behavior, performance, and accessibility have been tested on representative real devices. Store publication remains separately authorized.

## Conditional Reference

Read [Mobile Stack Evidence](references/mobile-stack-evidence.md) before comparing native or cross-platform architecture claims.
