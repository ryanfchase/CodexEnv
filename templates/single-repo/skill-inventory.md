# Single-Repo Skill Inventory

## Shared Foundation Skills

- `env-python-entrypoint`: `skills/shared/env-python-entrypoint/SKILL.md` (`supported`, `contract+probe`) resolve the preferred Python entrypoint
- `env-github-auth`: `skills/shared/env-github-auth/SKILL.md` (`supported`, `contract+probe`) confirm `gh` auth readiness and GitHub write-path safety
- `git-branch-pr-status`: `skills/shared/git-branch-pr-status/SKILL.md` (`supported`, `contract+probe`) determine whether a repo branch should be reused, refreshed, or published
- `git-repo-publish`: `skills/shared/git-repo-publish/SKILL.md` (`supported`, `contract+probe`) stage, commit, push, and open a ready-for-review PR safely
- `verify-run-local-default`: `skills/shared/verify-run-local-default/SKILL.md` (`supported`, `contract+probe`) choose the narrowest meaningful local verification path

## Repo-Local Skills

Derive these from `command-inventory.md` only after the commands stabilize.

- local startup: `.codex/skills/<repo-local-startup>/` (`pilot`, `smoke`) start or attach to a repo runtime safely
- local validation: `.codex/skills/<repo-local-validation>/` (`pilot`, `static`) run stable repo-native verification commands
- local publish helpers: `.codex/skills/<repo-local-publish>/` (`planned`, `static`) wrap stable repo-specific publish checks when they exist

## Registry Rule

- Each listed skill should include:
  - path
  - support status
  - validation level
  - short purpose
- Skills not listed here are not first-class for the repo yet.
