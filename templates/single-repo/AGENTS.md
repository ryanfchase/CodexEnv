# AGENTS.md

Instructions in this template apply to a single git repository.

## Workflow

- Treat this template as the canonical starting point for new repo work.
- Add a root-level `codex-template.json` so the repo advertises its template version, codexification stage, conformity status, and drift status.
- Add a root-level `codex-assessment.md` so the repo records the evidence behind its current stage and readiness.
- Add a repo-local `runtime-bootstrap.md` so shared skills can discover runtime and auth assumptions consistently.
- Add repo-local skills under `.codex/skills/` once the command inventory is stable.
- Inspect the relevant code paths before editing. Prefer `rg` for search.
- Keep changes minimal and localized to the requested behavior.
- Do not revert user changes you did not make.
- Use `apply_patch` for manual file edits.
- Before starting new work, check whether the current branch has an associated pull request and whether it is already merged.
- If the current branch's PR is merged, switch to `main`, pull the latest `origin/main`, and create a fresh `codex/<short-slug>` branch before making changes.
- Start implementation work from the latest `main`:
  - update local `main` from `origin/main`
  - create a new branch named `codex/<short-slug>`
  - do not make feature or bugfix commits on `main`
- If a change affects another repo or a cross-repo contract, stop and confirm ownership before editing beyond this repo.
- Treat the default stopping point as "verified and publishable." Do not assume this repo must also own last-mile deployment unless it explicitly says so.

## Verification

- Run the repo's native verification commands before responding.
- Use a verification-first ladder:
  - format or lint first
  - targeted tests next
  - broader tests when shared behavior changes
  - smoke, e2e, or compose-based checks when the repo exposes runnable services
- Keep the command inventory in the matching `command-inventory.md` file up to date.
- Seed that inventory from `research/command-catalog.md`, then replace placeholders with the repo's actual commands.
- Keep `skill-inventory.md` aligned with the shared foundation skills plus any repo-local skills derived from stable command inventory entries.
- Keep `.codex/skills/` aligned with `skill-inventory.md`; repo-local skills should be thin wrappers around documented repo commands.
- Validate every repo-local skill statically, and add smoke validation only when the skill starts services, runs Docker, or opens shells.
- Update `codex-template.json` whenever the repo is brought forward to a newer template version, when its codexification stage changes, when readiness evidence changes materially, or when local overrides change materially.
- Update `codex-assessment.md` whenever the readiness scorecard, latest evidence, or next promotion target changes.
- If the repo publishes container images, document that as an explicit optional capability rather than assuming it is part of the base codexification contract.
- When a repo opts into container publishing, keep the build or push path aligned with the repo's documented verification path and the owning GitHub Actions workflow.
- Container publication proves artifact readiness. It does not by itself require the repo to define environment-specific deployment machinery.

## Publish

- When the requested work is complete and validation passes, stage the intended files, commit them, push the branch to `origin`, and open a ready-for-review pull request against `main` with `gh` unless the repo documents a different publish flow.
- Open draft pull requests only when explicitly requested.
