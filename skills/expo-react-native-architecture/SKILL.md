---
name: expo-react-native-architecture
description: Design, review, and refactor scalable React Native applications built with Expo and Expo Router using feature-first architecture, thin route files, clear infrastructure boundaries, and pragmatic state management. Use when creating a new Expo project structure, adding a feature, deciding where code belongs, or reviewing architecture.
---

# Expo React Native Architecture Skill

Help agents create and maintain understandable React Native applications using Expo, TypeScript, and Expo Router. Prefer feature-first organization, thin route files, explicit infrastructure boundaries, and architecture proportional to the problem.

## Core principles

1. Keep `app/` focused on routing and screen entry; put substantial feature behavior in `src/`.
2. Group feature-owned code together and promote code to shared locations only when it is genuinely reusable or cross-cutting.
3. Give remote data, local UI state, shared client state, and persisted values clear owners.
4. Centralize app-wide infrastructure and native setup; avoid speculative layers and duplicate sources of truth.
5. Follow the repository's Expo SDK, Router, TypeScript, and platform conventions.

## Choose a reference

Read the guidance that matches the work. Read more than one when a change crosses boundaries.

- For folder layout, feature boundaries, shared UI, and infrastructure placement, read [references/project-structure.md](references/project-structure.md).
- For server state, client state, persistence, API boundaries, and secrets, read [references/state-and-data.md](references/state-and-data.md).
- For routes, layouts, deep links, native dependencies, and platform-specific code, read [references/expo-router-and-native.md](references/expo-router-and-native.md).

## Architecture workflow

When asked to create, extend, refactor, or review a project:

1. Inspect `package.json`, Expo and TypeScript configuration, route files, existing feature folders, and the current state/API libraries. Note the installed Expo SDK and Router versions before recommending APIs or native dependencies.
2. Reuse established conventions and dependencies. Do not rewrite a working architecture to match a template.
3. Classify the change as routing, feature code, shared UI, infrastructure, or app-wide configuration. Load the relevant references above.
4. Choose the smallest structure that fits and preserve routes, deep links, authentication behavior, and platform behavior during refactors.
5. Verify with repository checks relevant to the change. For native dependencies or app-config changes, include the relevant Expo prebuild or platform check when available. Report checks that could not be run; do not claim an unrun check passed.
6. Briefly explain important file placement and non-obvious architecture decisions.

## Review checklist

- Route files primarily handle routing and screen entry.
- Feature-specific code is grouped by capability; shared code is genuinely reusable.
- API clients and third-party SDK setup are centralized.
- Server state and client state have clear ownership.
- Imports follow clear boundaries and avoid circular dependencies.
- Route parameters and platform differences are handled intentionally.
- Secrets are not committed or exposed in client code.
- Relevant checks were run or their status was reported accurately.

## Expected output

For implementation work, provide a brief summary, important files added or changed, reasoning for non-obvious decisions, verification results, and known gaps.
