---
name: cryptography-key-management
description: Design or review application cryptography and key management across data classification, algorithms, libraries, key hierarchy, storage, access, rotation, recovery, compromise, deletion, crypto agility, and post-quantum migration. Use when encryption, signing, hashing, token protection, or managed key services are material; do not invent cryptographic primitives.
---

# Cryptography and Key Management

## Outcome

Produce a threat-driven cryptographic design whose approved primitives and keys are inventoried, isolated, least-privileged, rotatable, recoverable where required, destroyable, and replaceable without losing necessary data.

## Required Inputs

- data classes, adversaries, confidentiality duration, integrity, authenticity, non-repudiation, jurisdiction, and compliance needs
- data states and flows, clients, servers, regions, backups, exports, logs, caches, indexes, analytics, and deletion obligations
- use cases for encryption, signatures, MACs, hashing, password storage, token protection, key derivation, random generation, and transport
- platforms, protocols, maintained libraries, managed key or HSM services, trust boundaries, administrators, and disaster scenarios
- existing algorithms, certificates, keys, owners, locations, versions, cryptoperiods, usage volume, dependencies, and migration deadlines

## Safety and Permission Constraints

- Minimize or avoid storing sensitive data before adding encryption. Encryption does not correct excessive collection, weak authorization, endpoint compromise, or unsafe plaintext use.
- Use maintained platform protocols and well-reviewed libraries implementing standardized constructions. Do not design custom algorithms, modes, padding, key exchange, randomness, or serialized envelopes.
- Keep keys distinct by purpose, tenant or domain where required, environment, algorithm, and lifecycle. Never store plaintext keys beside ciphertext or commit them to source, images, artifacts, logs, or the vault.
- Treat managed KMS, HSM, libraries, providers, plugins, and migration tools as R2 or R3 assets requiring exact-version and permission review. Creating production keys, changing policies, rotating active keys, decrypting real data, or destroying key material is R3 and requires immediate authorization and recovery evidence.
- Destruction can make data permanently unreadable. Verify retention, legal hold, backup, escrow or recovery policy, and blast radius before deletion or disabling old keys.

## Workflow

1. Define the security property and threat for every proposed cryptographic use. Distinguish encryption, integrity, authentication, signatures, hashing, password storage, transport, tokenization, and secret management.
2. Inventory cryptographic dependencies and material: data, protocols, algorithms, modes, parameters, certificates, trust anchors, libraries, services, keys, aliases, owners, locations, access, backups, and consumers.
3. Select current standardized protocols and maintained implementations for the target platform and regulator. Record the exact version, parameters, hardware or module requirements, interoperability, performance, and deprecation triggers.
4. Design a key hierarchy and envelope where useful. Separate data-encryption and key-encryption keys, purposes, environments, tenants or domains, and administrator roles; bind ciphertext to algorithm, key ID, version, context, and authenticated metadata.
5. Generate keys with approved cryptographic randomness inside the strongest practical boundary. Prevent raw export where possible, restrict encrypt, decrypt, sign, verify, wrap, unwrap, rotate, disable, and delete permissions separately, and audit administration and use.
6. Define cryptoperiod and usage limits from data lifetime, primitive and mode limits, threat, compliance, compromise exposure, and operational feasibility. Rotation must create new writes safely while old data remains readable or is deliberately re-encrypted.
7. Design restore and disaster behavior. Determine which keys must be recoverable, how quorum or split control works, how backups remain decryptable, and how recovery is tested without exposing production material.
8. Prepare compromise response: identify affected ciphertext and signatures, stop use, revoke or disable, rotate, re-encrypt or re-sign, invalidate dependent credentials, investigate access, notify as required, and preserve necessary evidence.
9. Build crypto agility. Keep algorithms and key IDs versioned behind a narrow interface, support dual-read or hybrid transitions when justified, inventory quantum-vulnerable public-key uses, and track NIST post-quantum standards and protocol support without inventing a migration construction.
10. Test known-answer and negative cases, tampering, wrong key and context, nonce or IV uniqueness, rotation during traffic, partial re-encryption, old backup restore, unavailable key service, revoked access, corrupt metadata, compromise drill, and authorized destruction.

## Required Output

- data and threat map with required cryptographic properties and non-cryptographic controls
- cryptographic inventory with exact standards, libraries, protocols, parameters, owners, and deprecation triggers
- key hierarchy, storage, access, separation, metadata, generation, distribution, use, rotation, recovery, compromise, and destruction design
- ciphertext or signature format and migration compatibility plan
- crypto-agility and post-quantum discovery, prioritization, interoperability, and transition plan
- test evidence, operational runbooks, rollback or recovery, residual risks, and re-review triggers

## Completion Gate

Do not call the design ready until every use maps to a required security property, keys and algorithms are inventoried and access-controlled, rotation and old-data readability are proven, backup restore and compromise recovery pass, unauthorized tampering and use fail, destruction is governed, and an implementation or algorithm change has a tested migration path.

## Conditional Reference

Read [Cryptography and Key Evidence](references/cryptography-key-evidence.md) when choosing key lifecycle controls, interpreting current NIST status, or planning post-quantum transition.
