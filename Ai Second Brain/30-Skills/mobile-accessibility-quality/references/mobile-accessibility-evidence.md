# Mobile Accessibility Evidence

Verified: 2026-10-21

## Cross-Platform Interpretation

- [W3C WCAG2ICT](https://www.w3.org/TR/wcag2ict/) is an informative W3C Group Note explaining how WCAG 2.0, 2.1, and 2.2 can apply to non-web documents and software, including mobile apps. It is not normative, does not define mobile conformance, and does not replace platform-specific guidance or testing.
- [W3C WCAG2ICT overview](https://www.w3.org/WAI/standards-guidelines/wcag/non-web-ict/) states the scope and limitations, including that non-web software may need accessibility guidance beyond WCAG.

## Apple Platform Evidence

- [Apple: Performing accessibility testing for your app](https://developer.apple.com/documentation/accessibility/performing-accessibility-testing-for-your-app) recommends a task and device matrix, manual testing with accessibility settings, and assistive technologies such as VoiceOver, Voice Control, Switch Control, and Assistive Access.
- [Apple: Performing accessibility audits for your app](https://developer.apple.com/documentation/accessibility/performing-accessibility-audits-for-your-app) documents Accessibility Inspector and automated UI-test audits, and explicitly states that clearing audit findings does not guarantee an accessible app.
- [Apple Human Interface Guidelines: Accessibility](https://developer.apple.com/design/human-interface-guidelines/accessibility) covers perceivable, adaptable, and intuitive interface guidance, including text sizing, contrast, non-color cues, control size, motion, audio alternatives, and familiar interactions.

## Android Platform Evidence

- [Android: Build accessible apps](https://developer.android.com/guide/topics/ui/accessibility/) routes design, development, and testing guidance for Android accessibility.
- [Android: Principles for improving app accessibility](https://developer.android.com/guide/topics/ui/accessibility/principles) covers meaningful labels, accessible actions, built-in framework behavior, and alternatives to color-only communication.
- [Android: Test your app's accessibility](https://developer.android.com/guide/topics/ui/accessibility/testing) recommends combining manual assistive-technology testing, analysis tools, automated checks, and user testing. It covers TalkBack, Switch Access, Voice Access, and test APIs.

## Interpretation Boundaries

- Automated tools find only classes of detectable defects and can produce false positives or miss task-level barriers.
- Platform defaults help only when semantics and behavior are preserved. Custom rendering, gestures, wrappers, and cross-platform bridges require platform-specific verification.
- Accessibility declarations must describe observed support on the released build, device family, language, and journey scope rather than aspirations.
- Legal obligations vary by jurisdiction and product. Obtain qualified review where required.

## Re-Review Triggers

- new UI framework, custom control, device family, OS version, input mode, language, or media type
- accessibility standard, store declaration, procurement, or legal requirement change
- user report, blocked journey, component regression, or automated-audit rule change
