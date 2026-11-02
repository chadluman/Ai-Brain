---
name: browser-security-policy
description: Design, deploy, or review browser-enforced response policies and related server checks, including Content Security Policy, framing controls, HSTS, Referrer Policy, Permissions Policy, Fetch Metadata, MIME controls, and subresource integrity. Use when hardening a web application or changing origins, third-party resources, embeds, or browser capabilities.
---

# Browser Security Policy

## Outcome

Build a tested, least-privilege browser policy set that reduces injection, embedding, transport, capability, and cross-site request risk without silently breaking critical journeys or collecting unsafe reports.

## Required Inputs

- application origins, routes, rendering modes, browser and webview support policy, and deployment topology
- script, style, image, font, media, worker, frame, form, connection, navigation, and manifest sources
- inline code, dynamic code, nonces or hashes, service workers, third-party tags, CDN use, and build pipeline
- embedding and embedded-content needs, browser capabilities, cross-origin isolation, referrer requirements, and external links
- session and CSRF model, API endpoints, upload and download behavior, report collection, privacy, and incident response

## Safety and Permission Constraints

- Treat browser policies as defense in depth. They do not replace contextual output encoding, safe DOM APIs, input validation, CSRF defenses, authorization, or dependency review.
- Do not weaken a policy globally to fix one asset. Identify the exact route, directive, source, and business owner, and prefer removing unsafe behavior.
- Avoid broad wildcards, `unsafe-inline`, `unsafe-eval`, unrestricted framing, and unnecessary browser capabilities. Any exception needs a documented threat and retirement plan.
- Policy reports and referrers can contain full URLs, identifiers, or user data. Minimize, sample, redact, restrict access, set retention, and prevent attacker-driven report floods.
- HSTS, subdomain inclusion, preload, and cross-origin isolation can cause long-lived or ecosystem-wide outages. Verify every affected host and rollback constraint before enabling them.
- Changes to production edge, CDN, DNS, TLS, headers, public report collectors, or preload submissions are R3 and require immediate authorization, staged rollout, and rollback evidence.

## Workflow

1. Inventory every browser origin, resource type, third-party source, frame relationship, form target, connection target, worker, capability, and route-specific exception from observed builds and traffic.
2. Remove unnecessary inline code, dynamic evaluation, third-party tags, mixed content, insecure schemes, broad CORS, and unused capabilities before writing policy exceptions.
3. Design route-aware CSP beginning with a restrictive fallback. Define script trust with nonces or hashes where appropriate, constrain objects, bases, frames, ancestors, forms, workers, connections, upgrades, and reporting.
4. Stage CSP in report-only mode with synthetic and representative journeys. Filter noise, protect report ingestion, then enforce incrementally without treating report silence as proof.
5. Define framing with CSP `frame-ancestors` and any required compatibility fallback. Separately define which frames the application may load.
6. Define HSTS only after all scoped hosts work on HTTPS. Decide max age, subdomain scope, and preload separately with certificate and domain-recovery plans.
7. Choose Referrer Policy from the minimum cross-origin information genuinely required. Keep secrets and capability tokens out of URLs regardless of policy.
8. Disable unnecessary browser features with Permissions Policy and explicit iframe delegation. Verify exact supported syntax and browser behavior.
9. Add server-side Fetch Metadata policy for applicable cross-site request filtering with Origin or Referer and token fallbacks for supported legacy clients. Never use it as the only CSRF defense.
10. Apply `X-Content-Type-Options: nosniff`, correct media types, safe download disposition, and subresource integrity where externally hosted immutable resources and browser support make it effective.
11. Test critical routes, authentication, payments, editors, uploads, downloads, workers, offline behavior, embeds, extensions, and third-party failure across supported browsers and webviews.
12. Record every directive, owner, exception, compatibility fallback, report destination, data handling rule, staged deployment, rollback, and re-review trigger.

## Required Output

- origin, resource, embed, capability, and third-party inventory
- route-specific policy matrix and exact response-header plan
- CSP trust model, report-only evidence, enforcement rollout, and exception register
- HSTS, framing, referrer, permissions, Fetch Metadata, MIME, and integrity decisions
- supported-browser and webview verification evidence
- reporting privacy, abuse protection, monitoring, rollback, and recovery plan

## Completion Gate

Do not call the policy complete until enforced headers are verified on every relevant response path, critical journeys pass in supported browsers and webviews, negative tests demonstrate intended blocking, reports are privacy-controlled, and every exception has an owner and re-evaluation trigger.

## Conditional Reference

Read [Browser Security Policy Evidence](references/browser-security-policy-evidence.md) before selecting directives or copying a header set. Use [Web Application Security Review](../web-app-security-review/SKILL.md) for the wider application and [Session and Cookie Security](../session-cookie-security/SKILL.md) for sessions and CSRF.
