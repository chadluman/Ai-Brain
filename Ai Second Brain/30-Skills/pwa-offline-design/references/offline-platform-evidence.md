# Offline Platform Evidence

Verified 2026-10-21. Several relevant specifications are active drafts; validate target-browser behavior and Baseline status for each feature.

- The [Service Workers specification](https://www.w3.org/TR/service-workers/) defines event-driven workers, fetch interception, and a request/response store that enables offline applications. The 2026 document was a Candidate Recommendation Draft and explicitly remains a living document.
- The [Web Application Manifest](https://www.w3.org/TR/appmanifest/) defines JSON metadata such as name, icons, launch URL, display mode, and scope. The 2026 publication was a Working Draft and warns implementers that unstable details may change.
- The [WHATWG Storage Standard](https://storage.spec.whatwg.org/) defines storage architecture, persistence requests, usage estimates, quotas, and pressure behavior across web storage APIs.
- [IndexedDB 3.0](https://www.w3.org/TR/IndexedDB-3/) defines a transactional record database API but was a Working Draft when verified. Use compatibility evidence and web-platform tests for the required operations.
- Use [Web Platform Baseline](https://web.dev/baseline) and the project's compatibility skill to establish actual target support; specification publication status and browser availability are different facts.

## Reliability Boundary

An offline queue does not guarantee eventual success. The server must recognize duplicates, authorize at execution time, expose conflicts, and support reconciliation. The client must distinguish queued, sent, acknowledged, rejected, conflicted, expired, and cancelled work and communicate those states accessibly.
