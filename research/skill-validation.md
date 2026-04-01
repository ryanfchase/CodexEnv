# Repo-Local Skill Validation

This file defines how to validate repo-local skills without turning every thin wrapper into a full end-to-end test project.

## Goals

- Keep validation proportional to the skill complexity.
- Require every repo-local skill to prove it still matches the repo docs.
- Reserve executable smoke checks for skills with real runtime or environment risk.

## Two-Tier Model

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
