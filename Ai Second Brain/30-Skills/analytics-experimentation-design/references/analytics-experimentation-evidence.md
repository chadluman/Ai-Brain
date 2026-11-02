# Analytics and Experimentation Evidence

Verified: 2026-10-21

## Public and Standards-Based Guidance

- [GOV.UK: Choosing digital analytics tools](https://www.gov.uk/service-manual/measuring-success/choosing-digital-analytics-tools) compares purpose, total cost, hosting, ownership, retention, export, access control, sampling, support, tracking method, security, and privacy. Its detailed legal wording is jurisdiction-specific and older; recheck current law and provider behavior.
- [GOV.UK: Designing with data](https://www.gov.uk/service-manual/design/designing-with-data-an-introduction) connects hypotheses to expected user outcomes and measures, emphasizes permissions, data quality, lifecycle security, and privacy impact.
- [W3C Privacy Principles](https://www.w3.org/TR/privacy-principles/) provides current web privacy principles for purpose, minimization, transparency, user control, and accountability.
- [NISTIR 8062](https://csrc.nist.gov/pubs/ir/8062/final) introduces privacy engineering and the objectives of predictability, manageability, and disassociability. It is risk guidance, not jurisdiction-specific legal advice.

## Decision Boundaries

- Page views and clicks are often proxies. Pair behavioral signals with system-of-record completion, support, qualitative research, accessibility, and long-term outcomes where relevant.
- Client events can be blocked, duplicated, delayed, spoofed, or lost. Server events can miss user intent and consent state. Reconcile rather than assuming either is complete.
- Statistical significance alone does not establish product value, causality outside the experiment, equitable impact, or acceptable harm.
- Identity stitching increases linkability and privacy risk. Do not create a cross-device or cross-service profile unless the decision truly requires it and the use is authorized.
- Session replay and free-text capture have unusually high disclosure risk and require a separate R3 review rather than default analytics setup.
