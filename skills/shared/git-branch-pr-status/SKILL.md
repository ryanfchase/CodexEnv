---
name: git-branch-pr-status
description: Determine the current branch state and whether its pull request is open, merged, or missing. Use when a codexified repo needs to decide whether to continue on the current branch or start fresh from main.
---

# Git Branch PR Status

Skill metadata:

- `skill_id`: `git-branch-pr-status`
- `scope`: `shared`
- `template_types`: `single-repo`, `integration-workspace`
- `introduced_in`: `1.1.0`
- `changed_in`: `1.8.0`
- `depends_on`: `env-github-auth`
- `validation_level`: `contract+probe`
- `support_status`: `supported`

## Purpose

Decide whether the current branch is reusable, needs publication, or should be abandoned in favor of a fresh branch from `main`.

## Inputs

- current git branch
- repo `AGENTS.md`
- `gh` PR state for the branch when available

## Preconditions

- the repo follows the Codex branch/PR workflow

## Steps

1. Determine the current git branch.
2. Compare local branch intent against repo `AGENTS.md`.
3. Use `gh` when available to inspect the branch PR state.
4. Report whether the branch should be reused, refreshed from `main`, or published.

## Outputs

Return:

- branch name
- PR state
- recommended next branch action

## Failure Modes

- branch has no upstream and no PR context
- `gh` cannot inspect PR state for the current remote
- repo `AGENTS.md` conflicts with observed branch state

## Validation

- Contract: confirm the skill still matches the documented Codex git workflow.
- Probe: branch and PR inspection should return a concrete next action without mutating repo state.
