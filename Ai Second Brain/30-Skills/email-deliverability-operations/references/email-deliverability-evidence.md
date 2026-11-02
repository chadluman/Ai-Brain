# Email Deliverability Evidence

Verified: 2026-10-22

## Standards and Receiver Requirements

- [DMARC, RFC 9989](https://www.rfc-editor.org/info/rfc9989/) is the May 2026 Standards Track replacement for RFCs 7489 and 9091. It defines policy and alignment using SPF and DKIM results; reporting is separated into RFCs 9990 and 9991.
- [DMARC aggregate reporting, RFC 9990](https://www.rfc-editor.org/info/rfc9990/) defines aggregate XML feedback about authentication and sending sources. Report ingestion still needs authenticity, completeness, privacy, retention, and parser hardening.
- [DMARC failure reporting, RFC 9991](https://www.rfc-editor.org/info/rfc9991/) warns that individual failure reports can contain headers or entire message content with personally identifiable information. Request and retain them only when necessary and protected.
- [SPF, RFC 7208](https://www.rfc-editor.org/info/rfc7208/) authorizes sending hosts for a domain. It does not authenticate visible message content or replace aligned DKIM and DMARC.
- [DKIM, RFC 6376](https://www.rfc-editor.org/info/rfc6376/) defines domain signatures; review its listed updates, including current cryptographic algorithm and key guidance, before implementation.
- [One-click unsubscribe, RFC 8058](https://www.rfc-editor.org/info/rfc8058/) defines a DKIM-protected HTTPS POST flow and says it must not depend on cookies or HTTP authorization. The endpoint needs an opaque, hard-to-forge recipient and list binding.
- [Gmail email sender guidelines](https://support.google.com/mail/answer/81126?hl=en) document authentication, DNS, TLS, formatting, spam-rate, alignment, and one-click-unsubscribe expectations for mail to personal Gmail accounts. Thresholds and enforcement are receiver policy and can change.
- [Yahoo sender best practices](https://senders.yahooinc.com/best-practices/) document authentication, DNS, complaint-rate, alignment, unsubscribe, and RFC expectations for Yahoo recipients. Yahoo explicitly marks requirements as subject to change.

## Decision Implications

- Authentication protects domain use and informs receiver policy; it does not prove message truth, safety, permission, or inbox placement.
- DMARC enforcement should follow a complete sender inventory and observed aligned traffic. Moving directly to rejection can block legitimate systems, while remaining indefinitely at observation leaves spoofing risk unresolved.
- Aggregate and failure reports are untrusted external input and can expose addresses, domains, IPs, headers, or content. Parse defensively and apply access, purpose, and retention controls.
- Receiver thresholds are operational signals, not universal product targets. Define stricter internal guardrails where user trust or critical delivery requires them.
- Forwarding, mailing lists, security gateways, shared IPs, DNS errors, and key rotation create legitimate failure modes. Test the actual routing topology rather than assuming a single direct path.
