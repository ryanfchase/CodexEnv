---
name: env-python-entrypoint
description: Resolve the correct Python executable for a codexified repo, preferring repo-local virtualenv paths before falling back to system Python. Use when commands should avoid brittle guessing between .venv, venv, python3, and python.
---

# Env Python Entrypoint

Skill metadata:

- `skill_id`: `env-python-entrypoint`
- `scope`: `shared`
- `template_types`: `single-repo`, `integration-workspace`
- `introduced_in`: `1.1.0`
- `changed_in`: `1.1.0`
- `depends_on`: `runtime-bootstrap.md`

## Workflow

1. Read the repo or workspace `codex-template.json`.
2. Read `runtime-bootstrap.md` if present.
3. Resolve Python in this order:
   - `.venv/bin/python`
   - `.venv/bin/python3`
   - `venv/bin/python`
   - `venv/bin/python3`
   - `python3`
   - `python`
4. Prefer the repo-local executable when available.
5. If the repo documents a different Python entrypoint explicitly, honor the repo documentation.

## Output

Return:

- chosen executable
- why it was chosen
- any mismatch between documented and discovered runtime conventions
