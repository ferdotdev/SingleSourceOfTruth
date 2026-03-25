---
name: docs-conventions
description: "Conventions, structure and formatting rules for project documentation. Use this skill whenever creating or editing any .md documentation file, context files (AGENTS.md, CLAUDE.md, GEMINI.md, COPILOT.md, etc.), or any file inside /docs."
---

## Documentation Structure

Every project should maintain documentation in these locations:

| Location | Purpose |
|---|---|
| Context files (root) | Single source of truth for AI agents: rules, skills, agents, commands |
| `/docs/*.md` | Detailed documentation: guides, cheat sheets, troubleshooting |

Context files are any `.md` file in the project root intended for AI agents.

The one you should pay the most attention to, and the only one you should edit, is `AGENTS.md`.

This is because `CLAUDE.md`, `GEMINI.md`, `copilot-instructions-md`, and similar files have a symbolic link to `AGENTS.md` to maintain a "Single Source of Truth" approach and share the same conventions.

## Writing Rules

- Use imperative tone: "Run the command..." not "You can run the command..."
- Keep paragraphs short (3-4 lines max)
- One concept per section
- Prefer examples over explanations
- Match the language the project already uses in its docs, example if another docs are written in spanish like:

como-ejecutar-el-proyecto.md
comandos-frecuentes.md
buenas-practicas.md

Continue writing in spanish, NOT in english, to keep the consistency in the documentation

But if the documentation is in english by default, write in english

This does not apply for AGENTS.md and context files, which should be written in english, to maintain the consistency with the context files of the agents, like CLAUDE.md, GEMINI.md, etc.

## Formatting Standards

### Headings

```markdown
# Document Title (only one per file)
## Major Section
### Subsection
```

- Never skip heading levels (no `#` → `###`)
- Use sentence case: "How to run the project" not "How To Run The Project"

### Code Blocks

- Always specify the language: ```bash, ```js, ```php, ```py, etc.
- Include only runnable/realistic code, no pseudocode unless explicitly needed
- Add a brief comment above non-obvious commands

```bash
# Start containers in detached mode
docker compose up -d
```

### Commands and CLI References

Document commands with this format:

```markdown
### `command-name`

> Short description of what it does

**Usage:**
​```bash
command-name [options] <required-arg>
​```

**Example:**
​```bash
command-name --flag value
​```
```

### Tables

Use tables for comparisons, option lists, or environment variables:

```markdown
| Variable | Default | Description |
|---|---|---|
| `APP_PORT` | `8000` | Application port |
```

## Content Guidelines by File Type

### Context Files (AGENTS.md, CLAUDE.md, etc.)

These are **context files for AI agents**. They must be concise and scannable:

- Start with a brief project summary (stack, purpose, high-level architecture)
- List active rules with a one-liner description each
- List available skills and agents with their trigger/purpose
- Include frequently used commands grouped by category (dev, test, deploy, db, etc.)
- Specify versions of key dependencies when relevant
- Never include lengthy tutorials — link to `/docs/` instead

Example structure:

```markdown
# Project Context

## Stack
- Language: [language + version]
- Framework: [framework + version]
- Infra: [docker, cloud, etc.]

## Rules
- **rule-name**: What it enforces

## Commands
### Development
- `[start-command]` — Starts the dev server
- `[test-command]` — Runs the test suite

## Skills & Agents
- **agent-name**:
- **skill-name**:

What it does and when to invoke it
```

### /docs/ Files

These are **detailed documentation for humans and agents**. They should:

- Have a clear, descriptive filename: `setup-guide.md`, `troubleshooting.md`, `commands-cheatsheet.md`
- Start with a one-paragraph summary of what the doc covers
- Include a table of contents if the document has more than 3 sections
- End with a "See also" section linking related docs when applicable
- Include last updated date at the bottom: `> Last updated: YYYY-MM-DD`

### Suggested /docs/ Files

Not every project needs all of these, create them as the project grows:

- `setup-guide.md` — How to set up the project from scratch
- `commands-cheatsheet.md` — Quick reference for frequently used commands
- `architecture.md` — High-level architecture, folder structure, data flow
- `troubleshooting.md` — Common errors and their solutions
- `conventions.md` — Code style, naming, branching strategy
- `deployment.md` — How to deploy, environments, CI/CD

## Versioning and Change Tracking

When updating documentation due to dependency or tooling changes:

- Mention the **previous version** and the **new version**
- Note any breaking changes or migration steps needed
- Example: "Updated from FrameworkX 3.x → 4.x. See [migration guide](link)."

## What NOT to Document

- Auto-generated files or boilerplate unless customized
- Secrets, tokens, or credentials (reference `.env.example` or a vault instead)
- Temporary workarounds without marking them as `<!-- TODO: remove after X -->`
- Duplicate information already covered in another doc — link to it instead
- External library documentation that's already well-maintained upstream — link to it

## How to Decide What to Document

Ask these questions before writing:

1. **Will someone (human or agent) need this more than once?** → Document it
2. **Did someone just waste time figuring this out?** → Document it
3. **Did a dependency or config change?** → Update the affected docs
4. **Is it already documented elsewhere in the project?** → Link, don't duplicate
5. **Is it trivial and obvious from the code?** → Skip it