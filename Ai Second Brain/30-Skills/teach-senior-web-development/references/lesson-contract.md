# Senior Web Development Lesson Contract

Use this contract for tutoring, workshops, code walkthroughs, curricula, mentoring plans, and assessments. Scale its depth to the request rather than forcing every section into every response.

## Learner Contract

Capture only decision-changing context:

- desired capability or artifact;
- evidence of current skill, not a guessed label;
- available time and environment;
- existing codebase or chosen stack;
- constraints such as accessibility, device support, security, budget, or deadlines;
- whether the learner wants coaching, a guided build, review, or a direct answer.

If no codebase exists, choose the smallest project that makes the target concept observable. If a codebase exists, preserve its conventions unless changing them is the learning objective.

## Lesson Shape

1. **Outcome:** State one behavior the learner will be able to demonstrate.
2. **Mental model:** Explain the mechanism and its boundary in compact language.
3. **Focused demo:** Show the smallest runnable example that exposes the mechanism.
4. **Prediction:** Ask what will happen or where it will fail before running or revealing the result.
5. **Guided lab:** Supply constraints and checkpoints while leaving meaningful implementation work.
6. **Independent variation:** Change one requirement so the learner must transfer the concept.
7. **Verification:** Use tests, browser behavior, protocol output, query results, traces, or a review checklist.
8. **Review:** Discuss correctness, clarity, tradeoffs, failure handling, and production gaps.
9. **Reflection:** Ask the learner to explain the decision and name a condition that would change it.

For a quick explanation, compress this to outcome, mental model, one example, one check, and one next step.

## Progressive Help

Offer help in this order unless safety requires direct intervention:

1. restate the observable mismatch;
2. point to the relevant boundary or invariant;
3. suggest a diagnostic action;
4. reveal a partial pattern or pseudocode;
5. provide a complete solution with an explanation.

Never make the learner guess around an unsafe action, secret, destructive command, paid operation, or production mutation. Stop and apply the repository's permission boundary.

## Curriculum Shape

For a multi-session path:

- start with a thin vertical slice that can run locally with dummy data;
- separate fundamentals from optional extensions;
- introduce abstractions only after the concrete problem appears;
- revisit the same product across browser, server, data, testing, security, and operations where useful;
- use milestone reviews that require evidence, not self-reported confidence;
- make the capstone integrate learned concepts without hiding several new concepts inside it.

Each module should name its prerequisite, artifact, verification command or observation, common failure modes, and exit criteria.

## Assessment

Use four evidence levels:

| Level | Observable evidence |
|---|---|
| Needs guidance | Cannot yet explain the mechanism or complete the task without step-by-step direction |
| Functional | Produces the expected behavior in the demonstrated path |
| Reliable | Handles named edge cases, verifies behavior, and explains important tradeoffs |
| Senior judgment | Frames ambiguous requirements, compares alternatives, manages risk, communicates consequences, and leaves maintainable evidence |

Assess only dimensions relevant to the task: correctness, mental model, decomposition, readability, accessibility, security, testing, failure handling, performance, data integrity, operability, cost awareness, and decision communication. Separate automated evidence from qualitative judgment.

## Production-Readiness Label

End examples with one of these labels:

- **Concept demo:** proves one mechanism; deliberately omits production controls.
- **Practice implementation:** includes realistic structure and tests but has not passed production review.
- **Production candidate:** has explicit requirements and project-specific verification; still requires the applicable release authority.

Name the missing work instead of implying readiness.

## Evidence and Freshness

- Use the subject module to route to the relevant maintained skill and conditional evidence note.
- Recheck current primary sources for changing APIs, versions, browser support, security guidance, pricing, or service policy.
- Record the verification date in a curriculum or durable lesson when a changing fact affects the learner's decision.
- Label estimates and engineering judgment as such.
