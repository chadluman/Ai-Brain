# Release Quality Evidence

Verified: 2026-10-22

## Evaluation Framework

- [ISO/IEC 25040:2024](https://www.iso.org/standard/83467.html) is the current SQuaRE quality-evaluation framework for ICT products, data, and IT services. It supports systematic evaluation against documented criteria, including acceptance or release decisions, but does not prescribe project-specific test methods or thresholds.
- [ISO/IEC 25010:2023](https://www.iso.org/standard/78176.html) supplies a product-quality model for selecting relevant evaluation characteristics. [ISO/IEC 25019:2023](https://www.iso.org/standard/78177.html) supplies the quality-in-use lens for specified contexts. Neither model makes every characteristic equally important for every release.
- [ISO/IEC 25030:2019](https://www.iso.org/standard/72116.html) connects quality needs to governed, traceable, testable requirements. A release decision is weak when criteria are vague, untraceable, or created only after observing the candidate's results.

## Testing and Review Evidence

- [ISO/IEC/IEEE 29119-1:2022](https://www.iso.org/obp/ui?_escaped_fragment_=iso:std:iso-iec-ieee:29119:-1:ed-2:v1:en) describes risk-based software testing, test bases and oracles, levels and types, independence, exploratory and scripted work, manual and automated testing, reporting, and defect or incident management. It also makes clear that exhaustive testing is impractical.
- [ISO/IEC/IEEE 29119-2:2021](https://www.iso.org/standard/79428.html) specifies organizational, management, and dynamic test processes across lifecycle models.
- [ISO/IEC/IEEE 29119-3:2021](https://www.iso.org/standard/79429.html) defines test-documentation outputs. Tailor the information to the decision; do not create every template merely to appear complete.
- [ISO/IEC/IEEE 29119-4:2021](https://www.iso.org/standard/79430.html) defines test-design techniques. Technique choice and thoroughness must follow the risk, test basis, and quality characteristic.
- [ISO/IEC 20246:2017](https://www.iso.org/standard/67407.html), confirmed in 2022, provides a lifecycle framework for static review of work products. Reviews complement executable tests and can detect defects in requirements, design, code, tests, operations material, and other evidence.
- [ISTQB CTFL v4.0.1](https://istqb.org/certifications/certified-tester-foundation-level-ctfl-v4-0/) is a current, freely available testing syllabus covering lifecycle alignment, risk, monitoring and control, completion, configuration, defect management, test tools, and reporting. It is a training baseline, not a product certification or mandatory project process.

## Decision Interpretation

- A test result is evidence only for the identified candidate, conditions, oracle, data, and assertions. A passing suite is not a general quality guarantee.
- Coverage, pass rate, defect count, automation percentage, and aggregate scores can hide missing requirements or critical failures. Keep release-blocking risks visible rather than averaging them away.
- Retried or quarantined failures remain evidence about instability unless their cause and disposition are demonstrated. A green rerun does not erase the first failure.
- Severity describes impact; priority describes scheduling. Do not lower severity merely because a fix is inconvenient or the release date is near.
- Independence can improve defect detection, especially when consequence or conflicts are high, but familiarity and collaboration also matter. Record who produced and who evaluated critical evidence.
- `Conditional` is not a euphemism for missing critical evidence. It requires bounded exposure, owned exceptions, expiry, monitoring, containment, and a credible exit path.
