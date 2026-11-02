---
name: mobile-accessibility-quality
description: Plan or review accessibility and interaction quality for native or cross-platform iOS and Android journeys using platform semantics, assistive technologies, adaptive text, input alternatives, automated checks, and user testing. Use before release or when designing mobile screens, components, media, gestures, or navigation.
---

# Mobile Accessibility Quality

## Outcome

Make critical mobile journeys perceivable, operable, understandable, and robust across supported devices, settings, input modes, and assistive technologies, with reproducible evidence rather than tool-only claims.

## Required Inputs

- target platforms, versions, devices, orientations, form factors, languages, and UI framework
- critical journeys, screen inventory, custom controls, gestures, media, time limits, notifications, and error states
- supported accessibility features and any contractual, legal, procurement, or store requirements
- design tokens, component library, automated-test stack, device lab, and access to representative users

## Safety and Permission Constraints

- Do not claim WCAG, platform, legal, or store conformance from an automated scan or a framework default. WCAG2ICT is informative guidance for non-web software, not a mobile conformance standard.
- Preserve native semantic roles, names, values, states, actions, focus order, and announcements. Visual text or a test identifier is not automatically an accessible name.
- Do not make a gesture, color, motion, sound, biometric, or precise timing the only way to understand or complete a critical task.
- Treat disability-related user research and diagnostics as potentially sensitive data. Minimize collection, obtain appropriate consent, and do not record assistive-technology output or personal content by default.
- Accessibility scanners, SDKs, sample apps, and test libraries are executable assets requiring exact-version review before installation or use.

## Workflow

1. Define the critical journey and state matrix: first run, empty, loading, populated, validation error, network error, permission denial, offline, interrupted, success, and recovery.
2. Translate applicable product obligations into testable acceptance criteria. Use current platform guidance and WCAG2ICT as complementary evidence, not interchangeable certification.
3. Prefer native or framework components with correct semantics. For each custom component, specify role, label, value, state, actions, grouping, focus behavior, and input alternatives.
4. Verify content order, focus movement, headings or landmarks where supported, modal containment, announcements, error association, and return focus after navigation or dismissal.
5. Test large text and display scaling, reflow, clipping, contrast, color independence, reduced motion, reduced transparency, captions, transcripts, orientation, keyboard, switch, voice, and screen-reader operation as applicable.
6. Make targets large enough for the platform, provide alternatives to complex gestures, avoid unexpected timeouts, and preserve user settings.
7. Add automated semantic and UI checks for regressions, but keep manual device testing and disability-inclusive user evaluation in the release gate.
8. Exercise every critical task with iOS VoiceOver and relevant Apple settings, and Android TalkBack plus relevant switch, voice, font, display, and interaction settings.
9. Test on representative physical devices and OS versions. Cross-platform abstractions must be checked separately on each platform.
10. Triage defects by blocked task and user impact, attach reproducible evidence without personal data, assign ownership, and prevent recurrence in components and tests.

## Required Output

- requirement and critical-journey accessibility matrix
- component semantics and interaction acceptance criteria
- platform, device, setting, and assistive-technology test matrix
- automated-check scope plus known blind spots
- manual and user-test evidence with blocked-task severity
- remediation ownership, regression tests, and release exceptions
- dated declaration of tested scope and unresolved limitations

## Completion Gate

Do not call a journey accessible because an audit is clean. Completion requires critical tasks to succeed with representative platform assistive technologies and settings, unresolved blockers to be fixed or explicitly accepted by an authorized owner, and evidence to state the exact tested scope.

## Conditional Reference

Read [Mobile Accessibility Evidence](references/mobile-accessibility-evidence.md) before defining acceptance criteria or test coverage. Use [Web Accessibility Review](../web-accessibility-review/SKILL.md) for embedded or companion web content.
