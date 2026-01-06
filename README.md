# codex-skills

Note: This skill set is still being tested.

A small set of reusable Codex skills for clean git history and lightweight code review.

## Included skills

- `atomic-commit-agent`: Create clean, atomic commits after completing work.
- `code-reviewer`: Review committed changes and suggest improvements (no edits).

## Installation

Use the one-liner below to fetch the `skills/` folder and place it alongside any existing skills:

```
mkdir -p ~/.codex/skills && \
  curl -L https://github.com/benjipt/codex-skills/archive/refs/heads/main.tar.gz | \
  tar -xz --strip-components=2 -C ~/.codex/skills codex-skills-main/skills
```

This creates `~/.codex/skills` if needed, downloads the repo tarball, and extracts only the `skills/` subfolder into your Codex skills directory.

If you prefer, you can copy the skill folders manually into your Codex skills directory (commonly `$CODEX_HOME/skills` or `~/.codex/skills`):

```
skills/atomic-commit-agent/
skills/code-reviewer/
```

## Workflow

```
complete feature → atomic-commit-agent → code-reviewer → (if improvements implemented) atomic-commit-agent → done
```

1. Complete your feature or fix.
2. Run `atomic-commit-agent` to commit working code.
3. Run `code-reviewer` for a single review cycle.
4. If you implement suggestions, run `atomic-commit-agent` again (do not re-run review).

## Usage

Mention the skill name in your prompt:

- "call atomic-commit-agent"
- "use code-reviewer"
- "use $atomic-commit-agent"

## Packaging (optional)

Skills can be packaged into `.skill` files for distribution, but they are not required for use. Use your local Codex packager if you have it installed:

```
python3 $CODEX_HOME/skills/.system/skill-creator/scripts/package_skill.py skills/atomic-commit-agent
python3 $CODEX_HOME/skills/.system/skill-creator/scripts/package_skill.py skills/code-reviewer
```

## Contributing

Contributions are welcome! When modifying a skill:

1. Follow the skill format above
2. Provide a use case for the suggested change
4. Test the skill before submitting

## License

MIT.
