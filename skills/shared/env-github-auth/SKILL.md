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
- `changed_in`: `1.8.0`
- `depends_on`: `runtime-bootstrap.md`
- `validation_level`: `contract+probe`
- `support_status`: `supported`

## Purpose

Confirm that `gh` is the usable GitHub write path for the current codexified environment.

## Inputs

- repo or workspace root
- local `runtime-bootstrap.md`

## Preconditions

- `gh` should be installed when GitHub write workflows are expected

## Steps

1. Prefer `gh auth status` to verify readiness.
2. If auth is missing or invalid, direct the environment toward `gh auth login`.
3. Treat `gh` as the preferred interface for PR creation and PR status workflows.
4. When a workflow needs to create or update PR descriptions, prefer `--body-file` over inline shell body arguments.
5. Do not assume auth is valid just because git remotes exist.

## Outputs

Return:

- auth status
- whether PR/review operations are ready
- the next required auth step if not ready

## Failure Modes

- `gh` is not installed
- auth exists but is invalid for the current remote
- repo workflow assumes connector writes that are not actually available

## Validation

- Contract: confirm the skill matches shared GitHub write-path guidance and PR body safety rules.
- Probe: `gh auth status` should succeed or report a concrete remediation path.
