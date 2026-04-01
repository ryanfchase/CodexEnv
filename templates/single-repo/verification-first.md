# Single-Repo Verification-First Ladder

## Fill These In Per Repo

- default branch:
- local dev entrypoint:
- lint command:
- targeted test command:
- full test command:
- smoke or e2e command:
- local ports:
- compose workflow:

## Suggested Order

1. Inspect the changed code path.
2. Run formatting or lint checks.
3. Run targeted tests for the touched area.
4. Run the broader suite if the change crosses module boundaries.
5. Run smoke or e2e checks if the repo has a runnable service or UI.
6. Commit only after the verification result is acceptable.

## Notes

- Prefer the narrowest command that proves the changed behavior.
- If a command fails because the environment is missing prerequisites, document that before widening the scope.

