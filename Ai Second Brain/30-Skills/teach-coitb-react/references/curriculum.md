# COITB React Curriculum

Use this as an adaptable exam-preparation sequence, not a fixed calendar. Organize instruction around COITB's badge-page statements, not claimed official domains; order instruction by dependency and allocate practice by measured weakness. Build one original React application throughout so knowledge checks remain connected to working behavior.

## Learner Assumptions

- The learner has the HTML/CSS competence from the COITB HTML-CSS Web Designer preparation and the JavaScript competence from the COITB JavaScript Professional Developer preparation, or equivalents.
- The learner can create and edit files and run a development server; teach these first if the diagnostic shows a gap.
- Practice content and assets are original, licensed, or explicitly permitted.
- Exam preparation and certification are separate outcomes. Completing this curriculum does not guarantee a passing score.

## Final Observable Outcome

The learner can answer original questions across all curriculum areas and build a multi-section interactive React application containing reusable components, props and state discipline, controlled forms, conditional rendering, routing, API integration with loading and error states, and effect cleanup.

## Project Spine

Use a single multi-section application such as a task tracker, event planner, or small catalog browser, built with React:

- `src/components/`: reusable presentational components with clear props;
- `src/App.jsx`: composition, routing, and top-level state placement;
- `src/data/` or a small public API used read-only, with a local fallback;
- `src/styles.css`: shared base and responsive rules, kept separate from behavior.

A starter template or a single build tool is acceptable when the learner already understands what it does; it is not a curriculum topic in itself.

## Module 0 — Diagnostic and Exam Orientation

- **Outcome:** Produce area-level evidence and a prioritized study plan.
- **Demo:** Work through one original item by identifying the exact topic, eliminating distractors, and confirming the behavior in a minimal component.
- **Guided lab:** Inspect a deliberately uneven sample application for a component, state, effect, routing, and API-handling issue.
- **Independent task:** Complete a short original mixed diagnostic without notes.
- **Verification:** Record correct and incorrect results by area and error type; do not reduce the result to a single score.

## Module 1 — Components, JSX, and Props

- **Concepts:** function components, JSX expressions, props, children, composition, and reusable component boundaries.
- **Demo:** Convert a static page into components with clear props before adding state.
- **Guided lab:** Build the application's layout and a reusable card, list, and form-field component.
- **Independent task:** Extract a duplicated section into a reusable component without changing its behavior.
- **Original exam practice:** predict rendered output, identify prop errors, and choose the smallest correct component boundary.
- **Verification:** components are small, named for what they render, and reusable without hidden dependencies.

## Module 2 — State, Events, and Controlled Components

- **Concepts:** `useState`, state placement and lifting, immutable updates, event handlers, controlled inputs, and derived data.
- **Demo:** Trace a state update from event to re-render in a small form example.
- **Guided lab:** Wire the application's form and list interactions with lifted, immutable state.
- **Independent task:** Add a filter or sort control that derives its view from state instead of duplicating it.
- **Original exam practice:** predict state after a sequence of updates, identify stale-state errors, and choose the correct state placement.
- **Verification:** state lives in one place per concern; no view is stored twice in conflicting copies.

## Module 3 — Effects, Data, and Routing

- **Concepts:** `useEffect`, effect timing and cleanup, `fetch` in effects, loading and error states, conditional rendering, and routing.
- **Demo:** Trace an effect's fetch, loading, success, and cleanup sequence.
- **Guided lab:** Load application data in an effect with loading and error states, and add two routes.
- **Independent task:** Add a detail view reached by route that fetches and cleans up correctly.
- **Original exam practice:** predict effect order, identify missing cleanup, and choose the correct conditional-rendering branch.
- **Verification:** no effect leaks a subscription or sets state after unmount; every route renders a complete, keyboard-usable view.

## Module 4 — API Integration, Review, and Capstone

- **Concepts:** asynchronous data in components, error boundaries in spirit (graceful failure views), code organization for maintainability, and manual verification.
- **Demo:** Diagnose an injected defect by narrowing the suspect component before changing it.
- **Guided lab:** Write a short verification checklist and run it against the finished application.
- **Independent task:** Fix three injected defects, one each in state, effects, and routing, and record what proved each fix.
- **Original exam practice:** mixed timed sets across all areas, with rationales after attempts.
- **Verification:** the capstone meets the final observable outcome and the learner can explain every major decision in it.
