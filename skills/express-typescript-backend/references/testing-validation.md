# Testing and validation gate

## Choose existing tools

Inspect `package.json` scripts and CI; run only relevant commands through the project's package manager. Do not replace existing Jest/Vitest/Node test runner or lint setup. Prefer focused checks first and broader checks when feasible. Examples are illustrative: `test`, `typecheck`, `lint`, `build`, `format:check`.

## Test matrix

- Happy path: response contract, side effect, persistence and status.
- Input boundary: missing required fields, malformed types, invalid IDs, pagination bounds, unexpected fields.
- Auth: anonymous (401), authenticated without permission (403 or repository standard), other-tenant or other-owner resources, list leakage.
- Errors: missing resource, duplicate/unique conflict, downstream timeout, DB failure handling and sanitized response.
- Concurrency: retry/idempotency, transactional atomicity and race-prone uniqueness where relevant.
- Security-specific: upload constraints, signed webhooks, secrets redaction, injection attempts appropriate to feature.

Use isolated fixtures and disposable DBs; never point destructive test setup at production. Mock external services but retain meaningful handler-through-service tests where practicable. Assert stable response semantics, not implementation details.

## Mandatory closing checks

1. Run focused tests for changed code if available.
2. Run TypeScript typecheck, lint and build as supported and feasible; note exact skip reasons.
3. Inspect generated changes, `git diff --check`, `git diff --stat` and changed file content.
4. Check for debug prints, TODO placeholders, secret spills, broad type assertions, unsafe error leaks and accidental contract changes.
5. Report each validation command and whether it passed, failed or was not run. Do not label partial validation as fully verified.
