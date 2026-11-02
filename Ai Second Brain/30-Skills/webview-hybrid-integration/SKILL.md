---
name: webview-hybrid-integration
description: Wrap a web application as an iOS or Android app using a WebView or hybrid framework, with a safe native bridge, plugins, and store-ready lifecycle. Use when an existing web app must ship in app stores without a full native rewrite; do not use to choose native versus cross-platform versus web, which is covered by Mobile Stack Selection.
---

# WebView Hybrid Integration

## Outcome

Produce a hybrid app where the web app runs inside a controlled WebView, native capabilities are exposed through a narrow, authorized bridge, and the app behaves correctly through install, update, offline, background, and store review — without giving web content blanket native access.

Use [Mobile Stack Selection](../mobile-stack-selection/SKILL.md) to decide that a hybrid approach fits at all. Use this skill for the integration once that decision is made. Use [PWA and Offline Design](../pwa-offline-design/SKILL.md) when an installable web app, rather than a store app, would serve the need.

## Required Inputs

- The web app's critical journeys, and which of them need native capabilities: camera, files, notifications, biometrics, location, payments, background work, or deep links.
- The hybrid tooling choice: Capacitor, Cordova, or a platform WebView, with its plugin model and update mechanism.
- Platform constraints: minimum iOS and Android versions, store policies, signing, and the review evidence each store requires.
- Update and offline needs: how web content updates, how native code updates, and what happens when the two versions diverge.

## Workflow

1. Keep the bridge narrow and explicit. Expose only named, versioned bridge methods, each with its own authorization check, input validation, and error contract. Do not expose a generic "run native code" or "read any file" method to web content.
2. Treat web content as untrusted by the native layer, and native data as sensitive by the web layer. Validate bridge arguments on the native side, validate bridge results on the web side, and never pass credentials, tokens, or other users' data through the bridge unless that specific method requires it and is authorized.
3. Define the version contract: native app version, web content version, bridge version, and plugin versions, and what happens on mismatch. Prefer a web-content update that cannot break an old native shell, and a native update path that does not strand users on stale web content.
4. Handle lifecycle explicitly: app backgrounding and suspension, WebView reload and eviction, offline and poor-network behavior, deep links, and push notification handling. Use [Mobile Deep Link Navigation](../mobile-deep-link-navigation/SKILL.md) for link routing and [Mobile Offline Sync](../mobile-offline-sync/SKILL.md) for queued work.
5. Secure storage and sessions for the hybrid context: do not store long-lived credentials in WebView local storage by default, clear session data on logout and account switch, and use platform secure storage for tokens where the platform provides it. Use [Mobile Security and Privacy](../mobile-security-privacy/SKILL.md) for the threat model.
6. Test on real devices and real OS versions, not only in a browser or emulator: WebView versions differ from the system browser, and iOS and Android WebViews differ from each other. Use [Mobile Device Lab Selection](../mobile-device-lab-selection/SKILL.md) for device evidence, and test install, update, offline, background, and store-review journeys.
7. Prepare store evidence early: privacy labels, data-use declarations, permission justifications, screenshots, and the account and payment rules that apply to the release. Use [App Store Policy Readiness](../app-store-policy-readiness/SKILL.md) and [Mobile Release Operations](../mobile-release-operations/SKILL.md) for the release path.

## Safety and Permission Boundaries

- Treat every plugin, native module, and build tool as an executable asset requiring exact-version review. A plugin update is a new version, not a routine patch.
- Minimize device permissions, explain each request in context, and handle denial or revocation gracefully. Do not request a permission the current journey does not need.
- Signing, store accounts, certificates, production push credentials, and store submission are R3 and require immediate authorization.
- Never load remote web content into a privileged WebView without a defined origin allow-list, and never enable debugging or remote inspection in a release build.

## Outputs and Evidence

- A bridge contract: methods, arguments, authorization checks, version, and error behavior for each native capability.
- A version and update matrix: native, web, bridge, and plugin versions, and the behavior on mismatch.
- Device and store evidence: real-device test results for install, update, offline, background, and deep-link journeys, and the store policy checklist for the release.
