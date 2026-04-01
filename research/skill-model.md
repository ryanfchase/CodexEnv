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

Recommended location:

- `<repo>/.codex/skills/`

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
- `validation_level`

## Ownership Rules

- Shared skills own cross-repo conventions.
- Repo-local skills own only repo-specific execution details.
- Shared skills may call into repo-local command inventories conceptually, but should not duplicate those commands.
- Repo-local skills should version with the repo they automate, not with `CodexEnv`.

## Validation Model

Use a two-tier validation model for repo-local skills.

### Static

Required for every repo-local skill.

Confirm that:

- the skill is listed in `skill-inventory.md`
- the command or workflow matches `command-inventory.md`
- dependencies match `runtime-bootstrap.md` and shared skill assumptions
- the output contract is documented

### Smoke

Required only for repo-local skills that:

- start services
- run Docker
- open service or database shells
- depend on process readiness or container state

Smoke checks should stay minimal and validate the skill dispatch path rather than the whole repo.

## First Shared Skill Set

- `env-python-entrypoint`
- `env-github-auth`
- `git-branch-pr-status`
- `git-repo-publish`
- `verify-run-local-default`
