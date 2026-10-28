# Implementation and debugging workflow

## New endpoint

1. Find sibling routes and their validation, authentication, services, persistence and tests.
2. State endpoint contract: method/path, allowed principals, body/query/params, response statuses, error cases, pagination/idempotency semantics.
3. Implement using repository-local patterns. Align runtime parsing and inferred TS types. Do not mutate global app behavior for a single feature unnecessarily.
4. Enforce resource authorization in the business/data flow; add race-safe DB constraints and transactions when needed.
5. Update OpenAPI or other contract source of truth if maintained, and add tests for nominal, invalid and denied paths.

## Debug

1. Reproduce through a test, minimal request or trace when possible, without requiring real credentials.
2. Follow inbound middleware order through handlers, service, DB and outbound dependencies. Distinguish user input, application state, infrastructure failure and races.
3. Identify the actual failing assumption; avoid symptom-only catches, arbitrary retries and broad `try/catch` that hides errors.
4. Fix at the narrowest correct layer and preserve error translation. Add targeted regression tests.

## Refactor / review

- Capture expected behavior before editing: route signatures, status codes, serialized JSON, side effects and transaction boundaries.
- Reuse utilities only when duplication represents a stable shared abstraction; avoid speculative generalized frameworks.
- For reviews, quote exact file location and observable failure trigger; rank security/data integrity/availability bugs above minor performance issues; do not present preferences as defects.
- On completion, summarize concrete behavior change and any unverified edge cases. Avoid claiming tests pass when environment/config prevents execution.
