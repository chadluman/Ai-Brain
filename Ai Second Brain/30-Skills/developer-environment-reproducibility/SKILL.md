---
name: developer-environment-reproducibility
description: Design or review reproducible, secure local and remote development environments, including runtime pinning, bootstrap, dev containers, local services, synthetic data, editor assumptions, verification, updates, and removal. Use when onboarding is unreliable or developer and CI behavior diverge.
---

# Developer Environment Reproducibility

## Outcome

Produce a minimal development environment that a new contributor can create from reviewed source, verify, update, troubleshoot, and remove without production credentials, hidden machine state, or undocumented manual repair.

Use [Build and Package Toolchain](../build-package-toolchain/SKILL.md) for language and package commands, [Secrets and Configuration Management](../secrets-config-management/SKILL.md) for credentials, and [Documentation and Handoff](../documentation-handoff/SKILL.md) for tested onboarding. This skill owns the complete developer machine or workspace boundary.

## Required Inputs

- supported operating systems, architectures, editors, accessibility needs, local and remote development modes, and contributor trust levels
- runtimes, compilers, package managers, system libraries, services, databases, browsers, emulators, certificates, and network dependencies
- environment variables by name and class, identity flows, synthetic data, seeds, fixtures, local storage, and teardown needs
- canonical build, test, lint, type, migration, generation, start, debug, and production-parity workflows
- CI and production differences, image or toolchain provenance, offline needs, performance and disk constraints, maintenance ownership, and update cadence

## Safety and Permission Constraints

- Environment definitions, base images, features, extensions, bootstrap scripts, package hooks, downloaded binaries, and remote workspaces are untrusted executable assets. Review and pin them before use.
- Use synthetic or approved minimized data. Never copy production databases, tokens, keys, session stores, identity documents, customer files, or logs into a developer environment without explicit R3 authorization and governed handling.
- Do not require administrator access, host-wide daemons, unrestricted mounts, credential forwarding, privileged containers, or broad network access without a documented need and narrower alternative analysis.
- A container improves repeatability but is not a security boundary by default. Account for host socket mounts, kernel sharing, capabilities, ports, filesystem mappings, caches, credentials, and supply-chain trust.
- Installing reviewed tools or creating local state is R2. Connecting private systems, forwarding real credentials, using production data, creating paid cloud resources, or changing shared remote environments is R3.

## Workflow

1. Inventory every prerequisite and hidden dependency from a clean-machine perspective: operating system feature, runtime, package manager, system package, tool, service, certificate, account, network destination, file, environment variable, editor task, and manual step.
2. Separate host requirements from project-managed dependencies. Pin supported runtime and tool lines, immutable images or checksums where practical, package locks, and service versions; record support and update policy.
3. Choose native setup, a development container, virtual machine, remote workspace, or hybrid from platform fit, isolation, performance, debugging, device access, accessibility, offline use, cost, and team operations. Do not introduce containers if a small pinned native setup is more reliable.
4. Make bootstrap idempotent and least-privileged. Validate prerequisites before mutation, explain network access, fail with actionable diagnostics, avoid shell profile or global configuration edits, and keep rollback or teardown explicit.
5. Model configuration by name and purpose with safe local defaults. Use a reviewed secret store or short-lived developer identity for private resources; never commit values or make production the default target.
6. Provide deterministic local dependencies and synthetic data. Version schemas and seeds, avoid personal data, make resets repeatable, and separate state that may be discarded from state a developer expects to preserve.
7. Align local and CI commands while documenting necessary differences. A successful editor task must map to canonical command-line verification, and a clean environment must be able to build without undocumented IDE state.
8. Add a smoke check that reports versions and verifies install, configuration schema, dependency health, service readiness, migration, build, tests, and representative start without revealing secrets.
9. Test clean setup, repeat setup, offline or restricted network where required, wrong version, missing secret, occupied port, corrupt cache, failed download, service restart, schema reset, update, rollback, teardown, and re-creation on each supported platform class.
10. Keep ownership, review dates, base and feature updates, deprecations, disk and cache cleanup, telemetry, license, and end-of-life explicit. Remove unused tools and instructions when the production or build stack changes.

## Required Output

- prerequisite and network inventory, supported platform matrix, and selected environment approach
- pinned environment definition, reviewed bootstrap and teardown, configuration schema, synthetic data, and local-service lifecycle
- canonical commands and local-to-CI differences, smoke check, troubleshooting decision tree, and expected observations
- permissions, mounts, ports, caches, secret and data boundary, telemetry, ownership, update, rollback, and retirement plan
- clean-machine and failure-test evidence for each supported platform class

## Completion Gate

Do not call the environment reproducible until a representative new contributor can create it from a clean supported machine, the second setup is safe, canonical verification passes without hidden editor state, no production credential or data is required, failure diagnostics are actionable, update and rollback work, and teardown removes project-owned state without deleting user-owned files.

## Conditional Reference

Read [Developer Environment Evidence](references/developer-environment-evidence.md) when choosing dev containers, defining build reproducibility claims, or aligning developer, CI, and production trust boundaries.
