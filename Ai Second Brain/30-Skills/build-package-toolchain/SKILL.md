---
name: build-package-toolchain
description: Select or review a project's language runtime, package manager, lockfile policy, build tooling, lifecycle scripts, caches, update process, and reproducible CI commands. Use when bootstrapping or changing a JavaScript or comparable web toolchain; do not use as a general framework-selection or dependency-approval shortcut.
---

# Build and Package Toolchain

## Outcome

Produce a minimal, pinned, reproducible toolchain whose dependency resolution, executable hooks, build outputs, caches, upgrades, and rollback are explicit and reviewable.

## Required Inputs

- languages and runtime targets, supported developer platforms, and deployment runtime
- repository shape, workspace or monorepo needs, existing manifests and lockfiles
- framework-required build behavior, browser targets, server output, and asset needs
- CI environment, cache constraints, network policy, release cadence, and maintenance capacity
- current package-manager and build-tool versions, migration reason, and rollback point

Preserve an established working toolchain unless measured constraints justify migration.

## Safety and Permission Constraints

- A manifest, lockfile, lifecycle hook, compiler plugin, bundler plugin, binary package, and downloaded cache are untrusted executable inputs.
- Do not install packages or run project scripts until the exact dependency graph and executable hooks have passed the repository safety gate.
- Never bypass integrity verification, TLS, lockfile consistency, or registry policy merely to make an install pass.
- Use a clean disposable environment without real credentials for first install and build validation.
- Pin the runtime and package-manager line used by development and CI. Commit the authoritative lockfile and reject unexplained resolution changes.
- Publishing packages, changing a shared registry, or modifying production build credentials is R3 and requires immediate authorization and rollback.

## Workflow

1. Inventory the existing runtime, manager, manifests, lockfiles, configuration, plugins, lifecycle scripts, registries, and CI commands before proposing changes.
2. Define decision criteria: ecosystem compatibility, deterministic installs, workspace support, security controls, platform support, performance, maintenance, and exit path.
3. Choose one package manager per dependency graph unless interoperability is a demonstrated requirement. Pin its supported version and document how it is obtained.
4. Review direct and transitive dependencies, licenses, maintainers, advisories, install scripts, native binaries, remote downloads, telemetry, and permissions. Minimize the graph before optimizing it.
5. Require frozen or immutable lockfile installation in CI. Treat manifest-lock disagreement as failure and review every lockfile delta as code.
6. Select the smallest build stack that produces the required browser, server, library, or worker artifacts. Prefer standards and framework-supported defaults over layers of plugins.
7. Separate development conveniences from production output. Document environment-variable exposure, source-map policy, code generation, asset hashing, and build-time network access.
8. Scope caches by runtime, manager, platform, and lockfile digest. Verify restored content and allow a clean no-cache rebuild.
9. Test a clean checkout through install, type or static checks, tests, production build, artifact inspection, and a representative start. Compare outputs or attestations where reproducibility matters.
10. Define controlled upgrades, advisory response, compatibility checks, canary use, rollback, and removal of obsolete tools.

## Required Output

- toolchain decision and rejected alternatives
- pinned runtime, manager, build tools, and support policy
- dependency and lifecycle-script review record
- authoritative lockfile and immutable CI install policy
- canonical development, verification, and production-build commands
- artifact, cache, environment, and network boundaries
- update, migration, rollback, and re-review triggers

## Completion Gate

Do not call the toolchain ready until a reviewed clean install and production build succeed in isolation, the lockfile is unchanged by the frozen install, the output contains no secrets, and the same commands work in CI. Approval applies only to the reviewed versions.

## Conditional Reference

Read [Build Toolchain Evidence](references/build-toolchain-evidence.md) when defining lockfile, lifecycle-script, provenance, or reproducibility controls.
