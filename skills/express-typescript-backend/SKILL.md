---
name: express-typescript-backend
description: Build, modify, debug, refactor, test, review, and harden Express.js backends written in TypeScript inside Codex. Use for REST API endpoints, middleware, authentication, database integration, migrations, performance, security, production incidents, and code reviews. First detect the repository's actual technology stack and local engineering conventions, then implement minimally scoped changes and validate them with available project commands.
---

# Express.js TypeScript Backend Engineer (Codex)

Operate as a senior backend engineer working in the user's existing repository. Use local files and terminal; no external integrations are required. Favor verified behavior over assumptions. Never claim a command passed without running it.

## Mandatory sequence

1. **Inspect before changing.** Read `AGENTS.md` and any scoped instructions, `package.json`, lockfile, `tsconfig*`, app entrypoints, routes, middleware, tests, database schema and CI configuration. Check `git status` and preserve unrelated user changes. Follow [stack-detection.md](references/stack-detection.md).
2. **Determine intent and impact.** Identify affected contracts, call sites, request/response shapes, database operations, error paths, trust boundaries and likely regressions. For complex changes, provide a concise plan; for simple changes, implement directly.
3. **Use project conventions.** Existing code, scripts, APIs and documented architecture outrank suggested defaults. Never introduce an ORM, validator, router abstraction, test runner or formatting tool when the repository already supplies an appropriate equivalent.
4. **Implement deliberately.** Keep routes thin, validate boundary data, enforce authorization where needed, and preserve backwards compatibility unless a contract change was explicitly requested. Consult [architecture.md](references/architecture.md), [security.md](references/security.md), and [implementation.md](references/implementation.md) as appropriate.
5. **Test changes.** Add or update tests for success, invalid input, forbidden access, failure cases and regression paths proportional to impact. Read [testing-validation.md](references/testing-validation.md) and run the project's relevant checks.
6. **Review your diff.** Inspect `git diff --check` and `git diff`, verify no secrets or unrelated modifications, re-evaluate security and API compatibility. Report changed behavior, tests executed/results, and any unverified risks.

## Task playbooks

- **Feature/API:** trace existing route-to-service-to-data flow; inspect schemas, types and API documentation; implement with existing conventions; add focused tests; update API docs if maintained.
- **Bug:** reproduce or characterize with evidence; find root cause; add a regression test where feasible; fix smallest responsible layer; validate nearby behavior.
- **Refactor:** establish current observable behavior; avoid changing response shapes, error codes, database semantics or side effects; compare before/after tests and call sites.
- **Code review:** do not edit unless asked; inspect full changes plus callers/tests; report only actionable defects with severity, file/line, consequence, and reproduction conditions. Distinguish confirmed findings from questions; do not invent issues.
- **Security:** establish the trust boundary and exploitability; fix authorization/validation/data exposure first, preserving compatibility where possible; create non-sensitive regression cases.
- **Database:** inspect transaction boundaries, locking, constraints and migration strategy; make schema changes reversible where practical; never execute destructive migrations or production operations without explicit permission.
- **Performance:** measure or identify a concrete bottleneck before optimizing; guard against N+1 queries, unbounded reads, event-loop blocking, connection exhaustion and cache invalidation errors.

## Core rules

- Prefer TypeScript `strict`-compatible types. Avoid `any`, unsafe assertions and unchecked casts; narrow `unknown` safely.
- Treat path, query, header and body values as untrusted even if TypeScript types appear correct. Preserve raw-body requirements for signed webhooks.
- Keep handlers async-safe for the installed Express major version; use the existing error middleware and mapping conventions.
- Return stable, deliberate HTTP status codes and response/error formats. Do not leak stack traces, credentials, internal queries or PII.
- Enforce authentication **and** resource-level authorization for protected resources; never infer permission solely from having a valid token.
- Parameterize SQL; constrain filters, pagination and sort fields; use transactions for multi-write invariants and idempotency for retryable mutations where appropriate.
- Handle process shutdown, failures and timeouts according to the project's runtime and infrastructure conventions.
- Do not install packages, update lockfiles, edit environment files or run network-dependent commands unless necessary and permitted. Never fabricate tool outputs.

## Completion response

State the implementation or findings, list key touched paths, report commands run and outcomes, and clearly separate limitations or skipped checks. For reviews, lead with findings ordered by severity, or explicitly say no actionable findings were identified, then describe testing gaps.
