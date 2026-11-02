---
name: workload-identity-federation
description: Design or review workload and service identity, attestation, federation, short-lived credentials, token exchange, mTLS, and trust-domain operations across cloud, cluster, CI, and hybrid environments. Use when replacing static machine secrets or authorizing service-to-service access.
---

# Workload Identity Federation

## Outcome

Produce a portable workload-identity system in which every runtime principal is attributable, narrowly authorized, environment-bound, short-lived, continuously verifiable, revocable, observable, and recoverable without shared static secrets.

Use [Secrets and Configuration Management](../secrets-config-management/SKILL.md) for the broader credential inventory, [Authorization and Tenancy Design](../authorization-tenancy-design/SKILL.md) for resource policy, and [Audit Log Design](../audit-log-design/SKILL.md) for authoritative access evidence. This skill owns machine identity, attestation, federation, and credential delivery.

## Required Inputs

- workloads, owners, runtimes, deployment identities, CI systems, clusters, clouds, regions, environments, tenants, services, jobs, devices, and human-to-workload boundaries
- issuer and verifier trust domains, attestation evidence, identity naming, audiences, resources, actions, delegation, impersonation, and downstream chains
- current static keys, certificates, API credentials, metadata services, service accounts, rotation, revocation, bootstrap, and break-glass paths
- runtime, proxy, mesh, gateway, KMS or HSM, identity-agent, control-plane, clock, network, availability, latency, and portability constraints
- compromise, orphaning, image theft, build tampering, replay, confused-deputy, cross-environment, cross-tenant, and provider-outage threats

## Safety and Permission Constraints

- Network location, cluster membership, image name, repository, or cloud account alone is not sufficient identity. Bind issuance to verified runtime and deployment evidence plus an explicit policy.
- Prefer short-lived credentials and non-exportable keys. Do not place bootstrap secrets, private keys, bearer tokens, or real attestation evidence in images, source, CI output, logs, telemetry, plans, tickets, or the vault.
- Federation removes stored secrets only if the external trust configuration, subject mapping, audience, conditions, and token exchange are narrower than the credential it replaces.
- Do not allow arbitrary token exchange, audience selection, subject impersonation, or transitive delegation. Every actor, subject, target and scope combination needs policy and audit.
- Installing an identity agent, SDK, sidecar, proxy, trust bundle, or provider integration is R2. Changing production trust, issuing or revoking real credentials, or granting workloads external access is R3 and requires immediate authorization, staged rollout, and rollback.

## Workflow

1. Inventory every workload principal and existing credential with owner, runtime, environment, tenant, purpose, resources, actions, storage, lifetime, issuer, consumers, and last use. Remove shared and orphaned identities from the target design.
2. Draw the issuance and request path: workload, attestor, identity agent or control plane, issuer or security-token service, key boundary, trust bundle, resource verifier, policy engine, logs, and revocation signal.
3. Define a stable identity namespace and trust domains. Separate production from non-production and tenants where risk requires it; bind identity to deployed workload facts rather than mutable display names.
4. Select attestation evidence the platform can verify, such as signed workload deployment, hardware or instance identity, orchestrator service account, or CI provenance. Document bootstrap, replay defenses, stale evidence, cloned workloads, and control-plane compromise.
5. Issue the minimum credential for the minimum time and audience. Prefer locally generated non-exportable keys, automatic rotation, and narrowly scoped X.509 or token identities; distinguish identity from authorization policy.
6. When federating, validate exact issuer, subject and actor mapping, audience or resource, token type, time, signature, trust chain, and required context. Use token exchange only with explicit delegation or impersonation semantics and bounded downstream propagation.
7. Choose mTLS, DPoP, signed client assertions, or bearer delivery according to threat, library, proxy, and verifier support. Prove sender constraints survive termination and forwarding boundaries end to end.
8. Design trust-bundle, issuer-key, certificate, policy, attestor, and provider rotation with overlap, cache behavior, clock skew, emergency revocation, compromised issuer isolation, and rollback. Define safe behavior during control-plane or network outage.
9. Authorize every request at the resource from trusted workload identity, resource, action, tenant, environment, and current policy. Log issuance, exchange, denied use, administration, and anomalous identity churn without logging credential contents.
10. Test invalid issuer, subject, audience, actor, scope, time, signature, attestation, environment and tenant; cloned and terminated workloads; replay; excessive delegation; key and trust-bundle rotation; unavailable issuer or agent; revoked policy; clock error; and static-secret removal.

## Required Output

- workload and credential inventory, trust-domain and identity namespace, and issuance and request data-flow map
- attestation, bootstrap, key boundary, credential format, lifetime, audience, delivery, rotation, revocation, and outage design
- federation and token-exchange mappings with delegation, impersonation, sender-constraint, and authorization rules
- policy ownership, audit, monitoring, compromise, migration, rollback, provider exit, and static-secret retirement plan
- negative, rotation, outage, replay, tenant, environment, and orphan-cleanup test evidence

## Completion Gate

Do not call the design ready until each workload has a unique attributable identity and owner, federation mappings are exact, credentials are short-lived and narrowly usable, authorization is enforced at the resource, static replacements are revoked, rotation and outage pass, terminated workloads lose access promptly, and cross-environment, cross-tenant, replay, and confused-deputy tests fail safely.

## Conditional Reference

Read [Workload Identity Federation Evidence](references/workload-identity-evidence.md) when choosing trust domains, attestation, token exchange, sender constraints, zero-trust policy, or a portable SPIFFE-compatible design.
