# Vue, Angular, Svelte and other web frameworks

- Use the framework and version declared by the feature's package rather than imposing React patterns.
- **Vue:** Detect Vue 2 vs 3 and Options vs Composition API; preserve established `<script setup>`/composables, props/emits contracts, reactive refs/computed/watch choices, Pinia/Vuex if present, and route conventions. Use stable `:key` and clean up watchers/resources.
- **Angular:** Respect standalone vs NgModule style, Signals/RxJS and state conventions, dependency injection, change detection strategy, router and reactive forms. Use async pipe or lifecycle-safe subscription cleanup; track items by stable IDs and maintain template accessibility.
- **Svelte/SvelteKit:** Respect the version and rune/store patterns in use, load functions, server vs client code boundaries, form actions, route structure, and reactive dependencies. Keep secrets on the server and clean up subscriptions.
- **Other:** Identify docs and local examples before changing core patterns; prefer native semantics, project tokens, minimal dependencies and targeted regression tests.
- For all, derive format/lint/typecheck/test/build commands from actual package scripts and CI, never from assumptions.
