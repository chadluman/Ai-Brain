# Penetration Test Evidence

Verified: 2026-10-22

## Primary Sources

- [NIST SP 800-115](https://csrc.nist.gov/pubs/sp/800/115/final) covers assessment planning, execution, analysis, data handling, reporting, remediation, and a rules-of-engagement template. It is a final 2008 publication and should be used for durable process concepts, not current tool or web-technology details.
- [OWASP Web Security Testing Guide project](https://owasp.org/projects/web-security-testing-guide) identifies v4.2 as the current stable release and v5.0 as development work. Cite stable test identifiers for acceptance evidence unless a project deliberately adopts and labels a development section.
- [OWASP WSTG v4.2](https://owasp.org/www-project-web-security-testing-guide/v42/) provides a dated web application and API testing taxonomy. It is a test guide, not legal authorization, a complete threat model, or permission to use every technique against every environment.

## Decision Implications

- Separate permission from method. Public guidance can describe a test but cannot authorize it.
- Write asset identity and exclusions precisely; discovery does not expand scope.
- Old process guidance can remain useful when paired with current application requirements, platform behavior, and provider rules.
- Stable version identifiers make findings reproducible. Development content can inform research but should not silently replace the agreed baseline.
- A test report is not closure. Remediation, regression, authorized retest, cleanup, and residual-risk acceptance complete the workflow.
