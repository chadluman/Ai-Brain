# Mobile Performance Evidence

Verified: 2026-10-22

## Official Platform Sources

- [Apple: Improving app performance](https://developer.apple.com/documentation/xcode/improving-your-app-s-performance) describes a continuous cycle of field evidence, measurement, targeted change, and re-observation across launch, responsiveness, disk, memory, and energy.
- [Apple: Monitoring app performance with MetricKit](https://developer.apple.com/documentation/metrickit/monitoring-app-performance-with-metrickit) documents daily real-device metrics and diagnostics for CPU, memory, network, launch, disk, crashes, and hangs with environment context.
- [Apple MetricKit](https://developer.apple.com/documentation/metrickit) defines platform and OS availability and notes that supported metrics differ for visionOS and newer API generations.
- [Android vitals](https://developer.android.com/topic/performance/vitals/) documents user-perceived crash and ANR rates, battery, memory, app-version, device, and store-visibility metrics. Thresholds and planned enforcement dates must be rechecked rather than copied into durable policy.
- [Android Baseline Profiles](https://developer.android.com/topic/performance/baselineprofiles/overview) documents profile-guided ahead-of-time optimization for selected critical paths and recommends measuring startup and runtime effects for the actual release.

## Decision Boundaries

- MetricKit and Android vitals are aggregated field signals subject to OS support, user settings, eligibility, delivery delay, sampling, and platform definitions. Missing data is not proof of good performance.
- A store bad-behavior threshold is an external enforcement boundary, not an acceptable user-experience target.
- A mean hides slow users. Record distributions and affected populations, including low-memory devices, poor networks, large data sets, and accessibility settings.
- Baseline or startup profiles can improve selected paths but become release inputs that need regeneration, testing, and version control when code or journeys change.
- Debug builds, emulators, clean data, warm caches, and unconstrained power can misrepresent launch, compilation, storage, background, thermal, and battery behavior.
