# Mobile Device Lab Evidence

Verified: 2026-10-22

## Official Platform and Provider Sources

- [Apple Xcode Cloud](https://developer.apple.com/xcode-cloud/) describes parallel testing on a small frequent device set and a broader, less frequent configuration set. It is a hosted Apple service, not a universal default.
- [Apple TestFlight](https://developer.apple.com/testflight/) supports distributing beta builds to internal and external testers and collecting feedback before publication.
- [Android build-managed devices](https://developer.android.com/studio/test/managed-devices) defines reproducible virtual or remote physical device configurations, lifecycle management, sharding, and resource tradeoffs from Gradle.
- [Android testing across screen sizes](https://developer.android.com/training/testing/different-screens/tools) recommends matching tests to relevant screens and using managed devices or a device farm for hardware not locally available.
- [Firebase Test Lab](https://firebase.google.com/docs/test-lab/) describes hosted Android and iOS device matrices, supported test forms, CI integration, artifacts, and the boundary that it is not for backend load testing.
- [Firebase Test Lab deprecation FAQ](https://firebase.google.com/docs/test-lab/migrate-faq) states that Test Lab executions are supported until September 30, 2027 and directs migration toward Google Cloud Developer Device Platform.
- [Firebase Test Lab migration guidance](https://firebase.google.com/docs/test-lab/migrate) states that the replacement platform is in preview at verification time and that Android Device Streaming continues.
- [Google Play pre-launch reports](https://support.google.com/googleplay/android-developer/answer/9842757) adds automated store-side device evidence but has capacity, crawl, credential, and application-shape limits.

## Decision Boundaries

- Product names, lifecycle dates, preview status, devices, quotas, prices, retention, regions, and supported frameworks can change. Recheck at proof and purchase time.
- Hosted device testing transmits at least the application binary and test instructions and may transmit credentials, symbols, screenshots, video, logs, and crash data. Classify and minimize each item.
- Simulators and emulators provide fast, clean, reproducible feedback but do not reproduce every radio, sensor, thermal, memory, GPU, manufacturer, or installation behavior.
- Beta cohorts add real environments and human behavior but are not deterministic test automation and introduce consent, support, privacy, access, and expiration obligations.
- A provider migration announcement is a concrete exit trigger. Do not build a new long-lived workflow around a deprecated surface without an accepted transition plan.
