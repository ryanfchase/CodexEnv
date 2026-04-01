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
- template source
- applied date
- last reviewed date
- drift status
- explicit local overrides
- notes

Local working memory such as checkpoint summaries should live under `.codex-sessions/` and remain untracked.

## Template Lines

Use separate semantic version lines for the two template types:

- `single-repo`
- `integration-workspace`

Current starting versions:

- `single-repo@1.1.0`
- `integration-workspace@1.1.0`

## Drift States

- `clean`: local environment matches the base template except for allowed repo-local content.
- `overrides`: local environment intentionally differs from the base template in listed ways.
- `stale`: local environment is behind the current base template and should be reviewed for upgrade.

## Upgrade Workflow

1. Read local `codex-template.json`.
2. Compare `template_version` against the current version in the `CodexEnv` template workspace.
3. Review `CodexEnv/.codex-sessions/` for the relevant template changes.
4. Apply the desired template updates.
5. Update the local manifest:
   - `template_version`
   - `last_reviewed_at`
   - `drift_status`
   - `local_overrides`
   - `notes`

## Manifest Shape

Recommended fields:

- `template_type`
- `template_version`
- `template_source`
- `runtime_contract_version`
- `shared_skill_set_version`
- `applied_at`
- `last_reviewed_at`
- `drift_status`
- `local_overrides`
- `notes`

## Source of Truth

- `CodexEnv` is the maintainer workspace for template evolution.
- `CodexEnv` should be maintained as the canonical upstream git repository for template releases and tags.
- Each codexified repo or workspace keeps its own local manifest.
- Session summaries are the human-readable change log, not the machine-readable version identifier.
