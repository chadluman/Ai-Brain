# COITB MySQL Curriculum

Use this as an adaptable exam-preparation sequence, not a fixed calendar. These are preparation topics, not claimed official COITB domains; order instruction by dependency and allocate practice by measured weakness. Build one original database throughout so knowledge checks remain connected to working behavior.

## Learner Assumptions

- The learner can create and edit files and run a local MySQL database; teach these first if the diagnostic shows a gap.
- All practice data is synthetic. No production data, real user data, or real credentials are used.
- Practice content is original, licensed, or explicitly permitted.
- Exam preparation and certification are separate outcomes. Completing this curriculum does not guarantee a passing score.

## Final Observable Outcome

The learner can answer original questions across all curriculum areas and build a small application database containing a normalized schema with keys and constraints, correct SELECT queries with joins and aggregation, safe INSERT/UPDATE/DELETE operations, a view or stored routine where it genuinely helps, and a documented backup and restore check.

## Project Spine

Use a single small application database such as an event planner, task tracker, or catalog:

- `schema.sql`: tables, keys, constraints, and indexes, in dependency order;
- `seed.sql`: synthetic rows only, enough to make joins and aggregation meaningful;
- `queries.sql`: the application's real queries, each commented with what it returns and why;
- `checks.md`: a short list of integrity checks and their expected results.

No hosted database, account, or production connection is required.

## Module 0 — Diagnostic and Exam Orientation

- **Outcome:** Produce area-level evidence and a prioritized study plan.
- **Demo:** Work through one original item by identifying the exact topic, eliminating distractors, and confirming the result in a minimal database.
- **Guided lab:** Inspect a deliberately uneven sample schema for a key, relationship, query, constraint, and transaction issue.
- **Independent task:** Complete a short original mixed diagnostic without notes.
- **Verification:** Record correct and incorrect results by area and error type; do not reduce the result to a single score.

## Module 1 — Relational Design and Schema

- **Concepts:** tables and rows, primary and foreign keys, one-to-many and many-to-many relationships, normalization to third normal form, and when to denormalize deliberately.
- **Demo:** Convert an unstructured list into tables with keys before writing any query.
- **Guided lab:** Design the application's schema with keys and constraints.
- **Independent task:** Add a new entity and its relationship without breaking existing queries.
- **Original exam practice:** identify key errors, predict constraint violations, and choose the smallest correct schema fix.
- **Verification:** every table has a key; every relationship is enforced, not merely documented.

## Module 2 — Querying with SELECT

- **Concepts:** SELECT, WHERE, ORDER BY, LIMIT, joins, subqueries, aggregation, GROUP BY and HAVING, and NULL handling.
- **Demo:** Predict a join result before running it, including one NULL trap.
- **Guided lab:** Write the application's core read queries, one per real view.
- **Independent task:** Rewrite a fragile query as a clear join or aggregation with a documented result.
- **Original exam practice:** predict result sets, identify join errors, and choose the smallest correct query.
- **Verification:** every query returns the documented result on the seeded data, including edge cases.

## Module 3 — Writing Data Safely

- **Concepts:** INSERT, UPDATE, DELETE, transactions, isolation in plain language, constraints and defaults, and parameterized queries.
- **Demo:** Trace a transaction through commit and rollback before running it.
- **Guided lab:** Implement the application's write operations with transactions where a partial write would corrupt data.
- **Independent task:** Replace a string-built query with a parameterized one and explain the injection it prevented.
- **Original exam practice:** predict transaction outcomes, identify unsafe writes, and choose the correct constraint.
- **Verification:** no write leaves the database half-updated; no query builds SQL from untrusted input.

## Module 4 — Optimization, Views, and Capstone

- **Concepts:** indexes and when they help, EXPLAIN in plain language, views, stored routines where they genuinely help, and backup and restore checks.
- **Demo:** Diagnose a slow query by reading its plan before adding an index.
- **Guided lab:** Add one justified index, one view, and a backup/restore check to the project.
- **Independent task:** Fix three injected defects, one each in schema, query, and transaction code, and record what proved each fix.
- **Original exam practice:** mixed timed sets across all areas, with rationales after attempts.
- **Verification:** the capstone meets the final observable outcome and the learner can explain every major decision in it.
