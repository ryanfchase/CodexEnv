---
name: env-github-auth
description: Check and standardize GitHub CLI authentication for codexified environments. Use when work depends on gh, pull requests, reviews, issue operations, or remote repository access.
---

# Env GitHub Auth

Skill metadata:

- `skill_id`: `env-github-auth`
- `scope`: `shared`
- `template_types`: `single-repo`, `integration-workspace`
- `introduced_in`: `1.1.0`
- `changed_in`: `1.1.0`
- `depends_on`: `runtime-bootstrap.md`

## Workflow

1. Prefer `gh auth status` to verify readiness.
2. If auth is missing or invalid, direct the environment toward `gh auth login`.
3. Treat `gh` as the preferred interface for PR creation and PR status workflows.
4. Do not assume auth is valid just because git remotes exist.

## Output

Return:

- auth status
- whether PR/review operations are ready
- the next required auth step if not ready
