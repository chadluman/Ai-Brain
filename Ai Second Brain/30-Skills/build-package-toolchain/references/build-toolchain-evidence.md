# Build Toolchain Evidence

Verified: 2026-10-21

## Primary Guidance

- [npm `package-lock.json` documentation](https://docs.npmjs.com/cli/v11/configuring-npm/package-lock-json/) describes the lockfile as an exact dependency-tree record intended for source control and reproducible team, deployment, and CI installation.
- [npm `ci` documentation](https://docs.npmjs.com/cli/v11/commands/npm-ci/) documents clean automated installation from an existing lockfile and failure when the manifest and lockfile disagree.
- [npm lifecycle-script documentation](https://docs.npmjs.com/cli/v11/using-npm/scripts/) documents hooks that can execute during install, packing, publishing, and other commands. Treat every hook as executable third-party code.
- [npm provenance guidance](https://docs.npmjs.com/generating-provenance-statements/) documents registry provenance statements for supported CI publishing. Provenance is useful evidence, not proof that a package is safe.
- [SLSA 1.2](https://slsa.dev/spec/v1.2/about) supplies a broader source and build provenance model for assessing build integrity.

## Interpretation Boundaries

- npm documentation is a concrete provider example. pnpm, Yarn, Bun, language-specific managers, and framework tools require their own exact-version documentation and review.
- A lockfile improves repeatability but can faithfully reproduce a malicious dependency. It does not replace source, advisory, license, or behavior review.
- Disabling lifecycle scripts can reduce risk but can also break packages that legitimately require them. Review and allow only the necessary hooks.
- A successful build does not prove runtime correctness, security, accessibility, browser compatibility, or deployability.
