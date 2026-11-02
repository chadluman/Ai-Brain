---
name: mobile-performance-energy-quality
description: Define, measure, diagnose, and maintain mobile launch, responsiveness, frame, memory, storage, network, background, battery, crash, and hang quality. Use when setting mobile performance budgets, investigating regressions, preparing a release, or interpreting field health signals.
---

# Mobile Performance and Energy Quality

## Outcome

Create a journey-centered performance and resource plan that combines repeatable laboratory measurements with privacy-conscious field evidence and prevents optimization from degrading correctness, accessibility, or battery life.

## Required Inputs

- critical journeys and user-visible latency, smoothness, stability, and offline expectations
- supported platforms, OS versions, devices, memory tiers, networks, locales, and thermal conditions
- startup modes, background tasks, media, graphics, storage, sync, and external service behavior
- current measurements, field diagnostics, crash and hang evidence, release history, and known regressions
- telemetry consent, sampling, retention, access, symbolication, and cost constraints
- release gates, owners, target population, and acceptable tradeoffs

## Safety and Permission Constraints

- Performance telemetry can expose device, version, route, experiment, usage, network, and diagnostic data. Minimize, aggregate, restrict, retain briefly, and never capture content or identifiers without a justified purpose and authorization.
- Recheck platform metric definitions, store thresholds, collection eligibility, and OS availability. A current store threshold is not a timeless product budget.
- Do not disable accessibility, encryption, validation, synchronization safety, logging needed for incidents, or user controls to improve a benchmark.
- Use representative devices and release-equivalent builds. Simulator, debug, warm-cache, unconstrained-network, or single-run measurements cannot prove field performance.
- Profilers, agents, benchmark libraries, and optimization plugins remain executable assets requiring exact-version review.

## Workflow

1. Define performance in user terms per critical journey: cold and warm launch, input response, scrolling and animation, loading, save or sync completion, background completion, and recovery.
2. Set measurable budgets and guardrails for latency distributions, hangs or ANRs, crashes, frames or hitches, memory, disk, network, CPU or GPU, thermal pressure, and energy where relevant.
3. Establish a reproducible matrix of release build, device, OS, data size, account state, network, cache, battery, thermal state, and repetitions. Record raw results and environment.
4. Instrument only the boundaries needed to connect symptoms to journeys and versions. Preserve privacy and distinguish app work from network, provider, OS, and device effects.
5. Measure a baseline before changing code. Use platform profilers and traces to find the dominant cause rather than optimizing from intuition.
6. Change one material factor, remeasure the same distribution, and check correctness, accessibility, visual quality, data integrity, battery, and lower-tier devices for regressions.
7. Use platform-supported build optimizations only with representative before-and-after evidence and compatibility tests. Record generated profiles or configuration as release inputs.
8. Compare lab results with aggregated field health by app version, OS, device or memory tier, and journey. Account for eligibility, sampling, delayed reports, and survivorship bias.
9. Gate releases on significant regressions and severe stability or resource failures. Define rollback, feature-disable, triage, and escalation paths.
10. Trend budgets over releases and revisit them when product journeys, devices, OS behavior, data scale, dependencies, or store metrics change.

## Required Output

- journey budgets and stability or resource guardrails
- representative measurement matrix and reproducible baseline
- instrumentation and privacy plan
- trace or diagnostic evidence, cause hypothesis, and before-and-after distributions
- lab-to-field comparison with eligibility and sampling limitations
- release gates, rollback or mitigation, owners, and re-review triggers

## Completion Gate

Do not claim an improvement until a release-equivalent build shows repeatable distribution-level gains on representative physical devices, field signals are consistent where available, and correctness, accessibility, security, battery, and constrained-device guardrails remain intact.

## Conditional Reference

Read [Mobile Performance Evidence](references/mobile-performance-evidence.md) when selecting Apple or Android metrics, interpreting store health, or considering build-time optimization.
