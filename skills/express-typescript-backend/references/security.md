# Express + TypeScript security checklist

Apply in proportion to touched trust boundaries; repository policy takes precedence when stronger.

## Inputs and authorization

- Treat all request input as untrusted; validate structure, length, formats, ranges and enum membership. Runtime schemas are not optional just because TS types exist.
- Verify authentication and authorization separately, including per-tenant and per-resource ownership on reads, writes, lists and indirect references. Check that data-layer filtering cannot reveal another tenant's records.
- Do not build SQL with interpolation; parameterize values and allowlist dynamic table/column/sort identifiers. Constrain regular expressions, uploads and payload size.
- For outbound URLs or fetches, address SSRF with allowlists and network restrictions; validate redirects and DNS rebinding exposure when relevant.
- Avoid mass assignment, unsafe path traversal, command injection and prototype-pollution patterns. Use safe deserialization and filenames.

## Session, headers and secrets

- Check CORS origin allowlisting, credentials behavior, security headers, secure cookies, SameSite/CSRF requirements and proxy trust configuration against actual deployment.
- Avoid exposing access tokens, passwords, API keys, session IDs and PII in logs, exceptions, URLs, traces or fixtures. Keep `.env` files unchanged unless explicitly asked; never print secret values.
- Verify password hashing and JWT signature/algorithm/audience/issuer/expiry according to existing auth standards. For cookies, include CSRF protections where needed.
- For webhooks: preserve raw body until signature verification; verify using provider's timing-safe method and replay window; make side effects idempotent.
- Rate limit expensive/public/auth endpoints as appropriate, taking proxies and distributed replicas into account.

## Response and operations

- Centralize error handling and avoid returning stack traces, SQL errors or internal auth reasons. Preserve useful correlation IDs.
- Use least-privilege database and infrastructure credentials. Avoid unsafe production DB changes, unrestricted destructive commands or auth bypasses for tests.
- Prefer existing audited dependencies, lockfile integrity and minimal dependency additions; check changes that affect vulnerability exposure.
