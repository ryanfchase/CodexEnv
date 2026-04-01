# AGENTS.md

Instructions in this workspace apply to the CodexEnv template repository.

## Workspace

- This directory is a template workspace, not a production repository.
- This directory should also be maintained as the canonical upstream git repository for the Codex template system.
- Use it to capture reusable agent-assisted development patterns before copying them into new workspaces.
- Keep the template focused on verification-first workflows, repo boundaries, and repeatable commands.
- Treat `codex-template.json` as the standard manifest filename for any codexified repo or integration workspace.

## First Step

- Default to the single-repo template unless the task clearly involves sibling repositories.
- Identify whether the task belongs to the single-repo template or the integration-workspace template.
- Read the local `codex-template.json` manifest when present to determine template type, version, and drift state.
- Check the most recent session summary in `.codex-sessions/` before making assumptions about current standardization state.
- Read the research notes in `research/verification-first-patterns.md` before making assumptions about workflow shape.
- Read `research/runtime-bootstrap.md` before standardizing environment or auth behavior.
- Read `research/skill-model.md` before adding or changing skills.
- Read `research/template-versioning.md` before changing the versioning model.
- If you are extending a template, update the matching template `AGENTS.md` first, then the supporting docs.

## Scope

- This workspace is for documentation and standardization only.
- Prefer concise, reusable language over repo-specific implementation detail.
- The integration-workspace template should inherit the single-repo rules and add only the cross-repo coordination that is actually needed.
- When a meaningful milestone is reached, add or update a local session summary in `.codex-sessions/`.
- Version `single-repo` and `integration-workspace` separately using semantic versions.
- Shared foundation skills belong under `skills/shared/`; repo-local skills should be derived from command inventories rather than invented ad hoc.
