# Dependency Upgrade Evidence

Verified: 2026-10-22

## Current Sources

- [Semantic Versioning 2.0.0](https://semver.org/) defines version meaning only relative to a declared public API and requires released contents not be modified in place. It is a communication contract, not proof of compatibility, quality, or safety.
- [GitHub Dependabot version updates](https://docs.github.com/en/code-security/concepts/supply-chain-security/dependabot-version-updates) documents current hosted update behavior and a default three-day cooldown for version updates. Provider defaults, supported ecosystems, credentials, grouping, and terms must be checked for the exact account and date.
- [GitHub configuring Dependabot version updates](https://docs.github.com/en/code-security/how-tos/secure-your-supply-chain/secure-your-dependencies/configure-version-updates) defines the current repository configuration and schedules. Enabling it creates external state and pull requests and is not authorized by this R0 evidence note.
- [OpenSSF guides](https://openssf.org/resources/guides/) route to current secure-development, source-control, package-repository, npm, and open-source evaluation guidance. OpenSSF tools and badges can identify questions but do not replace package inspection and project tests.
- [NIST SP 800-218](https://csrc.nist.gov/pubs/sp/800/218/final) remains the final SSDF 1.1 baseline while an update is in progress. It supports continuous protection, response, provenance, and root-cause improvement without prescribing an update bot.
- [CISA Known Exploited Vulnerabilities Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog) is evidence of exploitation for listed vulnerabilities, not a complete dependency inventory, reachability result, or universal priority formula.

## Decision Implications

- Automation detects and proposes; accountable maintainers decide and verify. A bot identity and passing generic CI do not establish trust or product compatibility.
- Cooldowns can reduce exposure to a newly published malicious or defective release but delay fixes. Use different policy for urgent security response and ordinary freshness.
- Review the resolved graph, not only the direct version line. Transitive packages, install scripts, binaries, registries, licenses, and build output may change unexpectedly.
- Separate initial adoption review from routine updates, but re-run the full gate on maintainer transfer, new binary or script, license or telemetry change, provenance gap, broad permission, abandonment, or other material trust change.
- Closure requires deployment evidence and cleanup. Merging an update pull request does not prove that production artifacts use the new dependency or that obsolete credentials and adapters are gone.
