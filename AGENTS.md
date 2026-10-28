# Repository Guidelines

## Project Structure & Module Organization

This repository publishes reusable Codex skills under `skills/<skill-name>/`. Each skill's entry point and core workflow live in its `SKILL.md`; optional `references/` files hold longer or topic-specific guidance, and `agents/openai.yaml` holds display metadata. The current `frontend-engineer` skill includes Flutter, React/Next.js, other web frameworks, and shared quality references. Keep new guidance near the relevant skill or reference instead of creating unrelated top-level directories. `README.md` is the repository overview and contributor guide; update its Available skills section when adding a skill intended for discovery.

## Build, Test, and Development Commands

There is no application build or automated test command configured. Use `rg --files` to review repository contents and `rg '^#{1,3} '` on `README.md` and `skills/` to check documentation heading structure. Before submitting, read the changed Markdown in full, verify referenced paths exist, and inspect `git diff --check` for whitespace errors. Do not claim a build or test passed when no such command exists.

## Writing Style & Naming Conventions

Write concise, direct instructions with actionable steps and Markdown headings. Match the existing skill format: a short YAML front matter block with a stable `name` and clear `description`, followed by numbered workflow sections where useful. Use lowercase kebab-case for skill directories and reference filenames (for example, `frontend-engineer` and `react-next.md`). Keep framework-specific advice in its matching reference; put cross-framework guidance in `quality.md`. For each new skill, keep its instructions and supporting files together and update the README index when appropriate.

## Testing Guidelines

No test framework or test files are present. For documentation changes, review links and commands against the repository, check Markdown structure, and read the final diff. If executable validation is added later, document its command in the relevant skill and run it before submitting.

## Commit & Pull Request Guidelines

Recent history favors Conventional Commit prefixes such as `feat:` and `fix:`; use a concise imperative subject, for example `docs: clarify skill validation steps`. A pull request should explain the user-facing documentation change, list the files affected, and note the checks performed. Include screenshots only when a visual rendering change makes them useful.

## Security & Configuration

Do not commit credentials, tokens, or private project data. Keep `agents/openai.yaml` limited to skill metadata and avoid unrelated machine-specific files; `.gitignore` excludes `.DS_Store` and `node_modules/`.
