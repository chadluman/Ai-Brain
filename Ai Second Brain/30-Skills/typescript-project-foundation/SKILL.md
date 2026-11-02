---
name: typescript-project-foundation
description: Decide whether and how to introduce or strengthen TypeScript in a JavaScript project. Use for new project configuration, JavaScript migration, package boundaries, or type-safety review; do not treat static types as runtime validation or require TypeScript when its maintenance cost does not fit the project.
---

# TypeScript Project Foundation

## Outcome

Create a small, explicit TypeScript policy that improves change safety without hiding runtime uncertainty or coupling the project to unnecessary tooling.

Read [TypeScript evidence](references/typescript-evidence.md) before fixing compiler settings or migration policy.

## Inputs

Establish whether this is an application or library, the runtime and build tool, module format, supported environments, framework constraints, generated-code boundaries, package layout, JavaScript migration needs, team familiarity, and the sources of untrusted runtime data.

## Workflow

1. Decide whether TypeScript materially improves the project's maintenance, refactoring, editor, and contract needs. Record why plain JavaScript plus tests and JSDoc is or is not sufficient.
2. Verify the exact compiler version against the runtime, framework, build tool, test runner, and declaration dependencies before adoption or upgrade.
3. For a new codebase, enable `strict` unless a documented incompatibility prevents it. Treat exceptions as narrow, owned technical debt.
4. Make module and resolution settings match the actual host or bundler. Do not copy a generic `tsconfig` without understanding emitted code and resolution behavior.
5. Keep application types close to domain boundaries. Model absence explicitly, prefer narrowing from `unknown`, and audit `any`, assertions, ignored errors, ambient declarations, and generated types.
6. Validate all untrusted runtime input—HTTP payloads, environment variables, storage, messages, files, and third-party SDK results—before converting it to trusted domain types.
7. Run type checking independently in CI when the build tool only transpiles. When `tsc` emits production code, prevent stale output after type errors.
8. Add project references, shared configuration packages, or code generation only after scale justifies their complexity and each dependency passes review.

## Safety and Change Control

- TypeScript types are erased and do not validate runtime data, authorize a value, sanitize output, or enforce server-side access control.
- Installing the compiler, type packages, validators, plugins, or shared configurations is R2 and requires exact-version dependency and lifecycle review.
- Do not silence errors globally to finish a migration. Track narrow exceptions with an owner and removal condition.
- Compiler upgrades can add stricter checks; review release notes and run the full verification suite before adoption.

## Completion

Deliver the adoption decision, exact-version compatibility evidence, configuration rationale, runtime-validation boundaries, exception inventory, type-check command, CI gate, migration slices when applicable, and upgrade and rollback triggers.
