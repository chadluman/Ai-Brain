# Software Supply Chain Evidence

Verified 2026-10-21. Standards describe evidence formats and control levels; they do not certify an artifact by existence alone.

- [NIST SSDF 1.1](https://csrc.nist.gov/pubs/sp/800/218/final) defines secure software-development practices across preparation, protection, production, and vulnerability response.
- [SLSA 1.2](https://slsa.dev/spec/v1.2/about) provides incrementally adoptable source and build supply-chain requirements. Its provenance is verifiable information about where, when, and how an artifact was produced; higher levels increase guarantees and cost.
- [SPDX specifications](https://spdx.dev/use/specifications/) list SPDX 3.0 as current when verified and identify SPDX as ISO/IEC 5962:2021. Select a supported profile and serialization rather than assuming every tool supports the whole model.
- [CycloneDX specification](https://cyclonedx.org/specification/overview/) lists version 1.7 as current when verified and models components, services, dependencies, compositions, vulnerabilities, formulation, and other supply-chain information.
- [OpenSSF Scorecard](https://github.com/ossf/scorecard) is the canonical repository for automated open-source security-health checks. Read individual checks and evidence; the aggregate is a heuristic, not approval.

## Evidence Boundaries

- An SBOM is an inventory claim. Check completeness, exact versions, hashes, build stage, and whether generated or bundled code is represented.
- Provenance is useful only when its signer, builder identity, inputs, artifact digest, and consumer verification policy are trusted.
- A signature proves control of a key under a policy; it does not prove code safety, maintainer intent, license compatibility, or vulnerability absence.
- A clean vulnerability scan is time-bound and limited to its databases, reachability model, and configured scope.

Keep review records concise and link to immutable evidence instead of copying large external reports into the vault.
