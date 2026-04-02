# Codex Skill Model

This file defines how skills become a first-class operating surface in codexified environments.

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

## First-Class Skill Standard

Use a manifest-plus-prompt model.

- The skill file remains `SKILL.md`.
- The skill file is the authoritative contract for both humans and agents.
- Optional helper scripts may exist, but are not required for a skill to be first-class.
- A skill is first-class only when it is:
  - listed in the relevant `skill-inventory.md`
  - versioned by the owning template or repo
  - validated at its declared level
  - current with the repo's command inventory and runtime bootstrap docs

## Skill Metadata Convention

Every first-class skill should declare:

- `skill_id`
- `scope`
- `template_types`
- `introduced_in`
- `changed_in`
- `depends_on`
- `validation_level`
- `support_status`

Every first-class skill should also include:

- `purpose`
- `inputs`
- `preconditions`
- `steps`
- `outputs`
- `failure_modes`
- `validation`

Recommended `support_status` values:

- `planned`
- `pilot`
- `supported`
- `deprecated`

## Ownership Rules

- Shared skills own cross-repo conventions.
- Repo-local skills own only repo-specific execution details.
- Shared skills may call into repo-local command inventories conceptually, but should not duplicate those commands.
- Repo-local skills should version with the repo they automate, not with `CodexEnv`.
- Shared skills are guaranteed only when they are listed as supported by the current template version.
- Repo-local skills are guaranteed only when they are listed as supported in the repo-local `skill-inventory.md`.

## Skill Registry Rule

- `skill-inventory.md` is the authoritative skill registry for a template, repo, or environment.
- The registry should list:
  - skill id
  - path
  - support status
  - validation level
  - short purpose
- The registry should distinguish:
  - shared foundation skills
  - repo-local or workspace-local skills
  - deferred skills that are planned but not yet first-class

## Validation Model

Use separate validation models for shared and repo-local skills.

### Shared skills

Shared skills should use:

- `contract` validation for every shared skill
- `probe` validation when the skill inspects auth, branch state, or default verification dispatch

Contract validation confirms:

- the skill contract is complete
- the documented workflow still matches the template docs it depends on
- the output contract is explicit enough to reuse across repos

Probe validation confirms:

- the narrowest harmless command path still works
- the skill can inspect, select, or dispatch as documented without widening into full repo verification

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

These should be treated as the minimum first-class shared skill surface for current template lines.
