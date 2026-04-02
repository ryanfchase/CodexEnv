# Operational Readiness

This file defines how to tell whether a codexified repo or workspace is merely documented, or actually ready to function as an agent toolkit.

## Goals

- Make it easy for humans and agents to answer "how codexified is this?"
- Promote environments to `operational` only when there is real evidence, not just completed paperwork.
- Keep the feedback signal compact enough to live in the manifest, with optional narrative detail in `codex-assessment.md`.
- Keep codexification bounded so `operational` means "usable and publishable" rather than "fully deployed."

## Readiness States

Use `operational_readiness` in the manifest to summarize current execution readiness.

- `missing`: the environment does not yet have enough Codex structure to assess readiness meaningfully.
- `partial`: the environment is codexified and partly validated, but still lacks evidence for operational use.
- `passing`: the environment has enough evidence to be treated as operational for normal repo work.
- `blocked`: the environment would otherwise be ready, but a known blocker prevents the expected workflow from running.

## Assessment Checks

Use `assessment_checks` in the manifest as the built-in feedback loop.

Recommended checks:

- `readme_status_surface`
- `manifest_current`
- `docs_current`
- `command_inventory_grounded`
- `verification_path_defined`
- `verification_path_validated`
- `github_actions_verification`
- `integration_orchestration_defined`
- `integration_orchestration_validated`
- `cloud_runtime_defined`
- `registry_strategy_defined`
- `shared_skill_coverage`
- `repo_local_skill_coverage`
- `publish_flow_current`
- `operational_smoke`
- `container_publish_verification` for repos that opt into container-image publishing

Recommended values:

- `pass`
- `partial`
- `missing`
- `deferred`
- `blocked`

## Promotion Guidance

### Standardized

The environment may be `standardized` when:

- the README status surface exists
- the manifest is current
- the repo docs match reality
- the command inventory is grounded in real commands
- the publish flow is current

### Operational

The environment may be promoted to `operational` when:

- `readme_status_surface`: `pass`
- `manifest_current`: `pass`
- `docs_current`: `pass`
- `command_inventory_grounded`: `pass`
- `verification_path_defined`: `pass`
- `verification_path_validated`: `pass`
- `github_actions_verification`: `pass` when the repo uses GitHub and exposes a native verification command that should be enforced on change
- `shared_skill_coverage`: `pass`
- `publish_flow_current`: `pass`
- `operational_smoke`: `pass` or a repo-specific equivalent is explicitly recorded

`repo_local_skill_coverage` does not have to be `pass` for every repo type. It may be `deferred` when the current template line explicitly allows a repo to stay operational with shared skills plus documented commands.

`github_actions_verification` may be `deferred` only when the repo is not expected to use GitHub Actions or when there is a documented alternative CI system that enforces the same verification path.

`integration_orchestration_defined`, `integration_orchestration_validated`, `cloud_runtime_defined`, and `registry_strategy_defined` are most useful for integration-workspace templates or versioned environment repos. They may be omitted or `deferred` in ordinary single-repo app repos.
`container_publish_verification` is optional. It should be present only when a repo explicitly declares a container-image build or publish capability.

Operational promotion should stop at the repo or workspace boundary:

- app repos should prove that the runtime contract is explicit and the artifact is verifiable and publishable
- environment repos should prove that local orchestration and artifact-consumption contracts are explicit
- full deployment implementation is optional and should be tracked as an environment-specific extension rather than a base codexification requirement

When present, use:

- `missing`: the repo claims container publishing support but does not yet document a usable path
- `deferred`: container publishing is planned but not yet standardized
- `partial`: the build or push path is documented locally, but not yet enforced in CI
- `pass`: a documented GitHub Actions workflow owns the intended image build or push path
- `blocked`: the repo intends to publish images, but auth, registry, or workflow blockers prevent the path from being usable

## Evidence Recording

Use `codex-assessment.md` for the human-readable narrative:

- current classification
- why the current stage is justified
- the latest validation evidence
- blockers or warnings
- the next promotion gate

Use `codex-template.json` for the machine-readable summary:

- `next_stage_target`
- `operational_readiness`
- `assessment_checks`

Use the repo `README.md` for the thin human-facing dashboard:

- current codexification stage
- current readiness state
- compact visual stage path
- remaining work for the next promotion
- currently available toolkit surface

## Practical Rule

If an agent or human cannot tell whether the repo's documented verification path actually ran recently, the environment is not operational yet.

If an agent or human cannot tell whether the repo's documented artifact can be consumed by its owning environment, the repo may be standardized but is not fully operational for publishable workflows.

If an agent or human cannot scan the `README.md` and quickly understand the current stage, remaining work, and available toolkit, the environment is missing an important feedback surface.

If the `README.md` status surface starts to compete with the repo's main project description or setup docs, move detail back into `codex-assessment.md` and keep only the compact status card in the README.
