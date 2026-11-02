# Backend Runtime and Framework Evidence

Verified: 2026-10-21

## Runtime Lifecycle Sources

- [Node.js releases](https://nodejs.org/en/about/previous-releases) documents current release phases, LTS status, end-of-life lines, and a changing release-cycle policy. The page says production applications should use supported LTS lines.
- [Python version status](https://devguide.python.org/versions/) records supported CPython branches, status, schedules, and end-of-life dates.
- [.NET support policy](https://dotnet.microsoft.com/en-us/platform/support/policy/dotnet-core) distinguishes LTS and STS support, patch requirements, supported releases, and OS-policy dependencies.
- [Go release history and policy](https://go.dev/doc/devel/release) states that a major Go release is supported until two newer major releases exist and records security and bug-fix releases.
- [Rust platform support](https://doc.rust-lang.org/rustc/platform-support.html) defines target support tiers and their build, test, host-tool, and guarantee differences. It does not provide a long-term support branch.
- [Oracle Java SE support roadmap](https://www.oracle.com/java/technologies/java-se-support-roadmap.html) documents Oracle JDK support and licensing timelines. Other OpenJDK distributions have separate support and license terms and must be evaluated independently.

## Interpretation Boundaries

- A supported language runtime does not imply support for a framework, database driver, native dependency, operating system, container base, serverless host, or CPU architecture.
- Long-term support describes maintenance timing, not application fitness, security assurance, or zero-cost support.
- Framework documentation and benchmarks are maintainer evidence. Reproduce the workload with exact versions, deployment settings, and representative data.
- Developer throughput includes type checking, builds, test speed, debugging, profiling, deployment, incident work, upgrades, and hiring, not only lines of code.
- Memory-safe languages can eliminate classes of defects but do not prevent authorization, injection, logic, dependency, or operational failures.
- Serverless or edge runtime labels can hide limits on sockets, binaries, filesystem, duration, concurrency, background work, regions, and observability. Verify the selected host contract.

## Candidate Review Record

For every candidate, record:

- runtime, distribution, framework, server, package manager, and exact versions
- official support and security-policy URLs plus end dates
- license and production-support terms
- supported OS, architecture, hosting, driver, SDK, and observability matrix
- dependency count, native components, install hooks, downloads, telemetry, and network destinations
- measured workload results and the scripts or fixtures used to reproduce them
- patch, upgrade, rollback, and exit plan

## Re-Review Triggers

- runtime or framework support, license, security policy, or release-cycle change
- target OS, architecture, hosting, protocol, driver, or SDK change
- new workload shape, performance objective, compliance scope, or operational constraint
- upgrade failure, repeated incident friction, dependency compromise, or maintainer decline
