# Flag and Rollout Evidence

Verified: 2026-10-21

## Primary and Industry Sources

- [OpenFeature](https://openfeature.dev/) is a CNCF incubating, Apache-2.0, vendor-neutral feature-flag API specification. It supports portability at the application interface; a provider implementation, telemetry, control plane, and operational behavior still require review.
- [Google SRE: Canarying Releases](https://sre.google/workbook/canarying-releases/) defines canarying as partial, time-limited exposure evaluated against a control before rollout. It describes separating feature launch from binary release and stresses reliable decision signals.
- [Google SRE: On-Call](https://sre.google/workbook/on-call/) notes that independent feature disablement can reduce failure impact. Emergency controls still require access, audit, testing, and dependency-failure design.

## Decision Boundaries

- A standard client API reduces application coupling but does not make a flag provider safe, available, private, or inexpensive.
- A canary protects only the measured population and signals. Rare, delayed, accessibility, regional, data-integrity, and authorization failures may require specific cohorts and tests.
- Experiments require the separate analytics and experimentation controls; operational flags should not silently become research on users.
- Permanent configuration, permission, and entitlement rules should have explicit governance rather than remaining unowned temporary flags.
