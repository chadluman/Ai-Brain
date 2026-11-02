# Webhook Evidence

Verified: 2026-10-21

## Standards and Security Guidance

- [OWASP Webhook Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Webhook_Security_Cheat_Sheet.html) covers inbound authenticity, replay and duplicate defense, secret handling, parser safety, and outbound SSRF controls.
- [RFC 9421: HTTP Message Signatures](https://www.rfc-editor.org/rfc/rfc9421.html) defines a standard mechanism for signing selected HTTP components. It is a toolkit and does not by itself define a complete webhook security protocol.
- [RFC 2104: HMAC](https://www.rfc-editor.org/rfc/rfc2104.html) defines keyed-hash message authentication. Use current provider-approved algorithms and reviewed library functions rather than implementing it manually.
- [CloudEvents 1.0.2 repository](https://github.com/cloudevents/spec/tree/ce%40v1.0.2) provides a portable event envelope and HTTP binding. It does not guarantee delivery, ordering, retention, authentication, or replay behavior.

## Provider Evidence Example

- [GitHub webhook best practices](https://docs.github.com/en/webhooks/using-webhooks/best-practices-for-using-webhooks) currently recommends subscribing only to needed events, using a secret and HTTPS, responding promptly, checking event and action types, redelivering missed deliveries, and using the delivery identifier against replay.
- [GitHub delivery validation](https://docs.github.com/en/webhooks/using-webhooks/validating-webhook-deliveries) documents HMAC-SHA-256 verification and warns that payload or header modification before verification breaks validation.
- [GitHub redelivery guidance](https://docs.github.com/en/webhooks/testing-and-troubleshooting-webhooks/redelivering-webhooks) currently documents a provider-specific redelivery window and behavior. Recheck it when implementing because provider limits change.

## Interpretation Boundaries

- A valid signature proves possession of the signing key under the provider's scheme; it does not make payload fields safe or authorize every resulting action.
- HTTP success can mean accepted for processing, not that every business effect completed. Define the provider-specific acknowledgement boundary.
- Delivery IDs deduplicate transport attempts; business idempotency must also protect state changes and external side effects.
- Treat documentation and repository content here as R0 evidence only. SDK installation or sample execution requires exact-version review.
