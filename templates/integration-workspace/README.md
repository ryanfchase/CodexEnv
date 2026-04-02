# Integration-Workspace Template

Use this template for a workspace that contains sibling repositories, such as backend, frontend, and service directories that must coordinate through explicit contracts.

This template is derived from the single-repo workflow. Add only the cross-repo rules that are necessary to keep the boundary explicit.

## Template Shape

- `AGENTS.md` defines workspace routing and cross-repo behavior.
- `README.md` should include a `Codex Status` section that summarizes current stage, readiness, remaining work, and available toolkit entries.
- `readme-codex-status.md` provides the standard shape for that README dashboard section.
- `codex-template.json` identifies the template line, version, codexification stage, conformity state, and drift state.
- `codex-assessment.md` records the current readiness scorecard, evidence, and next promotion target.
- `runtime-bootstrap.md` records workspace runtime, auth, and escalation conventions.
- `verification-first.md` records how to validate contracts across repos.
- `command-inventory.md` lists the repeatable commands for each child repo.
- `skill-inventory.md` maps shared foundation skills plus workspace and child-repo skill layers.
- workspace and child-repo skills should declare a `validation_level`; require `static` for all and reserve `smoke` for runtime-sensitive flows.
- The child repo inventories should be seeded from the shared command catalog.

## Standard Workflow

1. Identify the child repo that owns the task.
2. Read that repo's `AGENTS.md`.
3. Inspect both sides of any contract change.
4. Start from the latest `origin/main` in each touched repo.
5. Validate each touched repo with its own commands.
6. Commit, push, and open PRs only after the cross-repo checks pass.
