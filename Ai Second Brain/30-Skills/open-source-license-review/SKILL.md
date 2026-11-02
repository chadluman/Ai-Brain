---
name: open-source-license-review
description: Identify and assess open-source and source-available license obligations for an exact software or content version and intended use. Use before copying, modifying, embedding, linking, distributing, hosting, selling, or approving a third-party asset when license scope or compatibility matters.
---

# Open Source License Review

## Outcome

Produce a version-specific license evidence record that maps every material component and file class to its stated terms, identifies use and distribution triggers, records obligations and unresolved conflicts, and routes legal interpretation to an authorized expert.

## Required Inputs

- exact asset, source URL, author or organization, version or commit, acquisition date, and checksum when available
- complete file inventory, nested archives, submodules, vendored code, generated output, binaries, fonts, media, models, data, documentation, and patches
- license files, notices, copyright statements, file headers, package metadata, dependency manifests, lockfiles, and contributor terms
- intended internal use, modification, linking, embedding, SaaS or network use, distribution, sale, app-store delivery, and recipient jurisdictions
- product licenses, proprietary boundaries, patents, trademarks, attribution surface, source-offer process, and release workflow

## Safety and Permission Constraints

- This skill organizes evidence and risk; it does not provide legal advice or declare legal compliance. Escalate ambiguous, conflicting, reciprocal, patent, trademark, data, model, export, or jurisdiction-sensitive questions to qualified counsel.
- Do not assume that public source, free download, GitHub hosting, an SPDX identifier, or a package-level license grants rights to every file or dependency.
- Do not clone, install, build, run, import, publish, distribute, or upload the asset merely to inspect licensing. Treat executable review separately under the root safety gate and use an isolated environment when authorized.
- Unknown provenance, missing or conflicting terms, copied assets without a grant, or obligations the project cannot meet require quarantine. Silence is not permission.
- Record license findings independently from security, privacy, maintenance, telemetry, and dependency risk; passing one review does not approve the asset.

## Workflow

1. Freeze the subject: exact source, immutable version, complete package boundary, intended use, modification, interaction, and distribution path.
2. Inventory every file class and nested component. Record origin, copyright holder, license statement, notices, generated or vendored status, and unexplained gaps.
3. Normalize stated licenses and exceptions with current SPDX identifiers or `LicenseRef` where no listed identifier applies. Preserve original texts and do not rewrite license language.
4. Verify whether a license is OSI-approved only when the open-source label matters. Do not treat SPDX listing as OSI approval or compatibility evidence.
5. Map the intended facts that may change obligations: copy, modification, static or dynamic linking, process separation, plugin or API boundary, network service, conveyance, distribution of binaries or containers, app-store terms, and sale.
6. Extract obligations without guessing: attribution and notices, license text, modification marking, source or corresponding-source availability, offer duration, installation information, patent terms, trademark limits, and downstream license conditions.
7. Compare component obligations with the project's inbound and outbound terms and delivery channel. Flag incompatible conditions, missing notices, unavailable source, noncommercial or field-of-use restrictions, and terms that are source-available rather than open source.
8. Define the compliance artifact and owner for each obligation. Include bill of materials, notice bundle, source archive or offer, attribution placement, release approval, inquiry path, retention, and change control where applicable.
9. Record legal questions and risk. Obtain qualified approval before consequential reuse when interpretation or compatibility affects distribution, business model, patents, regulated work, or meaningful exposure.
10. Issue `approved`, `approved-with-conditions`, `quarantined`, `rejected`, or `retired` for the exact version and use. Define removal, replacement, and re-review triggers; any material version or use change invalidates the result.

## Required Output

- review subject, provenance, immutable version or checksum, acquisition and review dates
- complete component and file-class inventory with license evidence and gaps
- SPDX expressions where applicable plus original license and notice locations
- intended-use and distribution facts, obligations, owners, and compliance artifacts
- compatibility, patent, trademark, platform, and unresolved legal questions
- separate security and operational review status
- decision, conditions, test evidence, removal plan, and next review trigger

## Completion Gate

Do not approve reuse until the entire relevant package is inventoried, every material file class has supported terms, intended-use triggers are explicit, obligations have owners and a release path, conflicts are resolved, and required legal review is recorded. Approval applies only to the reviewed version and use.

## Conditional Reference

Read [Open Source License Evidence](references/open-source-license-evidence.md) when identifying licenses, recording file-level declarations, assessing an organizational compliance process, or distinguishing open source from source-available terms.
