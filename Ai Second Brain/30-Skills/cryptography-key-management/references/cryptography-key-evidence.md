# Cryptography and Key Evidence

Verified: 2026-10-22

## Current Standards and Guidance

- [NIST key-management project](https://csrc.nist.gov/Projects/Key-Management/Key-Management-Guidelines) identifies SP 800-57 Part 1 Rev. 5 as final and Rev. 6 as a December 2025 initial public draft. It also records SP 800-131A Rev. 3 as an initial draft while Rev. 2 remains final.
- [NIST SP 800-57 Part 1 Rev. 5](https://csrc.nist.gov/pubs/sp/800/57/pt1/r5/final) is the current final general key-management recommendation covering material types, protection, inventory, access, lifecycle, compromise, backup, recovery, and cryptoperiods.
- [NIST SP 800-57 Part 1 Rev. 6 initial public draft](https://csrc.nist.gov/pubs/sp/800/57/pt1/r6/ipd) adds newer algorithms and key-encapsulation and destruction material. It is draft evidence, not a replacement for the final publication.
- [NIST post-quantum cryptography](https://www.nist.gov/pqc) identifies finalized FIPS 203, 204, and 205 and says migration planning should begin. Protocol, library, platform, module, performance, interoperability, and compliance support still require exact implementation proof.
- [NIST IR 8547 initial public draft](https://csrc.nist.gov/pubs/ir/8547/ipd) describes an expected transition from quantum-vulnerable standards. Its status is draft and its proposed dates must not be presented as final universal deadlines.
- [OWASP Cryptographic Storage Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html) emphasizes threat-driven placement, minimizing stored data, maintained libraries, authenticated encryption, key separation, usage limits, rotation, and crypto agility.
- [OWASP Key Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Key_Management_Cheat_Sheet) maps generation, storage, distribution, use, compromise, recovery, revocation, and destruction concerns for application teams. Verify referenced standards and platform capabilities independently.

## Decision Implications

- State whether a cited NIST document is final or draft. Do not silently merge proposed changes into a production requirement.
- Inventory first. Post-quantum planning needs to know which protocols, certificates, signatures, key exchanges, libraries, devices, archives, and data lifetimes are quantum-vulnerable.
- Prefer protocol and library upgrades supplied by competent maintainers over application-built hybrid constructions.
- Rotation needs both new-write behavior and old-data recovery. Destroying the last usable key is destructive data deletion.
- A managed key service reduces exposure only when policies, identities, logging, regions, recovery, quotas, and operator roles are designed and tested.
