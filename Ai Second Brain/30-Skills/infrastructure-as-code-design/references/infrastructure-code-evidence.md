# Infrastructure as Code Evidence

Verified: 2026-10-21

## Primary Guidance

- [NIST SSDF 1.1](https://csrc.nist.gov/pubs/sp/800/218/final) provides secure software-development practices that apply to infrastructure definitions and their delivery pipeline.
- [SLSA 1.2](https://slsa.dev/spec/v1.2/about) provides source and build provenance concepts for the tools, modules, providers, and artifacts in an infrastructure workflow.
- [OpenTofu state and plan encryption](https://opentofu.org/docs/language/state/encryption/) documents that plans and state can contain sensitive values, explains encryption scope and key-loss risk, and calls for backup and recovery preparation. Verify the page for the selected OpenTofu version.
- [OpenTofu state documentation](https://opentofu.org/docs/language/state/) describes the mapping between declared configuration and remote objects. It is product-specific evidence, not a universal state model.
- [OWASP Secrets Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html) covers secret lifecycle, least privilege, automation, rotation, audit, and CI/CD exposure relevant to infrastructure pipelines.

## Interpretation Boundaries

- Encryption at rest does not prevent an authorized plan or apply process from seeing values it needs, and key loss can make state unrecoverable.
- A successful plan is a provider-specific prediction, not a guarantee that apply will succeed or that the resulting service is correct.
- External modules and providers are executable supply-chain inputs. Version pins and signatures support review but do not replace it.
- Terraform, OpenTofu, Pulumi, cloud-native templates, and configuration-management tools have different state, language, license, and migration properties; evaluate the exact version and ecosystem.
