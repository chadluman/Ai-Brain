---
name: dependency-upgrade-operations
description: Operate routine, major, security, deprecation, runtime, container-base, CI-action, and transitive dependency upgrades after initial asset approval. Use when designing update cadence, automation, compatibility evidence, rollout, rollback, or removal without allowing update bots to merge on trust alone.
---

# Dependency Upgrade Operations

## Outcome

Produce a sustainable update system that keeps approved dependencies supported and secure, qualifies every resolved graph change, limits simultaneous risk, verifies behavior and artifacts, deploys safely, and removes obsolete or abandoned components.

Use [Software Supply Chain Review](../software-supply-chain-review/SKILL.md) for initial or materially changed asset trust, [Build and Package Toolchain](../build-package-toolchain/SKILL.md) for resolution and lockfiles, [Vulnerability Management Operations](../vulnerability-management-operations/SKILL.md) for exposure response, and [Release Quality Evaluation](../release-quality-evaluation/SKILL.md) for candidate disposition. This skill owns the update flow.

## Required Inputs

- direct and transitive dependencies, runtimes, container bases, operating packages, CI actions, build plugins, generated clients, schemas, SDKs, and external API versions
- current resolved versions, immutable sources, lockfiles, manifests, owners, support and deprecation status, advisories, licenses, permissions, telemetry, and data access
- compatibility contracts, supported clients and platforms, test coverage, artifact baselines, release cadence, maintenance capacity, and rollback behavior
- automation provider, registry and private dependency access, update grouping, cooldown, rate, credentials, network, review, merge, and bypass policy
- production exposure, exploitability, migration urgency, end-of-life dates, change freezes, and user-impact constraints

## Safety and Permission Constraints

- Treat every version, digest, lockfile, generated file, install hook, binary, release note, migration, and update pull request as untrusted input. Prior approval does not transfer to materially changed contents or permissions.
- Version numbers communicate maintainer intent only when the project follows the declared scheme. A patch can break behavior or be malicious; a major update can be low-risk after proper migration.
- Do not auto-merge solely because checks pass, a bot opened the change, a release is signed, or a vulnerability score is high. Review provenance, graph, scripts, advisories, license, compatibility, and test relevance.
- Update automation needs least-privilege read access to manifests and registries and narrowly scoped pull-request rights. Never expose broad repository, release, or production credentials to update jobs.
- Installing or executing an updated graph is R2 after review. Publishing, production deployment, credential or data migration, destructive cleanup, and emergency changes with material user risk are R3.

## Workflow

1. Maintain an owned inventory with exact resolved version or digest, purpose, dependency path, environment, permissions, data and secret reach, public or internal API used, support window, next review, and replacement route.
2. Classify updates as routine compatible, major or breaking, urgent security, runtime or platform, container base, build or CI, protocol or schema, abandoned replacement, or removal. Give each class a cadence, evidence requirement, and escalation owner.
3. Inspect release notes, changelog, migration and deprecation guides, immutable source and signatures or provenance where available, advisory status, maintainer and ownership changes, license, new dependencies, scripts, binaries, downloads, telemetry, permissions, and platform support.
4. Resolve in a clean disposable environment with frozen policy. Review manifest and entire lockfile or digest delta, unexpected transitive changes, package-source changes, duplicate versions, build output, and network activity.
5. Scope compatibility from the actual API and behavior used. Add contract, type, unit, integration, end-to-end, migration, accessibility, performance, security, and rollback tests proportional to the changed surface and consequence.
6. Keep changes reviewable. Separate unrelated major migrations; group low-risk related packages only when ownership and rollback align; update runtime, framework, plugins, and generated output together only when their compatibility matrix requires it.
7. Validate artifact and deployment behavior: clean build, SBOM and provenance change, size and license delta, configuration and environment changes, data or cache compatibility, observability, canary, rollback, and mixed-version operation.
8. For urgent vulnerabilities, combine affected-version and reachability evidence with exposure, exploitation, business harm, fix quality, compensating controls, and deployment coverage. Record why the chosen response and timing reduce total risk.
9. Roll out through the established release path with owners, health and security signals, stop conditions, and a proven rollback or forward-fix. Confirm every deployed artifact actually contains the intended fixed graph.
10. Remove obsolete packages, flags, adapters, credentials, registry access, generated outputs, compatibility code, and documentation. Track recurring blocks and replace dependencies whose support, governance, security, or upgrade cost no longer fits.

## Required Output

- dependency and support inventory with ownership, classification, cadence, and re-review triggers
- automation permission, grouping, cooldown, review, merge, and failure policy
- per-update provenance, release, advisory, license, graph, script, permission, and compatibility review
- test and artifact evidence, migration, rollout, monitoring, rollback, deployment confirmation, and residual risk
- deprecation, blocked-update, abandonment, replacement, removal, and retrospective record

## Completion Gate

Do not call an update complete until the exact resolved graph and artifact are known, unexpected changes are explained, relevant compatibility and negative tests pass, licenses and permissions remain acceptable, the deployed version is observable, rollback or recovery is proven, obsolete access and code are removed, and the inventory records the new approved version and next trigger.

## Conditional Reference

Read [Dependency Upgrade Evidence](references/dependency-upgrade-evidence.md) when interpreting version signals, selecting automation, using cooldowns and grouping, or distinguishing update, vulnerability, and supply-chain evidence.
