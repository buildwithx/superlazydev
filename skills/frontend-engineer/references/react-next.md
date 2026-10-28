# React / Next.js / TypeScript rules

- Determine React/Next versions and whether the package uses Next App Router or Pages Router. Respect the app's routing, data-fetching, auth, styling and component conventions.
- In Next App Router, preserve Server Components by default; add `'use client'` only to the smallest interactive boundary. Do not import server-only secrets or APIs into client code. Follow existing rendering/cache/revalidation strategy rather than inventing one.
- Keep React renders pure; use effects for synchronization with external systems, not derived state. Use stable keys based on identity, correct hook dependencies, and cleanup/abort for async subscriptions. Avoid memoization without a measured reason.
- For TypeScript, preserve discriminated unions and strict types; avoid `any`, unsafe casts, and silent nullable assumptions. Validate external data at a trust boundary where the codebase provides validation tooling.
- Preserve current state solutions (Redux, Zustand, Context, TanStack Query, etc.) and form handling. Don't duplicate remote state in local stores without a clear reason.
- Use semantic HTML, accessible names, logical focus order, keyboard interactions, and valid ARIA only as necessary. Test responsive behavior, CSS overflow, dark mode if supported, and reduced-motion preferences.
- Check package scripts and use the repo's manager (`npm`, `pnpm`, `yarn`, `bun`) and scripts for lint, typecheck, test and build; distinguish Next compilation checks from independently configured TypeScript or ESLint checks.
