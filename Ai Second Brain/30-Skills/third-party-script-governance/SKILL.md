---
name: third-party-script-governance
description: Admit, isolate, monitor, change, or remove third-party browser scripts, tags, pixels, widgets, iframes, workers, and SDKs. Use when external code may execute in a web origin or observe browser data; do not treat a tag manager, consent tool, CDN, or trusted vendor as a security boundary.
---

# Third-Party Script Governance

## Outcome

Permit only necessary third-party browser code with explicit ownership, least data and capability access, controlled change, measurable user value, tested failure behavior, and a fast removal path.

Use [Browser Security Policy](../browser-security-policy/SKILL.md) for response policies, [Privacy and Data Governance](../privacy-data-governance/SKILL.md) for lawful data use, [Web Performance Plan](../web-performance-plan/SKILL.md) for budgets, and [Software Supply Chain Review](../software-supply-chain-review/SKILL.md) for package admission. This skill owns browser-side vendor governance.

## Required Inputs

- user journeys, pages, data classes, consent or preference state, authentication and payment surfaces, and supported browsers
- every external script, tag, pixel, iframe, widget, worker, CDN resource, tag-manager container, first-party proxy, and network destination
- business owner, purpose, contract, vendor, exact version or change channel, loader chain, permissions, DOM and storage access, and removal dependency
- performance, accessibility, availability, privacy, security, regional, incident, monitoring, and retention requirements

## Safety and Permission Constraints

- Treat any script executing in the page as privileged application code. A vendor domain, tag manager, consent banner, allowlist, or Subresource Integrity hash does not make its behavior trustworthy.
- Do not expose credentials, payment fields, recovery data, private content, unrestricted DOM state, or unnecessary identifiers to third-party code. Prefer no browser integration, a server-side boundary, or a sandboxed isolated origin when it meets the need.
- Review the complete loader chain, nested tags, dynamic downloads, update mechanism, endpoints, telemetry, cookies, storage, and data recipients. Unknown or mutable code fails admission.
- Adding reviewed code in an isolated environment is R2. Changing a live tag manager, enabling production data collection, transmitting real user data, or changing consent behavior is R3 and requires immediate authorization, verified configuration, monitoring, and rollback.

## Workflow

1. Inventory each executable and embedded third party from source, built output, runtime traffic, tag-manager configuration, consent states, and browser extensions used for testing. Assign a business and technical owner.
2. For each item, document the exact user outcome, alternatives, data read and written, DOM reach, storage and cookie access, network destinations, geographies, subprocessors, permissions, update path, criticality, failure mode, and deletion or exit path.
3. Remove unused, duplicate, opaque, abandoned, overly broad, or unjustified code. Prefer static content, native platform behavior, first-party code, server-to-server exchange, or isolated frames with narrow messaging.
4. Review the exact asset and loader as an imported executable. Pin immutable versions where practical, verify provenance and license, inspect install or runtime downloads, scan advisories, and define re-review triggers.
5. Constrain execution and communication with route-specific CSP, integrity metadata where the resource is immutable and supported, correct `crossorigin` and referrer behavior, sandboxed frames, Permissions Policy, narrow `postMessage` origins and schemas, and destination allowlists.
6. Define consent and preference behavior before loading or transmitting. Verify that rejection, withdrawal, account change, logout, and deletion stop collection and clear or age out applicable state without breaking essential journeys.
7. Budget main-thread work, network, layout shift, memory, accessibility impact, and provider latency. Make nonessential integrations asynchronous, failure-isolated, and unable to block authentication, checkout, content, or recovery.
8. Establish controlled promotion, peer review, two-person approval for sensitive containers, audit history, environment separation, emergency disablement, vendor compromise response, and contract or provider exit.
9. Test allowed and denied consent, provider timeout and corruption, blocked domains, content blockers, slow devices, keyboard and assistive technology, script mutation, CSP violations, data leakage, account switching, logout, kill switch, and rollback.

## Required Output

- complete script, tag, embed, loader, destination, owner, purpose, permission, data, and lifecycle inventory
- per-integration keep, isolate, replace, quarantine, or remove decision with evidence and risk level
- exact browser-policy, consent, data-minimization, performance, accessibility, monitoring, and failure controls
- controlled-change, incident, kill-switch, removal, contract-exit, verification, and re-review plan

## Completion Gate

Do not approve an integration until every executable path and destination is known, its value exceeds its security, privacy, performance, accessibility, availability, and lock-in costs, sensitive journeys remain safe when it fails or is blocked, consent and deletion behavior are proven, and an owner can disable and remove it without losing authoritative data.

## Conditional Reference

Read [Third-Party Script Evidence](references/third-party-script-evidence.md) before admitting a browser vendor, selecting isolation controls, or relying on integrity metadata.
