# Hosting Runtime Evidence

Verified: 2026-10-21

## Standards and Durable References

- [NIST SP 800-145](https://csrc.nist.gov/pubs/sp/800/145/final) defines cloud essential characteristics and the IaaS, PaaS, and SaaS service models. Its 2011 terminology is durable but does not cover every modern provider product.
- [Open Container Initiative](https://opencontainers.org/) maintains open image, runtime, and distribution specifications. OCI compatibility improves artifact portability but does not make provider networking, orchestration, identity, storage, or operations portable.
- [OCI Runtime Specification](https://specs.opencontainers.org/runtime-spec/) and [OCI Image Specification](https://specs.opencontainers.org/image-spec/) define current standardized runtime bundle and image formats. Pin exact versions for implementation.
- [HTTP Caching, RFC 9111](https://www.rfc-editor.org/rfc/rfc9111.html) defines cache storage and reuse semantics relevant to browsers, CDNs, and reverse proxies.
- [Google SRE: Implementing SLOs](https://sre.google/workbook/implementing-slos/) helps translate user reliability needs into measurable service objectives rather than selecting a provider by feature list alone.

## Interpretation Boundaries

- Static, function, container, and VM are execution models, not quality tiers. Workload shape and operational constraints determine fit.
- Managed services can reduce operations while increasing provider coupling. Measure export and replacement boundaries, not just deployment ease.
- Provider feature, region, quota, runtime, support, and pricing claims age quickly and must be verified immediately before an ADR or purchase.
- Portability is only meaningful when artifacts, data, configuration, identity, observability, and operational procedures can all move within the required time.
