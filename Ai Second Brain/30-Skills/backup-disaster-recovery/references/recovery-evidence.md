# Recovery Evidence

Verified 2026-10-21.

- [NIST SP 800-34 Rev. 1](https://csrc.nist.gov/pubs/sp/800/34/r1/upd1/final) provides contingency-planning guidance and business-impact analysis for United States federal information systems. It was published in 2010, so use its durable planning structure while verifying technical controls against current platform and security guidance.
- The [NIST contingency-planning topic](https://csrc.nist.gov/topics/security-and-privacy/security-programs-and-operations/contingency-planning) frames recovery as coordinated plans, procedures, and technical measures, including alternate equipment, processing, and locations.
- The [CISA StopRansomware Guide](https://www.cisa.gov/stopransomware/ransomware-guide) recommends offline, encrypted backups of critical data and regular availability and integrity testing in a disaster-recovery scenario.
- Product-specific restore behavior must come from the exact database, object store, identity system, infrastructure platform, and managed-provider documentation selected by the project.

## Test Evidence

A recovery exercise should record the scenario, scope, source backup and timestamp, isolated destination, operators, start and completion times, errors, missing dependencies, achieved recovery point and time, data and invariant checks, critical-journey results, security and privacy checks, cleanup, and corrective actions.

Do not copy real sensitive data into an unsafe recovery environment merely to make a test realistic. Use protected replicas, masked data, or synthetic fixtures according to the risk model.
