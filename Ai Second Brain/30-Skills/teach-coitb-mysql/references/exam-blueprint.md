# COITB MySQL Backend Developer Exam Blueprint

Verified against official COITB pages on 2026-11-02. Recheck immediately before a study plan, mock exam, registration decision, or claim about current exam logistics.

## Credential and Exam Summary

- Official credential name: **MySQL Backend Developer Certification**.
- Published length, item count, and passing score, from COITB's own full-stack article: **90 minutes, 90 items, 70%**.
- Delivery described on COITB badge pages generally: online remote proctoring or an authorized test center; language listed as English.
- Position in the COITB pathway: the fourth credential in COITB's recommended full-stack sequence, after HTML-CSS Web Designer, JavaScript Professional Developer, and ReactJS Framework Developer.

## What Is NOT Verified Here

No COITB exam-outline page for this certification was located on 2026-11-02 through COITB's site search, so this blueprint does **not** claim official domain names, domain weights, or question counts by domain. The curriculum areas in the companion curriculum file are preparation topics drawn from relational database practice, not a reproduction of a COITB outline. Do not present them as official domains, and do not fill the gap with weights borrowed from another vendor's MySQL exam.

## Exam-to-Curriculum Interpretation

- Cover every curriculum area. Allocate practice by measured learner weakness, not by an invented weight.
- Teach query reading as well as query writing. A multiple-choice and scenario-based exam can test result sets, join behavior, constraint effects, and transaction outcomes without requiring a live database.
- Pair each area with a working project artifact. Correct answers without the ability to design a schema and write a correct, safe query are insufficient practical evidence.
- Teach security as a cross-cutting expectation: least-privilege accounts, parameterized queries, and no secrets in code or practice data, even though no separate security domain is claimed here.
- Treat administration topics such as replication and backup as awareness-level preparation, not as the core of this developer credential's curriculum, unless a located official outline says otherwise.

## Local Readiness Heuristic

This is a teaching heuristic, not a COITB policy or score prediction:

- complete at least three original mixed practice sets under time pressure;
- score at least 85% on each of the last two sets;
- score at least 75% within every curriculum area rather than relying on strength in one area to conceal a gap;
- explain the rationale for corrected answers without memorizing wording;
- complete the curriculum capstone acceptance criteria and diagnose at least one injected schema, query, join, constraint, and transaction defect.

If the exam date is near, prioritize high-weakness areas. If time permits, repair prerequisite gaps before increasing question volume.

## Standards Cross-Check

- [MySQL Reference Manual](https://dev.mysql.com/doc/refman/en/) is the official maintainer reference for MySQL syntax, data types, and behavior.
- [SQL standard behavior](https://www.iso.org/standard/63555.html) is a background reference only; MySQL's actual behavior governs practice, and the two differ in places.
- [OWASP SQL Injection Prevention](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html) is the practical baseline for safe query construction in the curriculum.

These sources are cataloged with their limits in the vault's [Source Registry](../../../20-Catalog/Sources/Source%20Registry.md).

## Re-Verification Triggers

Recheck when COITB changes the title, objectives, item count, duration, passing score, or delivery, when a dedicated exam-outline page appears, or when a learner reports a discrepancy between this blueprint and an official COITB page. Record the new verification date and what changed; do not silently carry the old numbers forward.
