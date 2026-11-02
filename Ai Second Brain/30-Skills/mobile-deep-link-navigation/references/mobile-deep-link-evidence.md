# Mobile Deep Link Evidence

Verified: 2026-10-21

## Verified Web-to-App Links

- [Apple: Allowing apps and websites to link to your content](https://developer.apple.com/documentation/xcode/allowing-apps-and-websites-to-link-to-your-content) documents Universal Links as standard HTTP or HTTPS links backed by a website-to-app association and browser fallback.
- [Apple: Supporting associated domains](https://developer.apple.com/documentation/xcode/supporting-associated-domains) documents the application entitlement and `apple-app-site-association` file, including per-host configuration and HTTPS hosting requirements.
- [Apple: Supporting universal links in your app](https://developer.apple.com/documentation/xcode/supporting-universal-links-in-your-app) warns that link input is an attack vector and directs apps to validate parameters and avoid dangerous direct actions.
- [Apple: Defining a custom URL scheme](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app) explains that another app can register the same private scheme and recommends Universal Links for links uniquely associated with a website.
- [Android: About App Links](https://developer.android.com/training/app-links/about) describes HTTPS App Links and Digital Asset Links domain verification, with browser fallback when the app is absent.
- [Android: Add App Links](https://developer.android.com/training/app-links/add-applinks) documents manifest intent filters and automatic verification.
- [Android: Verify App Links](https://developer.android.com/training/app-links/verify-applinks) documents device verification and testing. A valid-looking manifest alone is not verification evidence.

## Native OAuth Redirects

- [RFC 8252: OAuth 2.0 for Native Apps](https://www.rfc-editor.org/rfc/rfc8252.html) is an IETF Best Current Practice requiring native authorization requests to use an external user-agent and defining redirect choices and PKCE requirements.
- [RFC 9700: OAuth 2.0 Security Best Current Practice](https://www.rfc-editor.org/rfc/rfc9700.html) provides current OAuth security guidance, including redirect URI validation, PKCE, mix-up defenses, token protection, and deprecated patterns.

## Interpretation Boundaries

- Verified app links prove a configured association between an app identity and a domain; they do not authorize the signed-in user or validate the target resource.
- Custom schemes can remain necessary for legacy or protocol cases, but collision and interception risks must be explicit.
- Deferred deep linking and attribution services introduce a separate supplier, privacy, availability, and migration decision.
- Association behavior changes across OS versions and installation state. Test actual supported devices and web fallback rather than relying on configuration inspection alone.

## Re-Review Triggers

- domain, signing identity, application identifier, OAuth profile, or minimum OS change
- route taxonomy migration or addition of consequential link actions
- adoption or removal of a redirect, attribution, or deferred-link provider
- association failures, duplicate navigation, authorization bypass, or sensitive URL leakage
