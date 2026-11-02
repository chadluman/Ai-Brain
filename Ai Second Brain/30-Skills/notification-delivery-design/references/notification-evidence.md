# Notification Evidence

Verified: 2026-10-21

## Email Standards

- [DMARC, RFC 9989](https://www.rfc-editor.org/rfc/rfc9989.html) is the May 2026 Standards Track replacement for RFC 7489. It defines domain-based authentication, policy, and alignment using SPF and DKIM results. Reporting is separated into companion RFCs 9990 and 9991.
- [DKIM, RFC 6376](https://www.rfc-editor.org/info/rfc6376/) defines domain-key signatures and lists later updates, including cryptographic algorithm guidance. Deployment must account for those updates, not only the base text.
- [SPF, RFC 7208](https://www.rfc-editor.org/rfc/rfc7208.html) defines authorization of sending hosts. SPF alone does not authenticate visible message content or replace DKIM and DMARC alignment.
- [One-Click Unsubscribe, RFC 8058](https://www.rfc-editor.org/rfc/rfc8058.html) defines a DKIM-protected mechanism for one-click list unsubscribe. Legal and provider requirements still need current jurisdiction and provider checks.

## Push Provider Evidence

- [Apple User Notifications](https://developer.apple.com/documentation/usernotifications) states that local and remote delivery is attempted but not guaranteed. The app and server need recovery paths for missed notifications.
- [Firebase message priority](https://firebase.google.com/docs/cloud-messaging/customize-messages/setting-message-priority) distinguishes normal and high priority and warns that high priority is for time-sensitive, user-visible work. Platform rules differ.
- [Firebase message lifespan](https://firebase.google.com/docs/cloud-messaging/customize-messages/setting-message-lifespan) distinguishes backend acceptance from device delivery and documents expiry and offline behavior.
- [Firebase collapsible messages](https://firebase.google.com/docs/cloud-messaging/customize-messages/collapsible-message-types) states that delivery order is not guaranteed and that newer collapsible state may replace older state.

## Decision Boundaries

- Provider documentation establishes channel behavior, not consent, legality, deliverability, or product fitness.
- Opens and clicks can require tracking and can be inaccurate. Collect them only for a defined purpose and with appropriate disclosure and retention.
- Email authentication reduces spoofing and policy ambiguity but does not make content trustworthy or guarantee inbox placement.
- SMS and voice have country, carrier, identity, emergency, and cost rules that require a provider- and region-specific playbook before activation.
