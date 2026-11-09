---
name: ci-cd-release-design
description: Design or review continuous integration, artifact promotion, deployment, verification, and rollback for a software project. Use for new pipelines, production release gates, environment strategy, or deployment-risk reduction; do not deploy or change production without explicit authorization.
---

# CI/CD and Release Design

## Outcome

Produce a repeatable release path that builds once from reviewed inputs, promotes a verifiable artifact, limits credentials and blast radius, detects failure quickly, and can stop or recover safely.

Read [release evidence](references/release-evidence.md) before selecting provenance, CI identity, or rollout controls.

## Inputs

Establish repositories and branch policy, artifact types, environments, test and security gates, data and schema changes, deployment target, release frequency, risk class, availability and SLOs, approvals, secret and identity model, platform limitations, rollback time, compliance evidence, and operators.

## Workflow

1. Map source change through review, build, test, packaging, provenance, registry, promotion, deployment, verification, and recovery. Name the trust boundary and owner at each step.
2. Treat pull-request content and third-party workflow code as untrusted. Prevent untrusted code from reaching release credentials, protected environments, caches containing secrets, or privileged runners.
3. Pin and review actions, images, tools, dependencies, and reusable workflows. Use isolated ephemeral workers where feasible and minimize workflow and token permissions.
4. Build an immutable artifact once from an identified revision. Record its digest and provenance, retain required test evidence, and promote the same artifact rather than rebuilding per environment.
5. Prefer short-lived, narrowly scoped workload identity over stored long-lived credentials. Bind identity to the repository, workflow, revision or protected environment needed for the action.
6. Define environment separation, approvals, concurrency, change windows when justified, configuration ownership, secret injection, and audit history.
7. Keep application and schema changes backward-compatible across the rollout window. Separate irreversible migrations and destructive cleanup from ordinary deploys.
8. Choose rollout and rollback from risk: direct, rolling, blue/green, canary, feature flag, or another controlled method. Define automatic pause and rollback signals from user impact, correctness, security, and capacity.
9. Verify the running artifact, configuration, health, critical journey, observability, and data behavior. Exercise rollback and roll-forward before relying on either.

## 2026 Currency: Identity, Pinning, Signing, Speed, and Gates

- Prefer short-lived workload identity through OIDC federation over stored long-lived cloud secrets; a stored secret that never rotates is a standing credential, and rotation is not a substitute for removing it. Step 5 already requires short-lived identity; record OIDC as the mechanism.
- Pin workflow actions, reusable workflows, and container images by commit SHA or digest, not by mutable tag or branch, and review the pinned content before adopting a new pin.
- Sign built container images and publish a software bill of materials (SBOM) with the artifact, so promotion and deployment can verify what was built and from what. See [Container Design and Hardening](../container-design-and-hardening/SKILL.md) for image construction and [Software Supply Chain Review](../software-supply-chain-review/SKILL.md) for provenance review.
- Set a pipeline speed target and measure it: a cited 2026 figure treats under 30 minutes for the main pipeline as the target, with engineers reported to stop waiting past about 45 minutes. Treat both figures as cited targets, not measured properties of any project; a pipeline slower than its target needs a named owner and a reduction plan, not acceptance.
- Make release gates required, not advisory: a gate that can be skipped without a recorded exception and owner is a report, not a control. Record which gates block promotion, who can grant an exception, and where the exception is logged.

## Permission Boundaries

- Editing a local pipeline is R2. Creating credentials, changing repository or cloud settings, publishing artifacts, deploying, promoting, rolling back production, or mutating real data is R3.
- Never expose secrets in workflow files, command output, artifacts, caches, logs, pull-request contexts, or the vault.
- Approval gates must protect a consequential boundary; avoid ceremonial approvals that add delay without reducing risk.
- A successful job means its configured commands passed, not that the product or release is correct.

## Completion

Deliver the trust and artifact flow, pinned inputs, permission model, gates, environment controls, artifact and provenance policy, rollout and data-change strategy, observability and stop conditions, verified rollback or roll-forward procedure, audit and retention evidence, costs, and unresolved risks.
