# Monetization Evidence

Verified: 2026-10-21

## Primary Provider and Regulatory Sources

- [Apple: Choosing a business model](https://developer.apple.com/app-store/business-models/) describes free, freemium, paid, and paymium approaches and emphasizes aligning the model with goals and market expectations before app design is fixed.
- [Apple App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/) are the live source for App Store review and business rules. Recheck the applicable sections and regional terms immediately before design approval or submission.
- [Google Play payments policy](https://support.google.com/googleplay/android-developer/answer/9858738) defines current billing-system requirements, exclusions, eligible regional programs, disclosure expectations, and virtual-currency boundaries.
- [Google Play subscription policy](https://support.google.com/googleplay/android-developer/answer/9900533) requires truthful recurring value, clear price and renewal terms, and non-manipulative purchase experiences.
- [Google Play subscription lifecycle](https://developer.android.com/google/play/billing/lifecycle/subscriptions) documents server-verified subscription states, notifications, acknowledgement, entitlement, payment failure, expiry, and refund behavior.
- [Google Play backend integration](https://developer.android.com/google/play/billing/backend) calls for server-side lifecycle synchronization, duplicate-event handling, fraud controls, catalog management, and reconciliation.
- [Stripe recurring pricing models](https://docs.stripe.com/products-prices/pricing-models) distinguishes flat-rate, per-seat, tiered, and usage-based subscription structures. It is provider implementation evidence, not a recommendation to use Stripe or its executable agent tooling.
- [U.S. FTC subscription enforcement statement](https://www.ftc.gov/news-events/news/press-releases/2021/10/ftc-ramp-enforcement-against-illegal-dark-patterns-trick-or-trap-consumers-subscriptions) emphasizes prominent material terms, informed consent, and cancellation that is not obstructive.

## Decision Boundaries

- Platform and consumer rules vary by storefront, product type, region, court order, program enrollment, and time. This note captures evidence on the verification date, not a permanent legal conclusion.
- Provider documentation may promote that provider's model or tooling. No Stripe skill, plugin, CLI, package, account, or service was installed or approved while researching this note.
- Conversion alone is not success. Track retained value, complaints, cancellation success, refunds, disputes, involuntary churn, support burden, accessibility, and customer comprehension.
- Usage billing needs a stable meter, deduplication, late-event policy, customer-visible usage, limits or alerts, dispute evidence, and reconciliation. A precise meter can still be an unfair price metric.
- App-store purchase records and provider webhooks are external facts; the product needs an explicit authoritative entitlement model and repair path rather than trusting delivery order.
