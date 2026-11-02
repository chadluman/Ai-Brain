---
name: browser-extension-development
description: Design and build a browser extension for Chrome, Edge, Firefox, or Safari, covering manifest, permissions, content scripts, background work, storage, and store review. Use when the product itself is a browser extension; do not use for evaluating someone else's extension, which is covered by Developer Extension Evaluation, or for admitting third-party scripts to a website, which is covered by Third-Party Script Governance.
---

# Browser Extension Development

## Outcome

Produce a browser extension that does one job with the smallest permissions that job requires, works across its target browsers without silently breaking on one of them, and can pass store review without a last-minute permission or privacy rewrite.

## Required Inputs

- The extension's single job: what it changes, reads, or adds in the browser, and what it must never do.
- Target browsers and manifest versions: Chrome, Edge, Firefox, Safari, and their manifest v2/v3 differences, where they apply.
- Host permissions and data access: which sites, tabs, cookies, history, or storage the extension actually needs, and why each is required.
- Store and privacy requirements: the store's privacy, permission justification, data-use, and review rules for the exact release.

## Workflow

1. Define the extension's trust boundaries first: the extension core, content scripts, background/service worker, popup and options pages, and any web page or remote service it talks to. Treat web page content as untrusted input to the extension, and extension data as sensitive to web pages.
2. Request the smallest permissions that the job requires, and justify each one in the store listing. Prefer active-tab and optional permissions over broad host access, and request additional permissions only at the moment the user invokes the feature that needs them.
3. Separate content scripts from privileged code. Content scripts run in page context and must not be trusted with credentials, tokens, or privileged APIs. Pass messages through a validated, allow-listed message contract, and validate origin, shape, and authorization for every message.
4. Handle manifest and browser differences explicitly: background service worker versus background page, storage limits, declarative versus dynamic rules, and Safari-specific constraints. Do not assume Chrome behavior is Firefox or Safari behavior, and test each target browser separately.
5. Design storage, sync, and update behavior: what is stored locally versus synced, what is cleared on uninstall or logout, how settings migrate across versions, and how an update cannot silently widen permissions or data access.
6. Test as a store reviewer would: install from a clean profile, exercise every permission, check network destinations, verify that uninstall removes access and local data, and confirm that the extension does not break the host page, leak data to third parties, or inject unwanted content.
7. Prepare store evidence early: privacy policy and data-use declarations, permission justifications, screenshots, and the account and payment rules that apply. A permission added late in development can trigger a new review cycle, so lock the permission set before final testing.

## Safety and Permission Boundaries

- Treat every dependency, build tool, and third-party script in the extension as an executable asset requiring exact-version review. A dependency update is a new version.
- Never collect browsing history, page content, credentials, or personal data beyond the extension's stated job, and never send it to a destination the user has not been told about. Telemetry is data transmission.
- Never store secrets in extension code, settings, or synced storage. Use platform credential storage where the platform provides it, and record secret names and approved locations only.
- Publishing, updating, or changing permissions, data access, or store listings is R3 and requires explicit authorization at that step, with a rollback plan for the previous version.

## Outputs and Evidence

- A permission and data matrix: permission, why it is required, when it is requested, what data it touches, and where that data goes.
- A message contract: allowed messages, validation rules, and authorization checks between content scripts, background work, and any remote service.
- Browser and store evidence: clean-profile install and uninstall tests per target browser, network destination checks, and the completed store privacy and permission checklist.
