# CodexEnv Template Workspace

This directory is a staging area for reusable agent-assisted project templates.

## Order

- `templates/single-repo/` is the primary template.
- `templates/integration-workspace/` is derived from the single-repo rules and adds sibling-repo coordination.
- `research/` captures the source material and command examples that will later feed skills.

## Contents

- `.codex-sessions/` stores local checkpoint summaries for the template-standardization work and stays out of git.
- `research/verification-first-patterns.md` captures the workflow patterns already present in the reference environments.
- `research/command-catalog.md` seeds the repeatable command inventory.
- `research/template-versioning.md` defines the manifest, version, drift, and upgrade model.
- `research/runtime-bootstrap.md` defines shared environment, auth, and escalation conventions.
- `research/skill-model.md` defines shared-vs-local skill boundaries and metadata.
- `skills/shared/` contains the first shared skill set for codexified environments.
- `templates/single-repo/` standardizes the workflow for one repo owned end-to-end.
- `templates/integration-workspace/` standardizes the workflow for a parent workspace that coordinates sibling repos.

## Intended Use

Use these files as the starting point for future project work, then add repo-specific commands, ownership notes, and validation gates as each new workspace is introduced.

`CodexEnv` is intended to be the canonical upstream git repository for this template system.

The intended sequence is:

1. Reuse the single-repo template for a new repo.
2. Add a local `codex-template.json` manifest so the environment advertises its template type, version, and drift state.
3. Apply the shared runtime/bootstrap conventions and shared skill foundation.
4. Copy the relevant commands from the catalog into that repo's command inventory and derive repo-local skills from it.
5. Derive an integration-workspace template only when the work truly spans sibling repos.
