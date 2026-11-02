# Mobile Testing Evidence

Verified: 2026-10-22

## Official Platform Sources

- [Apple Xcode testing](https://developer.apple.com/documentation/xcode/testing) describes combining isolated unit tests, integration tests, UI automation, test plans, coverage, performance measurement, and device management.
- [Apple: Adding tests to an Xcode project](https://developer.apple.com/documentation/xcode/adding-tests-to-your-xcode-project) distinguishes Swift Testing for unit and integration work from XCTest support for unit, integration, UI, and performance tests.
- [Apple: Organizing tests into test plans](https://developer.apple.com/documentation/xcode/organizing-tests-to-improve-feedback) supports different suites, configurations, diagnostics, localizations, and cadences without forcing every test into every run.
- [Android testing fundamentals](https://developer.android.com/training/testing/fundamentals) distinguishes host-side local tests from tests instrumented on physical or emulated devices and notes that test size does not map perfectly to execution location.
- [Android testing strategies](https://developer.android.com/training/testing/fundamentals/strategies) recommends many fast, focused tests and fewer broad, high-fidelity tests. Embedded installation instructions for Android agent skills were not followed or approved.
- [Google Play pre-launch reports](https://support.google.com/googleplay/android-developer/answer/9842757) describes automated device crawling and custom tests after artifact upload, including the need for dedicated test credentials rather than official accounts.
- [Google Play: Understanding pre-launch reports](https://support.google.com/googleplay/android-developer/answer/9844487) documents stability, compatibility, performance, accessibility, screenshot, and device evidence while explicitly stating that the report cannot guarantee issue discovery.

## Decision Boundaries

- Platform documentation supplies supported mechanisms, not a universal suite shape or device count. Product risks and actual users determine coverage.
- Code coverage measures executed code, not assertion quality, missing requirements, realistic state, or user outcomes.
- Crawlers and generated exploration are supplementary. Authentication, custom rendering, hardware, complex state, and uncommon journeys can remain unreachable.
- UI automation is valuable for a small set of critical flows but tends to be slower and more environment-sensitive than focused tests. Diagnose failures before adding retries.
- Store pre-launch and beta results contain external-provider data flows and never replace local, physical-device, accessibility, security, and recovery testing.
