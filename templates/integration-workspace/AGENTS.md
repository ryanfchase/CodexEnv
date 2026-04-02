# AGENTS.md

Instructions in this template apply to a parent workspace that coordinates sibling repositories.

## Workspace

- Start from the single-repo template rules, then add only the sibling-repo coordination that the task requires.
- Add a root-level `codex-template.json` so the workspace advertises its template version, codexification stage, conformity status, and drift status.
- Add a root-level `codex-assessment.md` so the workspace records the evidence behind its current stage and readiness.
- Add a workspace-level `runtime-bootstrap.md` so shared skills can discover runtime and auth assumptions consistently.
- This workspace is a router, not a single source tree.
- Identify the child repository that owns the requested work before editing anything.
- Read the child repository's `AGENTS.md` before making assumptions about its workflow.
- If a change spans multiple repos, inspect both sides before editing either one.

## Workflow

- Inspect the relevant code paths before editing. Prefer `rg` for search.
- Keep changes minimal and localized to the requested behavior.
- Do not revert user changes you did not make.
- Use `apply_patch` for manual file edits.
- Before starting new work, check branch and PR state in each touched repo.
- If a repo's PR is merged, switch to `main`, pull the latest `origin/main`, and create a fresh `codex/<short-slug>` branch before making changes.
- Fetch `origin/main` before creating a new working branch in any touched repo.
- If the same change needs coordination across repos, keep the contract boundary explicit and validate each repo independently.

## Verification

- Use each child repo's own validation commands.
- Verify the changed repo first, then the dependent repo or contract partner.
- Keep a command inventory for each child repo so the workflow remains repeatable.
- Seed those inventories from `research/command-catalog.md`, then specialize them for each child repo and the workspace-level checks.
- Keep `skill-inventory.md` aligned with the shared foundation skills plus any workspace or child-repo skills derived from stable command inventory entries.
- Validate every workspace-local or child-repo-local skill statically, and add smoke validation only when the skill starts services, runs Docker, opens shells, or depends on process readiness.
- Update `codex-template.json` whenever the workspace is brought forward to a newer template version, when its codexification stage changes, when readiness evidence changes materially, or when local overrides change materially.
- Update `codex-assessment.md` whenever the readiness scorecard, latest evidence, or next promotion target changes.
- Treat container publishing as an opt-in capability for the child repos that actually build or ship images, not as a workspace-wide default.
- When a child repo publishes images, keep the container build or push path aligned with its documented verification path and the owning GitHub Actions workflow.

## Publish

- After validation passes in every touched repo, stage the intended changes, commit them, push the branch or branches to `origin`, and open the relevant ready-for-review pull request or pull requests against `main` with `gh` unless a repo documents a different publish flow.
- Open draft pull requests only when explicitly requested.
