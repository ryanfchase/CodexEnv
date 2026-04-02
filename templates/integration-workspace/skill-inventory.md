# Integration-Workspace Skill Inventory

## Shared Foundation Skills

- `env-python-entrypoint`: `skills/shared/env-python-entrypoint/SKILL.md` (`supported`, `contract+probe`) resolve the preferred Python entrypoint
- `env-github-auth`: `skills/shared/env-github-auth/SKILL.md` (`supported`, `contract+probe`) confirm `gh` auth readiness and GitHub write-path safety
- `verify-run-local-default`: `skills/shared/verify-run-local-default/SKILL.md` (`supported`, `contract+probe`) choose the narrowest meaningful local verification path

## Workspace Skills

- contract inspection: `.codex/skills/<workspace-contract-inspection>/` (`pilot`, `static`) read versioned runtime and consumption contracts
- shared service orchestration: `.codex/skills/<workspace-service-orchestration>/` (`pilot`, `smoke`) render, start, and tear down checked-in orchestration entrypoints
- workspace publish coordination: `.codex/skills/<workspace-publish-coordination>/` (`planned`, `static`) coordinate multi-repo publish steps when explicitly owned by the environment

## Child Repo Skills

Derive child repo skills from each child repo `command-inventory.md` and classify each one as `static` or `smoke`.

## Registry Rule

- Each listed skill should include:
  - path
  - support status
  - validation level
  - short purpose
- Skills not listed here are not first-class for the workspace yet.
