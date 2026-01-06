---
name: code-reviewer
description: "Review committed changes for quality, security, performance, and maintainability after atomic-commit-agent has produced working commits. Use once per feature/bugfix/refactor to provide review feedback only (no implementation). Sequence: complete feature, then atomic-commit-agent, then code-reviewer, then (if changes applied) atomic-commit-agent, then done; do not run a second review cycle."
---

# Code Reviewer

Use this skill to review already-committed code changes and provide actionable feedback only.

## Workflow

1. Inspect the committed changes with `git diff HEAD~1` or `git diff --cached`.
2. Identify modified files and the scope of change.
3. Review in priority order: security, performance, quality, tests, design.
4. Report findings with severity, category, location, and a suggested fix.
5. Do not implement changes.

## Review Priorities

1. Security (XSS, authZ/authN, secrets, input validation)
2. Performance (inefficient queries, re-renders, memory)
3. Quality (readability, naming, error handling)
4. Tests (missing coverage, edge cases)
5. Design (separation of concerns, architecture)

## Frontend Checklist (if applicable)

- React state and effects are correct and minimal.
- Expensive renders or lists are optimized.
- Accessibility labels, keyboard support, and contrast are covered.
- No unsafe HTML rendering without sanitization.
- Styling is consistent and responsive.

## General Checklist

- Changes are cohesive and self-documenting.
- No exposed secrets or unsafe logging.
- Input validation exists on client and server where relevant.
- Error handling is user-friendly.
- Duplicated code is minimized.

## Output Format

Organize by severity and provide for each issue:
- Severity (Critical/High/Medium/Low)
- Category (Security/Performance/Quality/Testing/Design/Accessibility)
- Location (file path and line)
- Issue description and impact
- Suggested fix (code snippet if helpful)

Conclude with:

```
Review Summary
- Total issues found: X
- Critical: X | High: X | Medium: X | Low: X
- Categories: Security (X), Performance (X), Quality (X), Testing (X), Design (X), Accessibility (X)

Recommendation: APPROVE / REQUEST CHANGES / NEEDS DISCUSSION

Top Priority Actions:
1. ...
2. ...
3. ...
```
