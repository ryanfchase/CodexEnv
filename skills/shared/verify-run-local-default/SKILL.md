---
name: verify-run-local-default
description: Choose and run the default local verification path for a codexified repo using its documented verification-first workflow and command inventory. Use when a repo needs the narrowest meaningful local validation before broader checks.
---

# Verify Run Local Default

Skill metadata:

- `skill_id`: `verify-run-local-default`
- `scope`: `shared`
- `template_types`: `single-repo`, `integration-workspace`
- `introduced_in`: `1.1.0`
- `changed_in`: `1.8.0`
- `depends_on`: `command-inventory.md`, `verification-first.md`, `runtime-bootstrap.md`
- `validation_level`: `contract+probe`
- `support_status`: `supported`

## Purpose

Select the narrowest meaningful local verification command using the repo's documented verification ladder instead of ad hoc judgment.

## Inputs

- local `verification-first.md`
- local `command-inventory.md`
- task context about the changed surface

## Preconditions

- the repo has a grounded command inventory and verification ladder

## Steps

1. Read the local `verification-first.md`.
2. Read the local `command-inventory.md`.
3. Select the narrowest meaningful validation command for the requested change.
4. Escalate only when the environment requires it.
5. Report what was run and what broader checks remain.

## Outputs

Return:

- command selected
- reason it is the default local check
- remaining validation not yet run

## Failure Modes

- the repo has no grounded `verification-first.md`
- `command-inventory.md` is stale or ambiguous
- the requested task touches multiple systems and no narrow default exists

## Validation

- Contract: confirm the selection rules match the repo verification-first model.
- Probe: given a concrete repo, the skill should identify one documented default path without widening unnecessarily.
