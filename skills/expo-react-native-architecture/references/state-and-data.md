# State and data boundaries

Use this reference when choosing state ownership, designing API boundaries, or adding persistence.

## Choose state by lifetime and owner

- **Server state:** Consider TanStack Query or the project's existing server-state library for fetching, caching, mutations, retries, and invalidation.
- **Local UI state:** Use React state or reducer hooks for state owned by one component or screen.
- **Forms:** Keep form state in the form layer. Add a form library when complexity warrants it or the project already uses one.
- **Shared client state:** Use the existing project convention, or a tool such as Zustand or Redux Toolkit, when state truly needs to be shared across distant components or routes.
- **Authentication:** Keep one clear source of truth for the current session and coordinate it with route protection. Avoid duplicating session state across stores and route-local state.
- **Persisted state:** Choose storage based on sensitivity. Use secure storage for credentials and secrets; use suitable ordinary storage for non-sensitive preferences.

Do not mirror all server data into a global client store when the server-state library can own it. Avoid adding a state-management dependency when the project already has a suitable convention.

## API boundaries

- Use one configured HTTP client per intended backend or configuration, not one per screen.
- Keep request/response DTOs distinct from domain models when their shapes or lifecycles differ.
- Type API boundaries, and validate untrusted runtime data when correctness or security requires it; TypeScript types do not validate network responses.
- Normalize transport errors at a shared boundary, then map them to useful feature-level outcomes.
- Keep feature operations in their feature and reuse shared client configuration and infrastructure.

## Configuration and secrets

- Keep secrets out of source control and client bundles. Anything shipped in a mobile app should be treated as potentially inspectable.
- Keep environment configuration explicit and compatible with Expo's public/private environment variable behavior.
- Centralize storage adapters and third-party SDK configuration so security and initialization rules are consistent.
