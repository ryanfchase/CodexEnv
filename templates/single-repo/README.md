# Single-Repo Template

Use this template for a repo that owns its code, validation, and release workflow end to end.

This is the source template. Derive integration-workspace behavior from it only when sibling repositories must be coordinated together.

## Template Shape

- `AGENTS.md` sets the operating rules.
- `codex-template.json` identifies the template line, version, and drift state.
- `runtime-bootstrap.md` records the repo's runtime, auth, and escalation conventions.
- `verification-first.md` records the local validation ladder.
- `command-inventory.md` lists the repeatable commands that may later become skills.
- `skill-inventory.md` maps shared foundation skills and future repo-local skills.
- repo-local skills under `.codex/skills/` should declare a `validation_level` and a minimal validation section.
- every repo-local skill requires `static` validation; use `smoke` validation only for runtime-sensitive or stateful skill paths.
- `verification-first.md` should be instantiated from the cataloged command examples.

## Standard Workflow

1. Inspect the relevant code path.
2. Confirm the branch and PR state.
3. Start from the latest `origin/main`.
4. Make the smallest safe change.
5. Run verification in order from fastest to broadest.
6. Commit, push, and open a PR after the checks pass.
