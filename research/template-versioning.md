# Codex Template Versioning

This file defines how codexified repos and integration workspaces identify their Codex template lineage.

## Goals

- Let an agent determine which Codex template an environment uses.
- Let an agent determine which internal template version is applied locally.
- Distinguish intentional local overrides from stale divergence.
- Make upgrades back to the base `CodexEnv` template predictable.
- Keep local session history separate from portable template state.

## Standard Manifest

Every codexified environment should keep a local `codex-template.json` at its root.

That manifest is the operative source of truth for:

- template type
- template version
- codexification stage
- conformity status
- template source
- template access mode
- template access reference
- applied date
- last reviewed date
- last conformity reviewed date
- drift status
- explicit local overrides
- notes

Local working memory such as checkpoint summaries should live under `.codex-sessions/` and remain untracked.

## Template Lines

Use separate semantic version lines for the two template types:

- `single-repo`
- `integration-workspace`

Current starting versions:

- `single-repo@1.2.0`
- `integration-workspace@1.2.0`

## Codexification Stages

- `discovered`: the repo or workspace is known, but Codex artifacts are not in place yet.
- `scaffolded`: the core Codex files exist, but they are incomplete, unreviewed, or not yet aligned to the current template.
- `standardized`: the Codex docs and manifest align with the current template line and the command inventory is grounded in real repo commands.
- `operational`: the environment is standardized and the intended skill coverage for that repo or workspace is in place.
- `maintained`: the environment is operational and has been reviewed forward to the current template line.

## Conformity States

- `conforming`: the environment matches the current CodexEnv standard closely enough to use without special remediation.
- `partial`: the environment is codexified, but required current template behaviors or metadata are still missing.
- `nonconforming`: the environment has Codex artifacts, but they diverge materially from the standard and should be repaired before being treated as current.

## Drift States

- `clean`: local environment matches the base template except for allowed repo-local content.
- `overrides`: local environment intentionally differs from the base template in listed ways.
- `stale`: local environment is behind the current base template and should be reviewed for upgrade.

## Template Access Modes

- `local-checkout`: a local CodexEnv checkout is available and should be used as the primary source.
- `remote-reference`: no local checkout is available, so the GitHub repository or tagged release is the fallback source.

## Upgrade Workflow

1. Read local `codex-template.json`.
2. Compare `template_version` against the current version in the available `CodexEnv` source.
3. Review the relevant template changes in local `.codex-sessions/` when a local checkout exists, or use the Git history and release notes when working from a remote reference.
4. Assess the environment for:
   - codexification stage
   - conformity status
   - drift status
5. Apply the desired template updates.
6. Update the local manifest:
   - `template_version`
   - `codexification_stage`
   - `conformity_status`
   - `last_reviewed_at`
   - `last_conformity_reviewed_at`
   - `drift_status`
   - `local_overrides`
   - `notes`

## Manifest Shape

Recommended fields:

- `template_type`
- `template_version`
- `codexification_stage`
- `conformity_status`
- `template_source`
- `template_access_mode`
- `template_access_reference`
- `runtime_contract_version`
- `shared_skill_set_version`
- `applied_at`
- `last_reviewed_at`
- `last_conformity_reviewed_at`
- `drift_status`
- `local_overrides`
- `notes`

## Source of Truth

- `CodexEnv` is the maintainer workspace for template evolution.
- `CodexEnv` should be maintained as the canonical upstream git repository for template releases and tags.
- Each codexified repo or workspace keeps its own local manifest with stage, conformity, and source-access data.
- Prefer a local CodexEnv checkout when one is available; otherwise use the GitHub repo as the fallback template source.
- Session summaries are the human-readable change log, not the machine-readable version identifier.
