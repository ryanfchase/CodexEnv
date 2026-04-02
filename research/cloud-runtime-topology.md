# Cloud Runtime Topology

This file defines the default cloud-runtime and container-registry model for codexified integration environments.

## Goals

- Keep local orchestration, cloud deployment, and app runtime ownership separate.
- Avoid forcing Docker publication onto repos that do not need a container runtime.
- Give integration environments one clear default for AWS-hosted container workloads.
- Keep registry and runtime decisions explicit in the manifest and assessment.

## Default Platform Model

Use a hybrid platform model for integration environments that span multiple repos.

- Long-running backend services:
  - default cloud runtime target: `aws-ecs-fargate`
  - default deploy registry: `aws-ecr`
- Static frontends:
  - default cloud runtime target: `static-hosting`
  - no container registry required unless the repo explicitly chooses containerized frontend delivery
- Special-purpose AWS container workloads such as Lambda container images:
  - allowed as repo-specific exceptions
  - still publish to `aws-ecr`

## Ownership Split

- App repos own:
  - image definitions when the app is containerized
  - application runtime contract
  - service-level verification
  - local-versus-cloud guardrails
- Integration environment repos own:
  - checked-in multi-repo local orchestration
  - cloud runtime topology
  - registry strategy
  - secret and config injection contracts
- Parent integration workspaces own:
  - repo routing
  - cross-repo assessment
  - visibility into which repo owns each contract

## Registry Standard

For AWS-managed container deployments, prefer `aws-ecr` as the authoritative deploy registry.

Reasons:

- AWS runtimes integrate directly with ECR.
- GitHub Actions can publish to ECR cleanly with AWS OIDC.
- This avoids adding GHCR pull credentials to AWS runtime paths.

Use one ECR repository per deployable containerized app.

Recommended tag shape:

- immutable commit tag: `sha-<git-sha>`
- moving integration tag: `edge`
- optional release tags when a repo adopts release/version semantics

## Runtime Classes

### Long-Running Service

Use for APIs or workers that should stay available continuously.

- target: `aws-ecs-fargate`
- registry: `aws-ecr`
- examples:
  - FastAPI backends
  - Node or Python APIs
  - background workers packaged as services

### Static Frontend

Use for Vite, React, or other frontend apps that compile to static assets.

- target: `static-hosting`
- registry: none by default
- examples:
  - S3 + CloudFront
  - GitHub Pages for preview or public docs

### Lambda Container Exception

Use only when the repo already has a strong Lambda-shaped runtime.

- target: `aws-lambda-container`
- registry: `aws-ecr`
- note: this is a repo-specific exception, not the default integration-environment target

## Local Development Mapping

The integration environment should expose a checked-in local entrypoint that maps cleanly to the cloud topology without pretending local and cloud are identical.

Recommended local composition:

- shared local infra:
  - Mongo
  - LocalStack when S3-style flows are needed
- backend services:
  - run from sibling app repos in containers or repo-native dev modes
- frontend apps:
  - run from containers only when the repo supports that cleanly
  - otherwise document host-run startup alongside the shared local stack

Local compose is for reproducible developer orchestration, not for modeling production deployment one-to-one.

## Secret and Config Rules

- App repos declare required runtime variables.
- Integration environment repos declare where those values come from in:
  - local development
  - cloud deployment
- Never check in real secrets.
- For AWS-hosted cloud runtimes, prefer:
  - SSM Parameter Store
  - Secrets Manager
  - IAM roles or OIDC for cloud auth

## Practical Rule

If a repo deploys into AWS and needs a private container image, default to `aws-ecr`.

If a repo is a static frontend, do not force it into a container registry just to satisfy template symmetry.

If a repo already has a Lambda container shape, keep that as an explicit exception rather than pretending every service should converge immediately to the same runtime.
