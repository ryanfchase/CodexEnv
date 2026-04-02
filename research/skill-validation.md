# Skill Validation

This file defines how to validate shared and repo-local skills without turning every thin wrapper into a full end-to-end test project.

## Goals

- Keep validation proportional to the skill complexity.
- Require every skill to prove it still matches the docs it depends on.
- Reserve executable smoke checks for skills with real runtime or environment risk.

## Shared Skill Validation

### Contract validation

Required for every shared skill.

Check:

- the skill contract includes purpose, inputs, preconditions, outputs, and failure modes
- the workflow still matches the template docs it depends on
- the skill remains reusable across the declared template types

### Probe validation

Required when the skill selects or inspects a live environment state.

Typical triggers:

- Python entrypoint resolution
- GitHub auth inspection
- branch or PR state inspection
- default verification-path selection

Probe checks should stay harmless and minimal. They should verify dispatch or inspection logic, not full repo verification.

## Repo-Local Skill Validation

Use a two-tier model for repo-local skills.

### Static validation

Required for every repo-local skill.

Check:

- the skill exists in `skill-inventory.md`
- the skill command matches `command-inventory.md`
- the skill fits the repo `runtime-bootstrap.md`
- the skill output section matches the intended behavior

### Smoke validation

Required only for repo-local skills that start or attach to stateful systems.

Typical triggers:

- local API startup
- Docker stack startup and teardown
- service shell attachment
- database shell attachment

Smoke checks should be as small as possible and answer only:

- did the documented command path work?
- did the expected target become reachable?

## UserService Pilot Mapping

- `user-service-local-api`: `smoke`
- `user-service-pytest-targeted`: `static`
- `user-service-pytest-all`: `static`
- `user-service-docker-stack`: `smoke`
- `user-service-shell-inspect`: `smoke`

## Guidance

- Do not widen a repo-local skill smoke check into full repo verification unless the skill itself owns that broader flow.
- Use the repo's existing verification-first ladder for broader validation after the skill check passes.
