# Codex Runtime Bootstrap

This file defines the shared runtime and auth assumptions that codexified environments should standardize before adding repo-local skills.

## Goals

- Prefer repo-local executables over global ones when available.
- Make GitHub auth predictable across machines.
- Reduce repeated sandbox/escalation friction.
- Give shared skills stable assumptions about Python, Node, git, and `gh`.

## Python Resolution Order

When a repo uses Python, prefer these entrypoints in order:

1. `.venv/bin/python`
2. `.venv/bin/python3`
3. `venv/bin/python`
4. `venv/bin/python3`
5. `python3`
6. `python`

Notes:

- Prefer repo-local virtualenv executables when present.
- Standardize on `.venv/` for new codexified repos when practical.
- If a repo already uses `venv/`, preserve the repo convention instead of forcing churn.

## Node and Frontend Resolution

- Prefer package-manager scripts over direct binary calls.
- Prefer local project tooling over global installs.
- Recommended order:
  - `npm run <script>`
  - local package manager equivalent already used by the repo
  - direct local binary only when the script layer is missing

## GitHub Auth

- Standard interactive bootstrap: `gh auth login`
- Standard validation check: `gh auth status`
- Prefer `gh` as the default GitHub write path for:
  - PR creation
  - PR updates
  - PR status checks
- When creating or editing PR descriptions with `gh`, prefer `--body-file` over inline shell body strings.
- Do not embed Markdown backticks inside inline shell `gh pr create --body "..."` or `gh pr edit --body "..."` commands.
- Use a quoted heredoc or temporary file for PR bodies so shell command substitution cannot inject command output into the description.
- Use the GitHub connector primarily for read workflows such as:
  - PR inspection
  - issue lookup
  - comment and review reads
- Open ready-for-review PRs by default.
- Open draft PRs only when the user explicitly asks for a draft or the repo documents a draft-first publish rule.
- If `gh auth status` fails, fix auth before attempting PR or review operations.

## Escalation Expectations

Agents should expect escalation or external approval more often for:

- git writes when the sandbox blocks `.git` lock creation
- networked operations such as pushing, fetching, dependency installs, or API calls
- Docker operations
- writes outside the writable workspace root

## Shared Skill Dependency Contract

Shared foundation skills may assume:

- the repo has a local manifest in `codex-template.json`
- runtime conventions are documented in `runtime-bootstrap.md`
- command inventories capture repo-local commands

Shared foundation skills should not assume:

- a specific Python package manager
- a specific Node package manager beyond the repo's documented choice
- that sandbox escalation has already been granted
