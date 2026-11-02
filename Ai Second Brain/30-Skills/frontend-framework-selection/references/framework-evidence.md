# Frontend Framework Evidence

Verified 2026-10-21. This is a source-routing note, not a permanent ranking. Recheck current stable versions, support, compatibility, and release status for every decision.

## Candidate Source Routes

- [React: Creating a React App](https://react.dev/learn/creating-a-react-app) recommends an application framework for a new React app while allowing a from-scratch path when constraints require it. That is React maintainer guidance, not evidence that React itself is required.
- [Angular versioning and releases](https://angular.dev/reference/releases) documents cadence, active and LTS support, deprecation, preview, and experimental status. [Angular version compatibility](https://angular.dev/reference/versions) maps supported Angular, Node.js, TypeScript, RxJS, and browser Baseline versions.
- [Vue Quick Start](https://vuejs.org/guide/quick-start.html) documents the official scaffold, optional TypeScript, and production build. Consult the current [Vue guide](https://vuejs.org/guide/introduction.html) and release notes for the capability under review.
- [SvelteKit introduction](https://svelte.dev/docs/kit/introduction) distinguishes the UI compiler from the application framework and documents integrated routing, rendering, data, and deployment capabilities.

Canonical repositories are [facebook/react](https://github.com/facebook/react), [angular/angular](https://github.com/angular/angular), [vuejs/core](https://github.com/vuejs/core), and [sveltejs/svelte](https://github.com/sveltejs/svelte). They are appropriate for provenance, release, governance, and issue research. Cloning, building, scaffolding, or executing any release remains R2 and requires exact-version review.

## Comparison Discipline

For each candidate capture the exact version and date, support window, browser and runtime matrix, license, core and transitive dependencies, security channel, release and migration policy, rendering modes, official adapters, and unresolved issues relevant to the project.

Compare one representative vertical slice, not unlike demos. Include HTML before JavaScript, client transfer and execution, critical interaction, accessibility tree and keyboard behavior, data and error flow, test setup, build output, deploy and rollback, and the maintainer workflow for an upgrade.
