# COITB Python Curriculum

Use this as an adaptable exam-preparation sequence, not a fixed calendar. These are preparation topics, not claimed official COITB domains; order instruction by dependency and allocate practice by measured weakness. Build one original Python application throughout so knowledge checks remain connected to working behavior.

## Learner Assumptions

- The learner can create and edit files and run Python; teach these first if the diagnostic shows a gap.
- All practice data is synthetic or learner-owned. No production data, real user data, or real credentials are used.
- Practice content is original, licensed, or explicitly permitted.
- Exam preparation and certification are separate outcomes. Completing this curriculum does not guarantee a passing score.

## Final Observable Outcome

The learner can answer original questions across all curriculum areas and build a small Python application containing correct values and control flow, functions and data structures, classes where they genuinely help, file handling, API consumption with error paths, and a small test suite.

## Project Spine

Use a single small application such as a task tracker, catalog browser, or data-cleaning tool:

- `app.py`: entry point and command-line interface, kept thin;
- `models.py` or `services.py`: core logic in small, testable functions;
- `data/`: synthetic input files only;
- `tests/`: a small test suite covering the core logic.

No web framework, database server, account, or package beyond the standard library is required for the core capstone.

## Module 0 — Diagnostic and Exam Orientation

- **Outcome:** Produce area-level evidence and a prioritized study plan.
- **Demo:** Work through one original item by identifying the exact topic, eliminating distractors, and confirming the behavior in a minimal script.
- **Guided lab:** Inspect a deliberately uneven sample program for a value, logic, data-structure, file-handling, and error-handling issue.
- **Independent task:** Complete a short original mixed diagnostic without notes.
- **Verification:** Record correct and incorrect results by area and error type; do not reduce the result to a single score.

## Module 1 — Language Fundamentals

- **Concepts:** values and types, variables, operators, conditionals, loops, string handling, and formatting.
- **Demo:** Predict the result of a short expression before running it, including one mutability trap.
- **Guided lab:** Build the application's core logic as pure functions over plain data.
- **Independent task:** Rewrite a fragile conditional chain as a clear, tested function.
- **Original exam practice:** predict values, identify invalid syntax, and choose the smallest correct fix.
- **Verification:** the learner predicts results before running code and can explain why a value changed.

## Module 2 — Functions, Data Structures, and Classes

- **Concepts:** functions and parameters, scope, lists, tuples, dictionaries, sets, comprehensions, and classes where they genuinely help.
- **Demo:** Trace scope and object identity in a small example.
- **Guided lab:** Implement the application's data handling with the right structure per concern.
- **Independent task:** Replace a duplicated data-handling pattern with a single function or class.
- **Original exam practice:** predict data-structure results, identify mutation side effects, and choose the correct structure.
- **Verification:** functions are small, named, and testable; no shared data is mutated by accident.

## Module 3 — Files, Modules, and APIs

- **Concepts:** file reading and writing, CSV and JSON handling, modules and packages, virtual environments in plain language, and HTTP requests with error paths.
- **Demo:** Trace a file or API operation through success and failure states.
- **Guided lab:** Load the application's data from files, and add one read-only API call with a local fallback.
- **Independent task:** Add a new data source without duplicating parsing code.
- **Original exam practice:** predict file and API outcomes, identify unhandled errors, and choose the correct error path.
- **Verification:** the application never crashes on a missing file or failed request, and never overwrites input data by accident.

## Module 4 — Errors, Testing, and Capstone

- **Concepts:** exceptions and handling, reading tracebacks, isolating a defect, writing small tests, and reviewing code for readability.
- **Demo:** Diagnose an injected defect by narrowing the suspect code before changing it.
- **Guided lab:** Write a small test suite and run it against the finished application.
- **Independent task:** Fix three injected defects, one each in logic, data handling, and error handling, and record what proved each fix.
- **Original exam practice:** mixed timed sets across all areas, with rationales after attempts.
- **Verification:** the capstone meets the final observable outcome and the learner can explain every major decision in it.
