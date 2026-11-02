# Repository Topology Evidence

Verified: 2026-10-22

## Current Sources

- [GitHub repository limits](https://docs.github.com/en/enterprise-cloud@latest/repositories/creating-and-managing-repositories/repository-limits) documents current recommended and enforced limits for repository size, directory shape, branches, objects, pushes, and automated operations. These are host-specific operational constraints, not universal reasons to split or combine code.
- [Git partial clone](https://git-scm.com/docs/partial-clone) can omit unneeded objects and fetch them on demand for large repositories. The Git documentation records availability, online and promisor-remote dependencies, performance costs, and current limitations.
- [Git sparse checkout](https://git-scm.com/docs/sparse-checkout) reduces the working tree to selected paths. It does not remove those paths from history or automatically scope builds, tests, ownership, and changes.
- [GitHub CODEOWNERS](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners) can request and, with protection, require owner review. GitHub notes that the ownership file itself should be protected; one matching owner's approval can satisfy the rule unless stronger workflow is added.
- [GitHub protected branches](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches) and [repository rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets) describe current host enforcement and bypass behavior. Rules must be verified on every relevant branch and tag.
- [NIST SP 800-218](https://csrc.nist.gov/pubs/sp/800/218/final) is the current final SSDF baseline while NIST works on an update. Its source-protection and development-process practices support repository controls but do not prescribe monorepo or polyrepo topology.

## Decision Implications

- Monorepo and polyrepo are means, not maturity levels. Decide from atomic change, access separation, release independence, scale, ownership, and operating cost.
- A monorepo can simplify coordinated refactors while increasing blast radius and requiring reliable affected-build, ownership, and access controls. Multiple repositories can isolate access and lifecycle while shifting compatibility and coordination to packages and services.
- Sparse and partial checkout mitigate some client costs but introduce network and tool assumptions. Benchmark the actual host, Git version, CI and developer workflows.
- CODEOWNERS is routing plus optional enforcement, not proof of domain understanding or multiple-person approval. Protect the policy file and test bypass paths.
- Repository moves are preservation exercises. Tags, immutable releases, licenses, authorship, attestations, issues, review history, and consumer references may live outside Git commits.
