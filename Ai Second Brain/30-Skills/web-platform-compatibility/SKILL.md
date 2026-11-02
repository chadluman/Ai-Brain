---
name: web-platform-compatibility
description: Define and verify browser, device, webview, and assistive-technology support for a web project. Use when selecting platform features, setting compatibility policy, planning progressive enhancement, or investigating cross-browser risk; do not treat Baseline status alone as proof of product compatibility.
---

# Web Platform Compatibility

## Outcome

Produce a support policy and verification plan that lets the project use the native web platform confidently without silently excluding required users.

Read [platform evidence](references/platform-evidence.md) before setting a Baseline target or making a compatibility claim.

## Inputs

Identify critical journeys, audience and geography, supported devices and operating systems, browser and webview constraints, assistive technologies, contractual requirements, traffic evidence, offline needs, and the cost of degraded or failed behavior. If analytics are unavailable or inappropriate, state a conservative initial target and how it will be validated.

## Workflow

1. Write a support policy in user terms. Separate fully supported, progressively enhanced, and unsupported environments; do not use "modern browsers" as a requirement.
2. Prefer semantic HTML and native controls, then broadly interoperable CSS and JavaScript. Add custom behavior only where it improves the required journey.
3. Inventory decision-critical platform features. Check current Baseline status and MDN compatibility data, then consult the underlying specification for normative behavior.
4. For a feature with limited availability, choose an acceptable fallback, progressive enhancement, alternate implementation, or reviewed polyfill. Record the user-visible loss and bundle, security, privacy, and maintenance costs.
5. Define representative test environments from the policy. Cover critical journeys, keyboard and assistive-technology behavior, viewport and input modes, slow or unreliable networks, and embedded webviews when applicable.
6. Use cross-browser test evidence and relevant web-platform-tests to investigate interoperability, but reproduce product behavior in the project's supported environments.
7. Add regression checks at the lowest reliable level and schedule review when audience evidence, browser support, or product requirements change.

## Safety and Scope

- Baseline is compatibility evidence, not accessibility, usability, performance, privacy, or security certification.
- Do not add a polyfill, transpiler, compatibility service, browser cloud, or telemetry endpoint until its exact version, permissions, network behavior, data handling, and removal path pass review.
- Do not transmit browsing or user data to a compatibility service without authorization and a privacy review.
- Never discard required users solely because a feature is convenient or fashionable.

## Completion

Deliver the support matrix, feature-risk inventory, fallback decisions, representative test matrix, automated and manual checks, known gaps, evidence dates, owners, and re-evaluation triggers. Label untested compatibility as an assumption.
