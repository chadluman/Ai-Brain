# COITB JavaScript Curriculum

Use this as an adaptable exam-preparation sequence, not a fixed calendar. These are preparation topics, not claimed official COITB domains; order instruction by dependency and allocate practice by measured weakness. Build one original interactive application throughout so knowledge checks remain connected to working behavior.

## Learner Assumptions

- The learner has the HTML/CSS competence from the COITB HTML-CSS Web Designer preparation, or equivalent page-building experience.
- The learner can create and edit files and open a page in a browser; teach these first if the diagnostic shows a gap.
- Practice content and assets are original, licensed, or explicitly permitted.
- Exam preparation and certification are separate outcomes. Completing this curriculum does not guarantee a passing score.

## Final Observable Outcome

The learner can answer original questions across all curriculum areas and build an interactive application containing correct values and control flow, functions and scope discipline, arrays and objects, DOM manipulation and events, forms and validation, asynchronous data handling with error paths, and a small set of tests or manual verification steps.

## Project Spine

Use a single interactive application such as a task tracker, event planner, or small catalog browser:

- `index.html`: meaningful structure and a native form;
- `styles.css`: shared base and responsive rules, kept separate from behavior;
- `app.js`: application state, rendering, events, and data handling in clearly separated functions;
- `data.json` or a small public API used read-only, with a local fallback.

No framework, bundler, package installation, or account is required.

## Module 0 — Diagnostic and Exam Orientation

- **Outcome:** Produce area-level evidence and a prioritized study plan.
- **Demo:** Work through one original item by identifying the exact topic, eliminating distractors, and confirming the behavior in a minimal script.
- **Guided lab:** Inspect a deliberately uneven sample application for a value, scope, DOM, asynchronous, and error-handling issue.
- **Independent task:** Complete a short original mixed diagnostic without notes.
- **Verification:** Record correct and incorrect results by area and error type; do not reduce the result to a single score.

## Module 1 — Language Fundamentals

- **Concepts:** values and types, variables and constants, operators, truthiness, coercion, conditionals, loops, and template literals.
- **Demo:** Predict the result of a short expression before running it, including one coercion trap.
- **Guided lab:** Build the application's core state and a pure function that transforms it.
- **Independent task:** Rewrite a fragile conditional chain as a clear, tested function.
- **Original exam practice:** predict values, identify invalid syntax, and choose the smallest correct fix.
- **Verification:** the learner predicts results before running code and can explain why a value changed.

## Module 2 — Functions, Scope, and Collections

- **Concepts:** function declarations and expressions, parameters and defaults, scope and closures, arrays and array methods, objects, destructuring, and iteration.
- **Demo:** Trace scope and closure behavior in a small counter or filter example.
- **Guided lab:** Implement list rendering from an array of objects with filter and sort controls.
- **Independent task:** Add a new collection operation without mutating shared state unexpectedly.
- **Original exam practice:** trace scope, predict array-method results, and identify mutation side effects.
- **Verification:** functions are small, named, and testable; no shared state is mutated by accident.

## Module 3 — DOM, Events, and Forms

- **Concepts:** selecting and updating elements, creating nodes, event listeners and delegation, event flow, form values, validation attributes and messages, and keyboard usability.
- **Demo:** Convert a static list into an interactive one with delegated events.
- **Guided lab:** Wire the application's form to add, edit, and remove items with validation feedback.
- **Independent task:** Add a keyboard-accessible interaction that does not depend on mouse-only behavior.
- **Original exam practice:** predict DOM results, identify event-flow errors, and choose accessible markup for an interaction.
- **Verification:** every interaction works by keyboard; form errors are announced and recoverable.

## Module 4 — Asynchronous JavaScript and Data

- **Concepts:** callbacks, promises, `async`/`await`, `fetch`, JSON, loading and error states, and timeouts.
- **Demo:** Trace a fetch sequence through loading, success, and failure states.
- **Guided lab:** Load application data asynchronously with a loading indicator and a clear error message.
- **Independent task:** Add retry-free graceful degradation when data fails to load.
- **Original exam practice:** predict promise order, identify unhandled rejections, and choose the correct error path.
- **Verification:** the application never leaves the learner in a silent loading state and never crashes on a failed request.

## Module 5 — Debugging, Testing, and Capstone

- **Concepts:** reading error messages, breakpoints and console inspection, isolating a defect, writing a small manual test plan, and reviewing code for readability.
- **Demo:** Diagnose an injected defect by narrowing the suspect code before changing it.
- **Guided lab:** Write a short verification checklist and run it against the finished application.
- **Independent task:** Fix three injected defects, one each in logic, DOM handling, and asynchronous code, and record what proved each fix.
- **Original exam practice:** mixed timed sets across all areas, with rationales after attempts.
- **Verification:** the capstone meets the final observable outcome and the learner can explain every major decision in it.
