# Architecture and API contracts

## Boundary responsibilities

- Router: declare HTTP methods, route structure, ordered middleware and handler binding.
- Controller/handler: parse validated input and translate application results into HTTP response; avoid domain logic and direct complex persistence access if project layers separate them.
- Service/use case: business invariants, authorization decisions and transaction coordination.
- Repository/data access: parameterized persistence, explicit projection and pagination, consistent error translation where appropriate.
- Middleware: cross-cutting authentication, authorization, validation, request IDs, centralized error mapping and observability.

These are boundaries, not a mandate to introduce folders/classes/DI. Follow existing module style; keep dependency direction clear and avoid circular imports.

## API rules

- Validate input at runtime and keep TS request types aligned with parsed schemas. Define allowlisted fields to prevent mass assignment.
- Preserve route/method/status/response compatibility; document intentional breaking changes, deprecation and versioning.
- Use correct response semantics (e.g. 201 for created resources, 204 without body, 400 malformed input, 401 unauthenticated, 403 unauthorized, 404 not found, 409 conflict, 422 validation where repo standard); preserve established mappings.
- Provide pagination bounds, deterministic sorting and a stable cursor if cursor pagination is selected; avoid opaque unbounded offsets for large datasets when inappropriate.
- Use consistent error codes and correlation IDs; redact implementation details from public responses.
- Ensure async job/side effect and DB write ordering respects retry semantics; avoid double-processing on retries.

## Storage and operations

- Implement database constraints for critical uniqueness/invariants as well as application checks.
- Use transactions when a partial commit violates business rules, and understand isolation/locking under concurrent requests.
- Plan migrations with compatibility between deployed app versions; backfill safely and avoid destructive rollback assumptions.
- Avoid N+1 DB reads and eager fetching of sensitive or large columns; select explicit fields when useful.
- Avoid CPU-heavy synchronous operations in the request thread; set timeouts and bounded retries for external dependencies.
