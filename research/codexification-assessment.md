# Codexification Assessment

This file defines how to assess whether a project is codexified, how far along it is, and whether it still conforms to the current CodexEnv standard.

## Goals

- Let an agent classify a repo or workspace quickly from the root manifest.
- Separate implementation progress from drift and intentional overrides.
- Make codexification upgrades repeatable across machines.
- Support both local CodexEnv checkouts and GitHub-based fallback access.

## Assessment Axes

Assess every codexified environment on three separate axes:

- `codexification_stage`
- `conformity_status`
- `drift_status`
- `operational_readiness`

Use `codexification_stage` to answer how far the environment has progressed.

- `discovered`
- `scaffolded`
- `standardized`
- `operational`
- `maintained`

Use `conformity_status` to answer how closely the environment matches the current CodexEnv standard.

- `conforming`
- `partial`
- `nonconforming`

Use `drift_status` to answer whether the environment is current or intentionally different.

- `clean`
- `overrides`
- `stale`

Use `operational_readiness` to answer whether the documented agent toolkit is actually ready for normal use.

- `missing`
- `partial`
- `passing`
- `blocked`

## Access Modes

Record how the template source was accessed.

- `local-checkout`: use the local CodexEnv checkout when present.
- `remote-reference`: use the GitHub repo URL or release tag when no local checkout is available.

The manifest should also record `template_access_reference` so an agent knows which local path or remote URL was used.

## Assessment Workflow

1. Read `codex-template.json` when present.
2. Determine:
   - template type
   - template version
   - codexification stage
   - conformity status
   - drift status
   - template access mode
3. Check for the expected Codex artifacts for that template line:
   - `README.md`
   - `AGENTS.md`
   - `codex-template.json`
   - `codex-assessment.md`
   - `runtime-bootstrap.md`
   - `verification-first.md`
   - `command-inventory.md`
   - `skill-inventory.md`
4. Compare those artifacts against the current CodexEnv template.
5. Record:
   - what is missing
   - what is stale
   - what is intentionally overridden
   - where checked-in integration orchestration lives when the environment spans multiple repos
   - which runtime class each major repo belongs to when cloud deployment is in scope
   - which optional capabilities are in scope for this repo or workspace
   - what evidence supports the current stage
6. Update the manifest after review.

## Stage Guidance

- `discovered`: no Codex artifacts yet.
- `scaffolded`: artifacts exist, but they are not yet aligned, current, or committed as the repo standard.
- `standardized`: the docs and manifest match the current template line and are grounded in real repo commands.
- `operational`: the repo or workspace is standardized and has the intended skill coverage in place.
- `maintained`: the environment is operational and kept current with template upgrades.

## Evidence Rule

Treat `standardized` as a documentation and alignment milestone.

Treat `operational` as an evidence milestone. The environment should not be promoted until there is a recorded readiness scorecard and at least one successful validation pass for the intended normal workflow.

Optional capabilities such as container-image publishing should be assessed separately from base codexification. A repo may be fully codexified without any container capability if its real workflow does not build or ship images.

## Practical Rule

Do not treat a repo as fully codexified just because `AGENTS.md` exists.

Treat it as current only when:

- the manifest is present and current
- the command inventory matches real commands
- the runtime and verification docs match reality
- the conformity review says the repo is usable against the current template line
