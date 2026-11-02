---
name: web-performance-plan
description: Define, measure, diagnose, and maintain user-centered web performance for important journeys. Use for performance budgets, Core Web Vitals work, release gates, or regressions; do not use a single Lighthouse score as proof of real-user performance.
---

# Web Performance Plan

## Outcome

Produce a measurable performance plan tied to real users, critical journeys, representative conditions, release budgets, diagnostic evidence, and ongoing ownership.

Read [metrics and evidence](references/metrics-and-evidence.md) before fixing thresholds or selecting measurement methods.

## Establish the Measurement Model

- Identify critical journeys, page types, user populations, geographies, devices, browsers, networks, cache states, authenticated states, and traffic patterns.
- Set budgets for user outcomes and limiting resources, not only one aggregate score.
- Use current Core Web Vitals as common field indicators: LCP for loading, INP for responsiveness, and CLS for visual stability.
- Segment field results across mobile and desktop and use the 75th percentile for Core Web Vitals evaluation.

Use field data to understand actual experience. Use reproducible lab tests to diagnose and prevent regressions. When field data is unavailable, label lab-based conclusions and plan how representative field evidence will be collected.

## Diagnose Before Optimizing

- LCP: break down server response, resource discovery, resource transfer, and render delay.
- INP: identify the responsible interaction and separate input delay, callback processing, and presentation delay.
- CLS: identify unexpected shifts and the elements, late resources, fonts, or DOM changes causing them.
- Use TTFB, FCP, long tasks, resource timing, JavaScript execution, network payload, memory, and server traces as diagnostics when relevant.
- Inspect complete user flows and post-load states, not only cold navigation to a landing page.

Prioritize changes by user impact, affected traffic, confidence, engineering cost, and risk. Avoid optimizations that damage accessibility, security, correctness, maintainability, or essential product behavior.

## Budgets and Verification

For each budget record the metric, journey, segment, threshold, percentile, test or field method, environment, owner, and release consequence. Include variance and repeated runs for lab measurements.

If real-user monitoring or analytics is proposed, perform privacy, consent, data-minimization, retention, telemetry, and dependency review before adding a library or endpoint.

## Completion

Deliver the baseline, budgets, field/lab distinction, bottleneck evidence, prioritized actions, regression gates, monitoring plan, data limitations, and re-evaluation triggers. A Lighthouse score may support diagnosis but must not be the sole performance acceptance criterion.

