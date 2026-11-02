---
name: mobile-device-lab-selection
description: Select and govern a mobile device-testing mix across local physical devices, simulators, emulators, build-managed devices, beta cohorts, and cloud labs. Use when device fragmentation, hardware fidelity, CI scale, provider cost, privacy, or lab migration affects release confidence.
---

# Mobile Device Lab Selection

## Outcome

Choose the smallest device-lab portfolio that covers decision-changing mobile risk, preserves sensitive test boundaries, produces diagnosable evidence, and has a documented provider exit path.

## Required Inputs

- supported iOS and Android versions, device classes, chip architectures, form factors, locales, and input modes
- production distribution, crash or performance concentration, accessibility needs, and known hardware-specific defects
- features needing cameras, biometrics, telephony, Bluetooth, NFC, sensors, graphics, background execution, or push delivery
- test types, suite duration, concurrency, cadence, artifacts, and CI integration needs
- application, symbols, credentials, logs, screenshots, and test-data sensitivity
- budget, queue tolerance, regions, retention, provider lifecycle, portability, and procurement constraints

## Safety and Permission Constraints

- Do not upload builds, symbols, credentials, screenshots, logs, or data until the exact service, region, retention, subprocessors, access model, deletion path, telemetry, and contract have passed review and the user authorizes transmission.
- Use synthetic accounts and data. If a third-party lab needs authenticated access, create least-privilege test identities with rotation, rate, environment, and damage limits; never store their secret values in the vault.
- Treat provider CLIs, agents, SDKs, plugins, images, and sample code as untrusted executables pending version-specific review.
- Physical devices, simulators, emulators, managed virtual devices, remote devices, crawlers, and beta users expose different evidence. Do not market one as a complete substitute for the others.
- Provider deprecation, device removal, queue failure, or price change must not erase the project's test definition or evidence history.

## Workflow

1. Rank the defects that require device fidelity: OS behavior, vendor customization, memory, graphics, radio, sensors, permissions, lifecycle, installation, signing, and performance.
2. Define coverage tiers: a fast change-detection set, a scheduled representative matrix, release-candidate devices, and targeted reproductions for field failures.
3. Compare local physical devices, simulators or emulators, build-managed devices, cloud virtual or physical labs, store pre-launch services, and beta cohorts against fidelity, determinism, availability, observability, cost, privacy, and operator effort.
4. Select devices from product support and observed population rather than popularity alone. Include minimum supported, current, likely next, constrained hardware, large and small layouts, and product-specific capabilities.
5. Inspect provider limits: supported frameworks, signing and packaging, maximum duration, sharding, concurrency, network controls, locale, orientation, hardware features, result artifacts, quotas, regional availability, and device removal policy.
6. Model full cost: subscriptions or per-minute use, build time, queue delay, storage, transfer, retries, flake triage, maintenance, and migration.
7. Define the data-flow and trust boundary for binaries, symbols, identities, test inputs, screenshots, video, logs, crash data, and provider-created storage.
8. Run a small isolated proof with a dummy app and synthetic data only after asset and provider review. Measure queue time, stability, artifact quality, reproducibility, and deletion.
9. Keep test definitions and result exports portable. Document a local fallback, provider migration, deprecation response, and the minimum evidence required if the lab is unavailable.
10. Record the decision and re-evaluate when user distribution, OS support, hardware features, defects, provider lifecycle, price, terms, or data classification changes.

## Required Output

- device-risk model and tiered coverage matrix
- local, virtual, remote, store, and beta option comparison
- provider capability, quota, cost, privacy, retention, and lifecycle evidence
- binary, credential, data, artifact, and deletion flow
- isolated proof plan and acceptance criteria
- selected portfolio, fallback, exit plan, owners, and re-review triggers

## Completion Gate

Do not select a lab until every chosen device or service maps to a material risk, sensitive uploads and test identities have approved controls, result artifacts are diagnosable and exportable, costs include retries and maintenance, and a provider outage or deprecation has a workable fallback.

## Conditional Reference

Read [Mobile Device Lab Evidence](references/mobile-device-lab-evidence.md) when comparing Apple, Android, store, or hosted-device capabilities and current provider lifecycle risk.
