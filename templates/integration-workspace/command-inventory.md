# Integration-Workspace Command Inventory

Populate this file from the child repos involved in the workspace, using `research/command-catalog.md` as the seed.

## Child Repo A

- start:
- lint:
- tests:
- smoke:
- branch checks:

## Child Repo B

- start:
- lint:
- tests:
- smoke:
- branch checks:

## Workspace-Level

- bring up shared services:
- seed test data:
- verify contract:
- teardown:

## Example Workspace Pattern

- backend-first validation when the API contract changes
- frontend verification when a payload or endpoint shape changes
- compose or smoke verification after the child repos are individually green
