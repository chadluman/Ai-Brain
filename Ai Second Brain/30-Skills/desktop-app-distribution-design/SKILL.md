---
name: desktop-app-distribution-design
description: Ship a signed, auto-updating desktop app that users and operating systems can trust, with a rollback path when an update fails. Use when distributing a desktop app outside a store or through one; do not use for mobile store release, which is covered by Mobile Release Operations, or for the in-app shell, which is covered by Desktop Web Shell Design.
---

# Desktop App Distribution Design

## Outcome

Produce a release pipeline that signs every installer and update, proves the update came from you before installing it, rolls out in stages, and can be rolled back, so users never have to choose between an untrusted download and a broken update.

Use [Mobile Release Operations](../mobile-release-operations/SKILL.md) for the mobile-store analogue. Use this skill for desktop, where there is no single store gate and signing, notarization, and updater integrity are the product's own responsibility.

## Required Inputs

- The target operating systems and install formats: for example, macOS app and disk image, Windows installer, and Linux package or AppImage.
- The signing identities and their owners: who holds each certificate and updater key, where they are stored, and who can rotate them.
- The update channel model: stable, beta, or both, and who receives each channel.
- The rollout and rollback policy: canary size, staged percentages, pause criteria, and what happens when an update fails on a user's machine.
- The release artifacts: installer, update payload, signature files, release notes, and version metadata, and where each is published.

If there is no signing identity for an operating system, do not ship for that system as if signing were optional. An unsigned desktop app teaches users to bypass the operating system's trust warnings.

## Workflow

1. Sign installers and updates per operating system, in the release pipeline, not on a developer machine. On macOS, sign with a Developer ID identity, submit for notarization, and staple the ticket; on Windows, sign with an Authenticode certificate; on Linux, ship checksums and, where a package repository is used, repository signing. Record which identity signed each release.
2. Sign updates with a dedicated updater key, and bake the matching public key into the app at build time. The updater must verify the signature before installing anything. An unsigned update is the worst supply-chain vector a desktop app has, because it runs with the user's trust already granted.
3. Never regenerate an updater key casually. Already-installed apps carry the old public key and will reject updates signed with a new one, with no in-app recovery. A key rotation is a migration plan, with a signed transition release and a manual reinstall path, not a secret rotation.
4. Roll out in stages: a canary group first, then increasing percentages, with a pause switch that stops the rollout without shipping new code. Monitor install success, launch success, and crash rates per stage before advancing.
5. Keep the previous version recoverable. An update that fails to launch must leave the user able to return to the last working version, by keeping the previous install, by offering a signed manual download, or by both. Test the failure path, not only the success path.
6. Test the full matrix before a public release: clean install, update from the previous version to the new version, and update from two versions back, on each target operating system, on a clean machine. A pipeline that only tests clean installs will miss updater failures.
7. Keep signing secrets in the release pipeline's secret store, with access limited to the release role, and never in the repository, in build logs, or in an installer. A leaked signing key is a release-incident, with revocation and rotation, not a quiet replacement.

## Safety and Permission Boundaries

- Treat the release pipeline as a security boundary. Anyone who can push an unsigned or mis-signed update can push code to every user's machine.
- Never ship a build that was not signed by the pipeline, and never ask users to disable Gatekeeper, SmartScreen, or equivalent protections to install your app. If the operating system blocks the install, fix the signing, not the user's settings.
- A new packaging, signing, or updater tool still requires the root security-review gate at its exact version, and its supply chain is reviewed under [Software Supply Chain Review](../software-supply-chain-review/SKILL.md). This skill approves no provider or package.

## Outputs and Evidence

- A per-OS signing, notarization, and updater-key design, with key owners and storage.
- A rollout, pause, and rollback policy, with the failure path a user follows when an update breaks.
- A release checklist covering clean install, previous-version update, and two-versions-back update on each OS.
- Tests or a test report for that matrix, with the canary and staged-rollout results for the release.
