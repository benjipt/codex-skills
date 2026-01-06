---
name: atomic-commit-agent
description: Create atomic git commits after completing a feature or logical unit of work and before code review. Use to decompose changes into conventional commits with square-bracket scopes, ensure each commit is complete and reversible, and include the originating model name in commit attribution when provided by the parent prompt.
---

# Atomic Commit Agent

Follow this workflow to turn completed work into clean, atomic commits.

## Workflow

1. Run `git status` to see all changes.
2. Review diffs and identify logical groupings that each do exactly one thing.
3. For each atomic unit:
   - Stage only the relevant files with `git add <files>` or `git add -p`.
   - Verify staged content with `git diff --staged`.
   - Commit with the message format below.
4. If changes span multiple concerns, split them into multiple commits.
5. When working bottom-up, commit foundations first and integration last.

## Commit Message Format

Use conventional commits with square-bracket scopes:

```
type[scope]: imperative summary (50–72 chars)

- Bullet describing what changed
- CLI/tools used if relevant
- LLM/model used if AI-assisted (only if provided)
```

### Commit Types

- `feat` new feature
- `fix` bug fix
- `refactor` restructure without behavior change
- `style` formatting only
- `docs` documentation only
- `test` tests
- `chore` maintenance/tooling
- `build` build/deps
- `perf` performance
- `ci` CI/CD

### Scope Guidelines

- Use lowercase, kebab-case scopes (e.g., `[auth]`, `[contact-form]`).
- Omit scope only if truly global.

## Model Attribution

This skill may be invoked by another model. Do not assume the skill runner is the code author.

- The invoking prompt must specify which model assisted in generating the code.
- Do not co-author commits. Instead, add an `Assisted by` line at the end of the commit message block.
- Extract the model name from the prompt and use it in the `Assisted by` line.
- If no model is specified, pause and request the model name before committing.
- Never use the skill runner's own model name as the assistant.

Examples:

```
Assisted by: GPT-5
```

```
Assisted by: GPT-4.1
```

## Verification Checklist

1. Verify atomicity: the commit does exactly one thing.
2. Verify completeness: no broken imports or syntax errors.
3. Separate concerns: split unrelated changes.
4. Confirm layering: foundational logic is not bundled with integration.

## Do Not Commit

- Mixed feature and refactor changes
- Incomplete implementations or broken states
- Debug statements or stray console logs
- Unrelated formatting bundled with logic
- Foundational logic bundled with UI/routing/integration

## Response Pattern

When asked to commit:

1. Report current git status and proposed atomic grouping.
2. Explain each commit's scope and why it is atomic.
3. Execute commits with proper messages.
4. Confirm with SHA and summary.
