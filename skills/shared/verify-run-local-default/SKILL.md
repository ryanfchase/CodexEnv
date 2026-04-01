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
- `changed_in`: `1.1.0`
- `depends_on`: `command-inventory.md`, `verification-first.md`, `runtime-bootstrap.md`

## Workflow

1. Read the local `verification-first.md`.
2. Read the local `command-inventory.md`.
3. Select the narrowest meaningful validation command for the requested change.
4. Escalate only when the environment requires it.
5. Report what was run and what broader checks remain.

## Output

Return:

- command selected
- reason it is the default local check
- remaining validation not yet run
