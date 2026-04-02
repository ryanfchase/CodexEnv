# Container Publish Capability

This file defines how CodexEnv should model container-image build and publish workflows.

## Goals

- Keep Docker and registry workflows available for repos that need them.
- Avoid forcing containerization onto repos that do not build or ship images.
- Make image build or publish checks visible to both humans and agents.
- Keep the first standard aligned to GitHub Actions rather than heavy local automation.

## Scope

Treat container publishing as an optional capability, not a base codexification requirement.

Use it only for repos or workspaces that explicitly build, tag, or publish images to a registry.

Do not treat frontend or static repos as nonconforming just because they have no Dockerfile, no image registry, or no container push workflow.

## Capability Levels

- `none`: the repo does not use container workflows
- `local-dev-only`: the repo uses Docker or compose for local verification, but does not publish images
- `build-only`: the repo builds images, but does not publish them as part of the standard workflow
- `publish`: the repo builds and publishes images to a registry

## Manifest Fields

Record these fields only when a repo or workspace opts into the capability:

- `container_strategy`
- `container_registry`

Suggested values:

- `container_strategy`: `none | local-dev-only | build-only | publish`
- `container_registry`: free-form repo-local identifier such as `ghcr.io/org/repo` or `ecr/account/region/repo`

## Readiness Check

Use `assessment_checks.container_publish_verification` only when the repo claims a container-image build or publish path.

Recommended values:

- `missing`
- `deferred`
- `partial`
- `pass`
- `blocked`

Interpretation:

- `missing`: the repo claims container publishing support but does not document a usable path
- `deferred`: container publishing is planned but not yet standardized
- `partial`: the build or push path is documented locally, but not enforced in CI
- `pass`: a documented GitHub Actions workflow owns the intended image build or push path
- `blocked`: the repo intends to publish images, but auth, registry, or workflow blockers prevent the path from being usable

## Standard v1 Expectation

The first CodexEnv standard for this capability is CI-owned verification:

- document how the image is built
- document which workflow owns the build or push path
- keep the workflow aligned with the repo's documented verification path
- treat GitHub Actions as the default enforcement point

Do not require a local `docker login`, `docker build`, `docker tag`, or `docker push` script in v1.

## Practical Rule

Container publishing should be modeled as a repo capability, not as a universal property of backend work.

If a repo only uses compose for local verification, keep that under normal verification and do not imply it also publishes images.
