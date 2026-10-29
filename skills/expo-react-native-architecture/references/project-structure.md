# Project structure and module boundaries

Use this reference when deciding where screens, feature code, shared UI, and infrastructure belong. Treat the layout below as a starting point; adapt it to the existing repository and create only directories with real contents.

## Example layout

```text
my-app/
├── app/                              # Expo Router routes and layouts
│   ├── _layout.tsx
│   ├── index.tsx
│   ├── (auth)/
│   │   ├── _layout.tsx
│   │   ├── login.tsx
│   │   └── register.tsx
│   └── recipes/
│       ├── index.tsx
│       └── [id].tsx
├── src/
│   ├── features/
│   │   ├── auth/
│   │   │   ├── components/
│   │   │   ├── hooks/
│   │   │   ├── services/
│   │   │   └── types/
│   │   └── recipes/
│   │       ├── components/
│   │       ├── hooks/
│   │       ├── services/
│   │       ├── types/
│   │       └── utils/
│   ├── components/                    # Shared UI, forms, and layout
│   ├── lib/                           # API, storage, analytics, integrations
│   ├── hooks/                         # Cross-feature hooks
│   ├── store/                         # App-wide client state, if needed
│   ├── config/
│   ├── constants/
│   ├── theme/
│   ├── types/                         # Cross-feature types
│   └── utils/                         # Cross-feature utilities
├── assets/
├── app.json
├── eas.json
├── package.json
└── tsconfig.json
```

## Routes and features

Keep `app/` for route files, dynamic route parameters, layouts, navigation configuration, and small adapters that render feature screens. Put API implementation, complex form logic, domain rules, and substantial reusable components outside route files.

```tsx
// app/recipes/[id].tsx
import { RecipeDetailScreen } from "@/src/features/recipes/components/RecipeDetailScreen";

export default function RecipeDetailRoute() {
  return <RecipeDetailScreen />;
}
```

Make the import alias match the project's TypeScript and Metro configuration. Some projects use `@/features/...` when `src/` is configured as the alias root.

Group code owned by one business capability under `src/features/<feature>/`. Useful folders can include:

- `components/`: UI mainly used by the feature.
- `hooks/`: feature-specific React hooks and orchestration.
- `services/`: feature use cases or API-facing operations.
- `types/`: feature-owned domain and application types.
- `utils/`: pure helpers specific to the feature.
- `stores/`: feature-owned client state, only when needed.
- `data/`: DTOs, mappers, and persistence adapters when the feature needs a distinct data layer.
- `domain/`: business rules and models when complexity justifies the layer.
- `screens/`: substantial screen compositions when separating them from route files improves clarity.

Do not force every feature to have every folder. Keep feature-specific components in the feature; for example, `RecipeCard` belongs in `features/recipes/components/`, not in generic UI.

## Shared code and infrastructure

- Put generic building blocks in `src/components/` (for example, `ui/`, `forms/`, and `layout/`).
- Put hooks, types, constants, and pure utilities used across features in their corresponding shared folders.
- Use `src/lib/` or `src/core/` consistently for API client configuration, storage adapters, third-party SDK setup, analytics, logging, and app-wide providers. Do not create both unless responsibilities are clearly distinct.
- Feature services should reuse configured infrastructure instead of creating a separate API client for each feature.
- A feature should not reach into another feature's private implementation. Expose a deliberate public module or promote genuinely generic code when cross-feature reuse becomes real.
- Avoid circular dependencies and catch-all files such as `helpers.ts`, `common.ts`, or `api.ts` that collect unrelated responsibilities.
- Prefer named exports for reusable components and utilities unless the project has a different convention. Expo Router route modules should export the required default route component.

## Official documentation

- [Expo documentation](https://docs.expo.dev/)
- [React Native documentation: Getting started](https://reactnative.dev/docs/getting-started)
- [TypeScript with Expo](https://docs.expo.dev/guides/typescript/)
