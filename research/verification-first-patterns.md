# Verification-First Patterns Observed in Reference Environments

This note captures the reusable workflow patterns that show up across the current workspaces.

## Template Direction

- Standardize the single-repo workflow first.
- Derive the integration-workspace workflow from the single-repo rules.
- Keep this phase docs-only so the command inventory is ready before skills are introduced.

## Shared Pattern

- Inspect the relevant code paths before editing.
- Check branch and pull request state before starting new work.
- Start from the latest `origin/main` before creating a task branch.
- Keep changes minimal and localized.
- Validate before responding.
- Commit, push, and open a PR only after validation passes.

## Workspace-Level Routing

### PROJECT1

- The parent workspace is not a git repository.
- The parent `AGENTS.md` routes work to the correct child repository first.
- Child repos have their own branch rules, validation commands, and repo-specific instructions.
- Multi-repo work is explicitly handled as a cross-repo change, not as a single shared repo.

### PROJECT2

- The parent workspace guidance is separate from the child repos.
- `ExampleBackend` treats the backend as a monorepo with a scraper/write path and a read API.
- `ExampleFrontend` treats the frontend as the product-facing app with its own local workflow and validation.
- Cross-repo changes require checking both sides before editing either repo.

## Command Sources For Standardization

Use these repo-specific commands as the seed material for future command inventories and skills.

- `PROJECT1/ExampleServer`: Python service with `nox`-driven lint, fast, all, integration, and export-focused sessions.
- `PROJECT1/ExampleViewer`: frontend app with lint, build, and Playwright e2e scripts.
- `PROJECT2/ExampleBackend`: backend service with `nox` lint/tests plus Docker Compose seed/test/smoke verification.
- `PROJECT2/ExampleFrontend`: frontend app with lint, tests, typecheck, build, and e2e scripts.

## Observed Validation Ladder

### Python service repos

- `python -m nox -s lint`
- `python -m nox -s tests`
- `python -m nox -s smoke_api` when the repo provides an API smoke session
- Docker-compose verification when the repo exposes seed/test/smoke services

### ExampleServer

- `nox -s fast`
- `nox -s all`
- `nox -s integration`
- `nox -s local-export-flow`
- `nox -s export-artifact -- /path/to/export.zip`

### ExampleBackend

- `python -m nox -s lint`
- `python -m nox -s tests`
- `docker compose -f compose.local.yml --env-file .env.local up --build -d db api`
- `docker compose -f compose.local.yml --env-file .env.local run --rm seed`
- `docker compose -f compose.local.yml --env-file .env.local run --rm tests`
- `docker compose -f compose.local.yml --env-file .env.local run --rm smoke`

### ExampleFrontend

- `npm run lint`
- `npm run test`
- `npm run typecheck`
- `npm run build`
- `npm run test:e2e -- <spec>`

## What To Standardize

- A single-repo template should define:
  - how to identify the repo owner
  - the local verification ladder
  - the branch and PR workflow
  - the command inventory for future skills
- An integration-workspace template should define:
  - how to identify the owning child repo
  - how to inspect both sides of a contract change
  - how to validate each touched repo independently
  - how to keep workspace-level coordination explicit
