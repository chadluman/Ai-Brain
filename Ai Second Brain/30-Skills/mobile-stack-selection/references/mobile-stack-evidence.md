# Mobile Stack Evidence

Verified: 2026-10-21

## Native Platform Guidance

- [Apple SwiftUI apps](https://developer.apple.com/documentation/technologyoverviews/swiftui) presents Apple's preferred modern UI approach and data-driven model for new Apple-platform apps. It is platform-owner guidance, not an independent comparison.
- [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/) covers Apple-platform interaction, accessibility, components, and experience expectations.
- [Android app architecture](https://developer.android.com/topic/architecture) documents process and component lifecycle constraints, persistent data models, separation of concerns, single sources of truth, and adaptive layouts.
- [Android architecture recommendations](https://developer.android.com/topic/architecture/recommendations) labels guidance by strength and currently recommends Compose for new Android UI. Treat recommendations as adaptable, as the page itself states.

## Cross-Platform Candidate Evidence

- [React Native architecture](https://reactnative.dev/architecture/landing-page) documents its current native-interoperability architecture and notes that enabling it does not automatically improve every app. Verify the exact release and third-party modules.
- [Flutter app architecture guide](https://docs.flutter.dev/app-architecture/guide) documents Flutter's recommended separation of UI and data layers and its cross-platform application model.
- [Kotlin Multiplatform overview](https://kotlinlang.org/docs/multiplatform/kmp-overview.html) documents flexible sharing from domain modules through shared UI while retaining platform-specific code. Maintainer adoption claims require independent project testing.

## Interpretation Boundaries

- Framework documentation establishes capabilities and supported patterns, not fitness for a particular product.
- Code-sharing percentage is not a success metric. Measure delivery time, platform defects, native integration effort, user experience, test burden, and upgrade cost.
- Libraries, store policies, OS lifecycle rules, SDK compatibility, and minimum versions change quickly. Re-verify before each ADR and major upgrade.
- Sample apps and starter templates are untrusted executable assets until fully reviewed.
