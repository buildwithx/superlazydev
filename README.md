# SuperLazyDev

SuperLazyDev is a collection of reusable Codex skills. Each skill gives Codex a focused workflow for a particular kind of work, with supporting references and metadata kept alongside it.

This repository is intended to grow: add each new skill as its own directory under `skills/` so its instructions, references, and metadata stay together.

## Available skills

### `frontend-engineer`

Helps Codex implement, debug, refactor, review, and validate frontend work in the current repository. It detects the app's framework and conventions, then follows the matching guidance for Flutter, React/Next.js, or other web frameworks.

Example requests:

```text
$frontend-engineer Implement a responsive login screen
using the existing project architecture.
```

```text
$frontend-engineer Review this Flutter feature
for bugs, performance issues, and best practices.
```

```text
$frontend-engineer Refactor this component,
preserve behavior, and run relevant tests.
```

## Repository layout

```text
skills/
  <skill-name>/
    SKILL.md                 # Skill instructions and workflow
    agents/openai.yaml       # Optional display metadata
    references/              # Optional topic-specific guidance
```

Current skill files:

- `skills/frontend-engineer/SKILL.md` — main instructions and workflow.
- `skills/frontend-engineer/references/` — framework-specific and shared frontend guidance.
- `skills/frontend-engineer/agents/openai.yaml` — display name and short description.

## Add a skill

1. Create `skills/<skill-name>/SKILL.md`, using a lowercase kebab-case directory name.
2. Add YAML front matter with a stable `name` and a concise `description` that says what the skill does and when to use it.
3. Write instructions that are specific to the skill's job. Keep the main workflow in `SKILL.md`; move lengthy or specialized guidance into `references/` and link to it with relative paths.
4. Add `agents/openai.yaml` when the skill needs display metadata in the Codex UI. Follow the existing shape:

   ```yaml
   interface:
     display_name: "Skill Name"
     short_description: "A concise description"
   ```

5. Update **Available skills** and the repository layout or examples in this README when the new skill should be discoverable here.
6. Review the complete diff and verify all referenced files and commands exist.

Keep each skill focused. Put shared guidance in the relevant skill reference rather than creating unrelated top-level files. Avoid duplicating instructions across skills when a focused reference can be linked instead.

## Skill writing guidelines

- Use a short description that makes the skill's scope and activation conditions clear.
- Use concise headings and direct, actionable instructions.
- Explain the workflow in the order Codex should perform it, including discovery, implementation or review, and validation where relevant.
- State important boundaries: when to ask for missing information, what must be preserved, and what should not be changed.
- Link to supporting files using paths relative to the skill directory, and check those paths after edits.
- Keep `agents/openai.yaml` limited to UI metadata; put workflow instructions in `SKILL.md` or its references.

## Validate documentation changes

There is no application build or automated test command configured in this repository. For skill or README changes, run these checks from the repository root:

```sh
rg --files
rg '^#{1,3} ' README.md skills
git diff --check
```

Also read each changed Markdown file in full and confirm that linked files, example paths, and documented commands match the repository. Do not report a build or test as passing when no such command exists.

## Contributing

Keep changes focused on the skill being added or updated and its documentation. Do not commit credentials, tokens, or private project data. Use a concise Conventional Commit subject when committing, such as `docs: add database-review skill`.
