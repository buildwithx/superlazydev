# Repository-first stack detection

Run this inspection before proposing architecture or editing files. Avoid treating dependency presence alone as proof a library is in use; verify imports and runtime wiring.

## Inspect

- Scope: `pwd`, `git status --short`, ancestor/scoped `AGENTS.md`, package workspaces, nearest `package.json` and lockfiles (`bun.lock`, `bun.lockb`, `pnpm-lock.yaml`, `yarn.lock`, `package-lock.json`). Respect a monorepo's package boundary.
- Runtime and TS: Node/Bun version declarations, `engines`, `.nvmrc`, `.node-version`, `tsconfig*`, tsx/ts-node, ESM vs CJS, path aliases, build scripts and output target.
- Web stack: installed Express major version, entrypoint, `Router` mounting, middleware order, error handler, request typing and `express-async-errors`/wrappers. Express 4 and 5 differ in async rejection handling.
- Validation/contracts: Zod, Joi, express-validator, class-validator, typebox, Yup, OpenAPI generators, Swagger docs, shared DTOs.
- Data: Prisma (`schema.prisma`), Drizzle, TypeORM, Sequelize, Knex, Mongoose, raw SQL, migrations, connection lifecycle, repositories and transactions.
- Auth and infrastructure: JWT/session/OAuth, authorization guards, cookie and CORS settings, Redis, queues, background jobs, logging, tracing, observability, deployment/runtime config.
- Quality: Jest/Vitest/Node test runner, Supertest, ESLint, Prettier, formatting, coverage thresholds, test databases, containers, CI scripts.

Useful read-only commands, adapted to the repository: `cat package.json`, `find . -name AGENTS.md -print`, `rg 'express\(|Router\(|errorHandler|zod|prisma|drizzle' src test`, `rg --files | head -100`. Avoid scanning `node_modules`, `.git`, generated outputs, or secrets.

## Decision rules

1. If project conventions and dependencies are evident, use them, even if they are not your preferred tools.
2. If conflicting patterns exist, prefer the pattern in the affected feature and the most recent maintained code; explain substantial ambiguity.
3. If there is no established pattern for a **new** application, suggest a lean baseline: Express + TypeScript strict mode, schema validation at the edge, centralized error handling, structured logging, env validation, tests and safe shutdown. Choose supporting libraries only when requirements warrant them.
4. Identify available package-manager and scripts rather than assuming `npm`, `pnpm`, `yarn` or `bun`. Do not switch managers.
5. Treat incompatible major-version APIs as distinct. Verify installed versions before adopting copied examples.
