# Quality and validation matrix

## All frontend work

- Behavior: acceptance criteria, edge cases, null/empty/error, retries, race conditions, disabled/submitting states, idempotency where appropriate.
- UX: responsive constraints, scrolling, keyboard/insets, touch targets, visual hierarchy, reduced motion, light/dark mode when present.
- Accessibility: labels, semantics, focus visibility and order, keyboard/screen reader behavior, contrast; don't rely solely on color.
- Quality: types/null safety, predictable state ownership, composable code, resource cleanup, no unnecessary dependencies, no sensitive logging, tested error paths.
- Security: escape untrusted content appropriately, avoid unsafe HTML injection, respect auth boundaries, do not expose keys in client bundles.

## Choose commands from repository evidence

| Stack | Typical commands (confirm project conventions first) |
|---|---|
| Flutter/Dart | `dart format --output=none --set-exit-if-changed .`, `flutter analyze`, `flutter test` |
| npm | `npm run lint`, `npm run typecheck`, `npm test`, `npm run build` |
| pnpm | `pnpm lint`, `pnpm typecheck`, `pnpm test`, `pnpm build` |
| yarn | `yarn lint`, `yarn typecheck`, `yarn test`, `yarn build` |
| bun | `bun run lint`, `bun run typecheck`, `bun test`, `bun run build` |

Do not run a command merely because it appears above; verify the script exists, choose smallest relevant scope, and report unavailable checks accurately. Inspect baseline failure context before attributing failure to the patch.

## Final verification record template

- **Changed:** files/features and user-visible effects.
- **Validated:** commands executed and pass/fail outcomes.
- **Not validated:** unavailable commands or environmental blockers.
- **Risks:** any uncovered boundary or missing design/device check.
