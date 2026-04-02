# CodexEnv Template Workspace

This directory is a staging area for reusable agent-assisted project templates and shared agent-toolkit conventions.

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
- `research/cloud-runtime-topology.md` defines the default cloud-runtime and registry model for integration environments.
- `research/skill-model.md` defines shared-vs-local skill boundaries and metadata.
- `research/skill-validation.md` defines the static-versus-smoke validation standard for repo-local skills.
- `research/codexification-assessment.md` defines lifecycle stages, conformity review, and template access modes.
- `research/operational-readiness.md` defines the scorecard and evidence needed to promote a codexified environment from standardized to operational.
- `research/container-publish-capability.md` defines the optional container-image build and publish capability for repos that actually ship images.
- `research/cloud-runtime-topology.md` defines the ownership split between app repos, environment repos, and any later deployment implementation.
- `skills/shared/` contains the first shared skill set for codexified environments.
- `templates/single-repo/` standardizes the workflow for one repo owned end-to-end.
- `templates/integration-workspace/` standardizes the workflow for a parent workspace that coordinates sibling repos.

## Intended Use

Use these files as the starting point for future project work, then add repo-specific commands, ownership notes, validation gates, codexification assessment data, and operational-readiness evidence as each new workspace is introduced.

The default stopping point is "verifiable and publishable," not "fully deployed." Environment-specific deployment remains optional unless the owning integration repo explicitly takes it on.

`CodexEnv` is intended to be the canonical upstream git repository for this template system.

The intended sequence is:

1. Reuse the single-repo template for a new repo.
2. Add a local `codex-template.json` manifest so the environment advertises its template type, version, stage, conformity, drift, and readiness state.
3. Apply the shared runtime/bootstrap conventions and shared skill foundation.
4. Copy the relevant commands from the catalog into that repo's command inventory and derive repo-local skills from it.
5. Add optional capabilities such as container publishing only when the repo's real workflow needs them.
6. Derive an integration-workspace template only when the work truly spans sibling repos.

When possible, use a local `CodexEnv` checkout as the template source. If no local checkout exists, the GitHub repo is the supported fallback source for codexification and conformity work.
