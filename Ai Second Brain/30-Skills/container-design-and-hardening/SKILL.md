---
name: container-design-and-hardening
description: Design hardened container images with multi-stage builds, minimal bases, pinned tags and digests, non-root execution, read-only filesystems, secret handling, scanning, signing, and SBOMs. Use when building or shipping container images for deployment.
---

# Container Design and Hardening

## Outcome

Produce container images that are small, reproducible, and defensible: only the application and what it needs at runtime, built reproducibly, run with least privilege, scanned, signed, and traceable to their source.

Use [CI/CD and Release Design](../ci-cd-release-design/SKILL.md) for the pipeline that builds and promotes images, and [Hosting and Runtime Selection](../hosting-runtime-selection/Hosting%20and%20Runtime%20Selection.md) for where the images run.

## Snapshot and re-check

Research for this skill was checked 2026-11-09. Treat image-hygiene practice as durable, but re-check tool versions, platform features, and policy dates before citing them — they are a 2026-11-09 snapshot and may have moved on.

## Multi-stage builds and minimal bases

Multi-stage builds are table stakes: build in a fat builder stage with the toolchain, then copy only the built artifacts into a slim runtime stage. The runtime image should contain the application and its runtime dependencies, not the compiler, the package manager, or the build cache.

Minimal or distroless base images strip the shell, package manager, and debug tools from the runtime image. Docker Hardened Images follow this model. The trade-off is real: a fat base image carries most of its vulnerabilities in operating-system packages rather than in application code, so shrinking the base shrinks the vulnerability surface — but vendor claims about how much vulnerability reduction a minimal image achieves are marketing, not independently reproduced, so treat any such figure as unverified and do not cite it as fact.

## Pinning

Never use the `:latest` tag for anything that matters: it is a moving target, so a rebuild can silently change the base image and a rollback cannot reproduce what ran. Pin base image tags, and pin the image digest where reproducibility matters, so the exact image is recorded and repeatable. Keep a `.dockerignore` so build context stays small and stray files — including anything that looks like a secret — never reach the build.

## Runtime hardening

- **Run as non-root.** Give the container a dedicated, unprivileged user. A process that escapes its container as root is a different incident from one that escapes as an unprivileged user.
- **Read-only root filesystem.** Mount the root filesystem read-only and give the application only the writable paths it genuinely needs. This limits what a compromised process can change and makes tampering visible.
- **No secrets in the image.** Never put secrets in environment variables baked into the image, in build arguments, or in any layer — layers are history and cannot be un-shipped. Use BuildKit secrets at build time and inject runtime credentials at run time from a secret store.

## Scanning, signing, and SBOMs

- **Scan in CI.** Scan images with a scanner such as Trivy or Docker Scout on every build, and fail the build on high or critical findings by a stated threshold. Scanning is a gate, not a report nobody reads.
- **Sign images.** Sign with cosign and Sigstore so a deployed image can be proven to be the image that was built and reviewed, not a substitute.
- **Generate SBOMs.** Produce a software bill of materials for each image so that when a vulnerability is announced, the team can answer "are we affected?" by looking at the inventory instead of guessing.
- **Registries.** Push to a registry that fits the deployment — common choices include GitHub Container Registry, Docker Hub, AWS ECR, Google Artifact Registry, and Azure Container Registry. Most offer built-in scanning; use it as a second layer, not as the only scan.

Use [Software Supply Chain Review](../software-supply-chain-review/SKILL.md) for the wider review of dependencies, build inputs, and artifact provenance, and [Dependency Upgrade Operations](../dependency-upgrade-operations/Dependency%20Upgrade%20Operations.md) for keeping base images and dependencies current.

## Debugging without weakening the image

Distroless images are harder to debug because there is no shell inside them. Do not solve that by shipping debug tools in the production image — that hands an attacker the same tools. Use a debug sidecar or an ephemeral debug container attached to the same environment instead, so the production image stays minimal and the debugging capability stays separate and short-lived.

## Failure modes

- A fat base image whose vulnerabilities live in operating-system packages the application never uses.
- `:latest` in a deployment, so nobody can say which image is actually running.
- A secret baked into a layer, discovered later, that cannot be removed without rebuilding and rotating.
- Debug tooling shipped in production "temporarily" and never removed.

## Supporting skills

- [CI/CD and Release Design](../ci-cd-release-design/SKILL.md) — building, tagging, scanning, and promoting images in the pipeline.
- [Hosting and Runtime Selection](../hosting-runtime-selection/Hosting%20and%20Runtime%20Selection.md) — where images run and what the runtime provides.
- [Software Supply Chain Review](../software-supply-chain-review/Software%20Supply%20Chain%20Review.md) — dependencies, build inputs, SBOMs, and artifact provenance.
- [Dependency Upgrade Operations](../dependency-upgrade-operations/Dependency%20Upgrade%20Operations.md) — keeping base images and dependencies current, including rebuilds on upstream changes.

## State

Risk: R0 (draft).
Draft pending representative validation.
