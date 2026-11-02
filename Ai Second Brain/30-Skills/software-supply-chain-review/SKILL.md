---
name: software-supply-chain-review
description: Review software dependencies, build inputs, packages, containers, generators, CI actions, and release provenance before adoption or release. Use for dependency intake, repository qualification, SBOM planning, or supply-chain hardening; do not approve an asset from reputation or an aggregate score alone.
---

# Software Supply Chain Review

## Outcome

Produce a version-specific trust decision and control plan for every external or generated asset that can affect source, builds, releases, runtime behavior, or customer data.

Read [supply-chain evidence](references/supply-chain-evidence.md) before selecting an SBOM, provenance, or repository-scoring standard.

## Inputs

Identify the asset, exact version or digest, source and maintainer, purpose, execution phase, environments, consumers, data and secrets reachable, network and filesystem access, update mechanism, license, transitive dependencies, and replacement path.

## Workflow

1. Inventory source, packages, lockfiles, registries, build tools, compilers, generators, CI actions, container bases, downloaded binaries, scripts, plugins, SDKs, and release artifacts. Include development and test dependencies when they execute.
2. Resolve provenance to an immutable tag, commit, digest, or checksum. Record acquisition date, author or organization, license, security policy, support status, and expected purpose.
3. Inspect the complete package, hidden files, archives, workflows, hooks, native binaries, generated files, dynamic downloads, telemetry, update checks, and credential or broad-permission access.
4. Explain every direct dependency and high-impact transitive dependency. Reject padding, unexplained install scripts, duplicate libraries, abandoned components, and unresolved critical risk.
5. Check current official advisories, release notes, issue history, maintenance and governance evidence, and platform compatibility. Use automated scores only to identify questions for manual review.
6. Define least-privilege build and runtime permissions. Isolate untrusted builds and tests with dummy data, no real credentials, constrained network, and disposable state.
7. Pin and lock approved inputs where supported. Generate and retain an SBOM and provenance at the artifact boundary when they improve traceability, then verify them instead of only producing them.
8. Define upgrade, emergency patch, quarantine, revocation, removal, and rollback procedures. Approval applies only to the reviewed version and configuration.

## Decision

Use the root review outcomes: `approved`, `approved-with-conditions`, `quarantined`, `rejected`, or `retired`. Assign the highest applicable R0-R3 risk. Unknown provenance, opaque binaries, prompt-injection behavior, hidden tracking, credential harvesting, destructive defaults, or unresolved high-impact vulnerabilities fail review.

## Completion

Create the review record with identity and purpose, immutable source, license, risk and permissions, dependencies, network and telemetry, findings and mitigations, advisory evidence, isolated tests, SBOM and provenance status, decision, rollback, and next review trigger. Do not install or execute from a documentation review alone.
