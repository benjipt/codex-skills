# Commit Health Tracking Plan

## Goal
Track how many commits in a repo are in a broken state by running a configurable
acceptance criteria across the last N SHAs, then store results so the Codex
skill can read and learn from them.

## Acceptance Criteria (Default)
- `bun lint`
- `bun run test`
- `bun run test:e2e`
- `bun run build`

Notes:
- This sequence is configured for a specific repo.
- Make this generic/smart/flexible for other repos in the future (per-repo
  overrides or auto-detected criteria).

## High-Level Flow
1. Enumerate last N SHAs (e.g., `git rev-list --max-count N HEAD`).
2. For each SHA:
   - Checkout SHA.
   - Run acceptance commands.
   - Record per-command pass/fail, overall status, duration, and metadata.
3. Skip SHAs already processed (cache).
4. Aggregate results (broken %, most common failing command, trend).

## Data Storage
- Store locally under Codex skill data:
  - `~/.codex/skills/data/commit-health/<repo-id>.jsonl`
  - or `~/.codex/skills/data/commit-health/<repo-id>.sqlite`

## Data Model (Example)
- `repo`, `branch`, `sha`, `timestamp`
- `criteria` (list of commands)
- `results` per command (exit code, duration)
- `status` (pass/fail)

## Integration With Skill
- Skill reads aggregated stats to adjust prompts/workflows.
- Use stored stats to avoid slow or flaky checks by default.
