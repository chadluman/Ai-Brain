---
name: repository-topology-selection
description: Select or review monorepo, polyrepo, workspace, package, and source-control topology for applications and shared components. Use when deciding what belongs in one repository, splitting or combining repositories, or designing ownership, CI scope, release, access, and large-repository behavior.
---

# Repository Topology Selection

## Outcome

Produce a repository structure whose collaboration and atomic-change benefits fit ownership, access, build, release, compliance, scale, and lifecycle needs, with explicit package contracts and a reversible migration path.

Use [Build and Package Toolchain](../build-package-toolchain/SKILL.md) for workspace tooling, [CI/CD and Release Design](../ci-cd-release-design/SKILL.md) for pipelines, and [Software Supply Chain Review](../software-supply-chain-review/SKILL.md) for repository and build trust. This skill decides source grouping rather than selecting a monorepo tool. Use [Version Control Workflow Design](../version-control-workflow-design/SKILL.md) for branching models; this skill decides how source is grouped, and that skill decides how branches flow through it.

## Required Inputs

- products, deployables, libraries, schemas, infrastructure, documentation, generated artifacts, ownership, contributors, and external consumers
- dependency and change graph, frequency of cross-component changes, compatibility policy, release coupling, and versioning needs
- confidentiality, least-privilege access, regulated separation, vendor access, open-source boundaries, and export controls
- repository size and growth, files and binaries, history, branches and tags, clone and fetch behavior, CI fan-out, cache, and hosting limits
- code review, ownership, merge, release, incident, archive, migration, and disaster-recovery workflows

## Safety and Permission Constraints

- Repository placement is not an authorization boundary unless the host and workflow enforce the required access. Do not put material with incompatible visibility or legal obligations together merely for convenience.
- Keep generated artifacts and large binaries out of ordinary Git history unless an explicitly reviewed storage mechanism and retention need justify them. Deleting a current file does not remove it from history.
- Monorepo tools, remote caches, CI actions, generators, migration utilities, and hosted integrations are executable or networked assets requiring version-specific review.
- Preserve authorship, licenses, tags, release provenance, issue and review evidence, and required history during moves. Do not rewrite shared history or delete source repositories without explicit authorization and a verified backup.
- Creating or migrating private repositories, changing access, publishing code, rotating credentials, rewriting history, or archiving the last authoritative copy is R3 when it affects external systems or recoverability.

## Workflow

1. Map components, owners, consumers, visibility, releases, deployments, licenses, data or secret exposure, and change relationships. Identify changes that must be atomic and components that must be isolated.
2. Compare one repository, several repositories, and a hybrid on cross-project refactors, review, ownership, access, CI scope, release independence, package publishing, incident blast radius, discoverability, onboarding, hosting limits, and exit cost.
3. Choose repository boundaries from the strongest constraints. Security, legal, visibility, archival, and ownership boundaries can override convenience; frequent atomic change can justify colocation when access permits it.
4. Inside each repository, define root responsibilities, workspace or package boundaries, dependency direction, ownership, public exports, generated-code location, and artifact storage. Avoid one undifferentiated dependency graph.
5. Define change detection and affected scope from the real dependency graph. A path filter alone is unsafe when transitive dependencies, configuration, schemas, toolchains, or shared infrastructure can affect downstream outputs. In a monorepo, use affected-graph CI — build, test, and release only the packages a change actually reaches, computed from that graph. Tooling such as Turborepo or Nx provides this; without it a monorepo degrades into a slow polyrepo that carries shared overhead without the coordination benefit. No current usage or share survey for Turborepo versus Nx was retrieved, so do not cite one as a reason to prefer either.
6. Protect source and review policy: branch or ruleset coverage, required checks, ownership, bypass, tag and release controls, sensitive paths, automation identity, and audit. Test rules on the default and release branches actually used.
7. Measure clone, checkout, status, history, review, CI queue, cache, and release behavior at expected scale. Use sparse checkout or partial clone only after documenting offline, missing-object, tooling, and host support.
8. Define package and service compatibility whether code is co-located or separate. Atomic commits do not remove the need for runtime deployment order, data migration, rollback, or compatibility with existing consumers.
9. Migrate incrementally with immutable source references, history and attribution preservation, dual-build or package bridges where required, permission verification, consumer cutover, and a recovery copy. Remove the bridge only after reconciliation.
10. Review repository health and topology when access, ownership, release cadence, build time, scale, licensing, acquisition, open-source plans, or collaboration patterns materially change.

## Required Output

- component, ownership, visibility, dependency, change, and release map
- topology comparison, selected repository boundaries, ADR, and rejected alternatives
- workspace or package structure, allowed dependencies, ownership, review and source-protection policy
- affected-build, cache, package, compatibility, versioning, and release design
- measured scale evidence plus migration, history, permission, rollback, archive, and exit plan

## Completion Gate

Do not call topology ready until visibility and ownership are enforceable, critical cross-component changes and independent releases are supported, affected builds account for transitive inputs, repository operations meet measured targets, branch and tag protections are tested, and split or merge migration can be reversed without losing source, history, attribution, or release evidence.

## Conditional Reference

Read [Repository Topology Evidence](references/repository-topology-evidence.md) when evaluating host limits, ownership controls, sparse or partial checkout, large-repository mitigation, or source protection.
