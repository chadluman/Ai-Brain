# App Store Policy Evidence

Verified: 2026-10-22

## Official Store Sources

- [Apple App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/) is a living rules source covering completeness, metadata, beta distribution, payments, privacy, accounts, content, and reviewer access. Recheck it for every submission.
- [Apple: Submitting to the App Store](https://developer.apple.com/app-store/submitting/) lists build, product-page, privacy, accessibility, rating, availability, and submission preparation.
- [Apple App Store Connect upload builds](https://developer.apple.com/help/app-store-connect/manage-builds/upload-builds/) provides current supported build and upload toolchain requirements and role boundaries.
- [Apple TestFlight overview](https://developer.apple.com/help/app-store-connect/test-a-beta-version/testflight-overview/) documents beta information, review, tester access, feedback, metrics, expiration, and stopping a test.
- [Google Play target API requirements](https://support.google.com/googleplay/android-developer/answer/11926878) gives current submission and discoverability deadlines by Android target API and product class. Dates are volatile and must not be copied into undated policy.
- [Google Play Data safety](https://support.google.com/googleplay/android-developer/answer/10787469) requires accurate declarations for application and third-party SDK data behavior and explains testing-track scope, policy status, and continuing accuracy.
- [Google Play pre-launch reports](https://support.google.com/googleplay/android-developer/answer/9842757) documents automated artifact testing and safe test-account expectations before release.

## Decision Boundaries

- Official help can describe platform policy but does not interpret local law or guarantee approval. Regulated, children, finance, health, gambling, content, tax, and privacy questions may require qualified review.
- Requirements differ by store, product type, target, region, account program, and date. Record the exact scope next to every finding.
- Privacy and Data safety declarations include third-party SDK behavior. Vendor disclosures are evidence to verify, not a substitute for inspecting the exact integrated version and observed data flow.
- Beta and pre-launch services transmit builds and may process credentials, logs, screenshots, video, feedback, crash data, and tester information. Apply provider and data review before use.
- An accepted release can become noncompliant after application, SDK, policy, target API, metadata, backend, or data-use changes. Maintain the evidence after launch.
