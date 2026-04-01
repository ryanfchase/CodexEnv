---
name: git-branch-pr-status
description: Determine the current branch state and whether its pull request is open, merged, or missing. Use when a codexified repo needs to decide whether to continue on the current branch or start fresh from main.
---

# Git Branch PR Status

Skill metadata:

- `skill_id`: `git-branch-pr-status`
- `scope`: `shared`
- `template_types`: `single-repo`
- `introduced_in`: `1.1.0`
- `changed_in`: `1.1.0`
- `depends_on`: `env-github-auth`

## Workflow

1. Determine the current git branch.
2. Compare local branch intent against repo `AGENTS.md`.
3. Use `gh` when available to inspect the branch PR state.
4. Report whether the branch should be reused, refreshed from `main`, or published.

## Output

Return:

- branch name
- PR state
- recommended next branch action
