# Mobile Release Evidence

Verified: 2026-10-21

## Platform Sources

- [Apple App Review](https://developer.apple.com/app-store/review/) routes to current preparation, submission, common issues, agreements, and review criteria.
- [Apple App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/) are the current platform-owner criteria for safety, performance, business, design, and legal review. They can change and must be checked at submission time.
- [Android app signing](https://developer.android.com/studio/publish/app-signing) explains mandatory signing, Play App Signing, the distinction between app-signing and upload keys, update continuity, compromise handling, and multi-store considerations.
- [Google Play test tracks](https://support.google.com/googleplay/android-developer/answer/9845334) describes internal, closed, and open testing and current account-specific prerequisites.
- [Android publishing](https://developer.android.com/studio/publish) covers release configuration, signing, release-artifact testing, and distribution options.

## Decision Boundaries

- Platform-owner guidance is authoritative for its store but not proof that a product is safe, accessible, lawful, or appropriate in every region.
- Store review can be delayed or rejected, and an approved build can still fail in production. Plan schedule and operations without assuming review timing or quality assurance.
- Mobile clients update slowly. Backend and data contracts may need compatibility across multiple released versions and offline devices.
- A staged rollout limits exposure but does not provide an instant downgrade for devices that installed a bad version. Keep server-side mitigation and a corrected-build path.
