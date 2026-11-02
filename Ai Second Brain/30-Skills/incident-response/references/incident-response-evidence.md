# Incident Response Evidence

Verified: 2026-10-21

## Primary Guidance

- [NIST SP 800-61 Rev. 3](https://csrc.nist.gov/pubs/sp/800/61/r3/final), final April 2025, integrates incident response into Cybersecurity Framework 2.0 risk management across preparation, detection, response, and recovery. It supersedes Rev. 2.
- [CISA Federal Government Cybersecurity Incident and Vulnerability Response Playbooks](https://www.cisa.gov/news-events/news/federal-government-cybersecurity-incident-and-vulnerability-response-playbooks) provides a standardized public-sector operational reference. Adapt roles, authorities, and reporting requirements to the organization rather than copying them blindly.
- [Google SRE: Managing Incidents](https://sre.google/sre-book/managing-incidents/) describes incident command, operations, communications, planning, a recognized command post, a live state document, explicit handoffs, and practice.
- [Google SRE incident-management guide](https://sre.google/resources/practices-and-processes/incident-management-guide/) emphasizes coordination, communication, control, blameless postmortems, and tracked corrective actions.

## Interpretation Boundaries

- Cybersecurity, privacy, safety, fraud, and reliability incidents overlap but can have different evidence, notification, containment, and authority requirements.
- A generic playbook cannot determine legal notification duties or forensic procedure. Use current jurisdiction-specific qualified advice.
- Restoring availability can destroy evidence or reintroduce compromise. The authorized incident lead must balance these risks explicitly.
- Postmortem action counts are not proof of learning. Prioritize systemic actions, assign owners and dates, and verify completion and effectiveness.
