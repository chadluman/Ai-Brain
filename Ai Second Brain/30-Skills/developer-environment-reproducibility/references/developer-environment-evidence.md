# Developer Environment Evidence

Verified: 2026-10-22

## Current Sources

- [Development Containers specification](https://containers.dev/) is an open metadata specification for development-specific container settings, tools, and configuration. Its reference implementations, images, features, and editor integrations are separate executable assets requiring exact-version review.
- [Development Containers overview](https://containers.dev/overview) distinguishes development from production images and describes reuse across local, CI, and test workflows. Similarity improves consistency but does not establish production parity or isolation.
- [NIST SP 800-218](https://csrc.nist.gov/pubs/sp/800/218/final) remains the current final SSDF 1.1 baseline; NIST publicly reported update work in 2026. Its protection-of-software and development-environment practices support least privilege, provenance, and separation without requiring a particular local platform.
- [SLSA 1.2 requirements](https://slsa.dev/spec/v1.2/requirements) are approved requirements for source and build tracks. SLSA provenance and isolated hosted builds can strengthen release evidence, but they do not make a developer laptop or dev container reproducible by themselves.
- [Reproducible Builds definition](https://reproducible-builds.org/docs/definition/) distinguishes reproducing identical outputs from merely repeating setup. Achieving bit-for-bit reproducibility requires declared inputs and control of timestamps, paths, ordering, locale, toolchains, and other nondeterminism.

## Decision Implications

- “Works in a container” and “securely isolated” are different claims. Review host mounts, sockets, capabilities, network, credentials, image provenance, and update behavior.
- Pinning every byte forever prevents maintenance. Pair deterministic input resolution with an owned, tested update cadence and rollback.
- Local and CI should share commands and declared inputs, while production images should omit development tools and credentials. One image for every purpose is not automatically safer.
- Synthetic deterministic data is part of environment reproducibility. Production snapshots add privacy, retention, authorization, and contamination risk and should not be the default.
- State the evidence level precisely: repeatable setup, functionally equivalent build, or bit-for-bit reproducible artifact are different outcomes.
