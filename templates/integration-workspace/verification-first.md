# Integration-Workspace Verification-First Ladder

## Fill These In Per Child Repo

- repo name:
- owning team or role:
- default branch:
- local dev entrypoint:
- lint command:
- targeted tests:
- full suite:
- smoke or compose verification:

## Suggested Order

1. Determine which repo owns the requested change.
2. Read the child repo instructions.
3. Inspect the contract boundary in both repos if the change crosses repos.
4. Run the fastest meaningful check in the owning repo.
5. Run dependent repo checks if the contract shape changes.
6. Run compose or smoke checks if the workspace supports them.
7. Publish only after both sides are verified.

## Notes

- Treat cross-repo contract changes as higher risk than isolated implementation changes.
- Keep any workspace-level notes about ports, environment files, and service startup commands close to the command inventory.

