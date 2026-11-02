---
name: mobile-web-experience-design
description: Design web experiences specifically for iOS Safari, Android Chrome, and in-app browsers, covering viewport, touch, safe areas, install, push, storage, and platform quirks. Use when a web product must work well on phones, not just shrink a desktop layout; do not use for support policy alone, which is covered by Web Platform Compatibility, or for native apps, which are covered by Mobile Stack Selection.
---

# Mobile Web Experience Design

## Outcome

Produce a mobile web experience that feels native where it matters and degrades gracefully where the platform does not support a feature: correct viewport and safe-area layout, reliable touch interaction, install and push behavior that matches what each platform actually allows, and no dependence on a desktop assumption.

Use [Web Platform Compatibility](../web-platform-compatibility/SKILL.md) to set the support policy. Use this skill for the mobile-specific design and verification inside that policy.

## Required Inputs

- Target devices and browsers: iOS versions and Safari, Android versions and Chrome, and any in-app browsers that matter (social, messaging, or embedded WebViews).
- Critical mobile journeys: what users actually do on a phone, in what context, and what must work with one hand, on a slow network, or offline.
- Platform-sensitive features: install, push notifications, background work, storage, camera, files, payments, and deep links, and which of them are required versus nice to have.
- Real-device evidence: which devices and OS versions will be tested, and how in-app browser behavior will be verified.

## Workflow

1. Design for the phone first for mobile-critical journeys: thumb reach, touch target size, readable text without zooming, and a layout that survives the dynamic viewport, safe areas, notches, and on-screen keyboards. Test with the keyboard open, not only with it closed.
2. Inventory iOS Safari, Android Chrome, and in-app browser differences before relying on a feature: service worker and push support, storage quotas and eviction, fullscreen and install prompts, viewport units, input and focus behavior, media autoplay, and background limits. Record each difference as a supported, degraded, or unsupported behavior, with the user-visible fallback.
3. Do not assume a PWA install, push subscription, or background sync will be available on iOS just because it works on Android, or in an in-app browser just because it works in Safari or Chrome. Design the journey to work without install and without push, and treat install and push as enhancements.
4. Handle storage as a limited, evictable resource on mobile: define what is cached, what is persisted, what is lost on eviction or logout, and how the user recovers. Use [Browser Storage Data Safety](../browser-storage-data-safety/SKILL.md) and [PWA and Offline Design](../pwa-offline-design/SKILL.md) for the storage and offline model.
5. Design touch and input explicitly: touch targets, gestures versus buttons, long-press and swipe conflicts, haptic and scroll behavior, and accessible alternatives for every gesture. Do not rely on hover, right-click, or precise mouse behavior on a phone.
6. Optimize for mobile networks and devices: bundle size, image and media sizes, font loading, and startup time, measured on a real mid-range device on a slow network, not only on a desktop with throttling. Use [Web Performance Plan](../web-performance-plan/SKILL.md) for budgets.
7. Verify on real devices: iOS Safari, Android Chrome, and at least one major in-app browser, across the supported OS versions, for every critical journey, including install, push, offline, deep link, and payment flows where they apply.

## Safety and Permission Boundaries

- Do not request device permissions, push permission, or install prompts before the user understands the value. Explain each request in context and handle denial gracefully.
- Do not store sensitive data in mobile browser storage by default, and clear it on logout, account switch, and shared-device use.
- In-app browsers may share cookies, state, or network behavior with their host app. Do not assume an in-app browser is a private, isolated browser, and do not pass credentials through deep links or URLs.
- Store submission, push credentials, and production configuration are R3 where they apply and require immediate authorization.

## Outputs and Evidence

- A mobile platform matrix: feature, iOS Safari behavior, Android Chrome behavior, in-app browser behavior, and the fallback for each.
- A mobile journey checklist: viewport, safe area, keyboard, touch, install, push, offline, and deep-link behavior for each critical journey.
- Real-device test evidence for the supported devices and OS versions, with any platform-specific defects and their fallbacks recorded.
