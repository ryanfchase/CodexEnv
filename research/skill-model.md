# Codex Skill Model

This file defines how skills are organized in codexified environments.

## Skill Classes

### Shared foundation skills

These live in `CodexEnv/skills/shared/` and are reusable across codexified environments.

Use them for:

- runtime discovery
- GitHub auth checks
- git/PR status workflows
- default verification dispatch

### Repo-local skills

These are derived from a repo or workspace `command-inventory.md`.

Use them for:

- repo-specific startup commands
- repo-specific validation commands
- repo-specific operational flows

Do not create repo-local skills until the command inventory is stable.

## Skill Metadata Convention

Every skill should declare:

- `skill_id`
- `scope`
- `template_types`
- `introduced_in`
- `changed_in`
- `depends_on`

## Ownership Rules

- Shared skills own cross-repo conventions.
- Repo-local skills own only repo-specific execution details.
- Shared skills may call into repo-local command inventories conceptually, but should not duplicate those commands.

## First Shared Skill Set

- `env-python-entrypoint`
- `env-github-auth`
- `git-branch-pr-status`
- `git-repo-publish`
- `verify-run-local-default`
