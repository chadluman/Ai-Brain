# Web Performance Metrics and Evidence

Verified 2026-10-21. Core Web Vitals can evolve; recheck before setting a new baseline.

## Current Core Web Vitals

Google's [Web Vitals](https://web.dev/articles/vitals) guidance identifies the current stable set and recommends evaluating the 75th percentile, segmented across mobile and desktop:

| Metric | Good threshold |
|---|---:|
| Largest Contentful Paint (LCP) | 2.5 seconds or less |
| Interaction to Next Paint (INP) | 200 milliseconds or less |
| Cumulative Layout Shift (CLS) | 0.1 or less |

The [threshold methodology](https://web.dev/articles/defining-core-web-vitals-thresholds) documents the user-experience and achievability reasoning and was last updated 2025-05-07 when verified.

## Measurement Roles

- [Optimize LCP](https://web.dev/articles/optimize-lcp) recommends starting with real-user evidence when available and using lab tools for diagnosis.
- [Optimize INP](https://web.dev/articles/optimize-inp) describes field identification followed by lab reproduction and separates interaction latency into input delay, processing, and presentation delay.
- [Lighthouse](https://github.com/GoogleChrome/lighthouse) provides lab diagnostics. Navigation, timespan, and snapshot modes cover different portions of a user flow; no one mode proves overall quality.
- [`web-vitals`](https://github.com/GoogleChrome/web-vitals) is Google's measurement library for Web Vitals. It is a candidate dependency, not pre-approved code; review its exact version, privacy impact, telemetry destination, and integration before use.

## Interpretation

- Treat the published “good” thresholds as a common experience baseline, not necessarily the project's final performance budget.
- Record page/journey, device class, network, browser, geography, cache state, sample period, percentile, and dataset limitations.
- Distinguish field measurement from synthetic lab measurement and do not compare unlike populations as if they were equivalent.

