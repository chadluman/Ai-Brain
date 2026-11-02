# Browser Security Policy Evidence

Verified: 2026-10-21

## Standards and Security Guidance

- [Content Security Policy Level 3](https://www.w3.org/TR/CSP/) is a W3C Working Draft that defines resource and execution controls, framing, sandboxing, reporting, and policy delivery. It states that CSP is defense in depth rather than a first-line injection defense.
- [OWASP Content Security Policy Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html) provides deployment patterns and warns that granular allow-list policies can remain bypassable when they are too permissive.
- [HTTP Strict Transport Security, RFC 6797](https://www.rfc-editor.org/rfc/rfc6797.html) defines browser enforcement of HTTPS for known HSTS hosts. Subdomain and preload scope require separate operational care.
- [Referrer Policy](https://www.w3.org/TR/referrer-policy/) defines how browsers control referrer information for subresources and navigation. It cannot stop every URL leak.
- [Permissions Policy](https://www.w3.org/TR/permissions-policy-1/) is a W3C Working Draft defining response and iframe controls for browser features. Syntax and interoperability can change.
- [Fetch Metadata Request Headers](https://www.w3.org/TR/fetch-metadata/) is a W3C Working Draft defining request-context signals such as site, mode, destination, and user activation.
- [OWASP CSRF Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html) describes Fetch Metadata policy with mandatory fallback behavior and places it alongside token and origin defenses.
- [Subresource Integrity](https://www.w3.org/TR/SRI/) is a W3C Working Draft defining browser verification of fetched resource integrity. Exact algorithm and browser support must be checked.
- [OWASP HTTP Headers Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html) summarizes security-relevant response headers and their common boundaries. It is practical guidance rather than a copy-ready universal configuration.

## Interpretation Boundaries

- CSP source lists are not a trust inventory unless every allowed origin and script path is controlled. A compromised allowed host can undermine the policy.
- Nonces must be unpredictable and unique per response, applied only to intended elements, and not exposed to unsafe templating. Hashes bind exact content and add deployment coordination.
- `frame-src` controls frames the page loads; `frame-ancestors` controls who may embed the page. They are not interchangeable.
- HSTS is learned over HTTPS and can affect subdomains for its lifetime. Preload has an external submission and removal lifecycle.
- Fetch Metadata is request context, not identity or authorization. Some clients and webviews may omit it.
- Permissions Policy reduces available features but does not replace user permission prompts or safe capability use.
- SRI helps with unexpected resource changes but not a malicious resource approved with a matching new hash, dynamic APIs, or unsupported fetch paths.

## Verification Prompts

- Are headers present on HTML, errors, redirects, authenticated pages, static responses, and edge-generated responses where intended?
- Does the CSP block untrusted inline script, dynamic evaluation, unexpected frames, form targets, workers, and connections?
- Can required third-party resources be removed, self-hosted, sandboxed, or isolated instead of allowed broadly?
- Are report endpoints authenticated where possible, rate-limited, size-limited, sampled, redacted, and retained briefly?
- Do older browsers and embedded webviews receive safe fallback behavior rather than silent authorization assumptions?

## Re-Review Triggers

- new origin, route, renderer, tag, CDN, frame, worker, browser capability, or webview
- CSP, Permissions Policy, Fetch Metadata, SRI, browser, or framework behavior change
- policy violation spike, bypass report, data leak, mixed content, certificate failure, or third-party compromise
- HSTS scope or preload change, domain migration, or certificate-automation change
