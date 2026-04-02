---
name: git-repo-publish
description: Publish validated repo changes using the documented Codex git workflow. Use when a codexified repo needs to stage, commit, push, and open a PR consistently.
---

# Git Repo Publish

Skill metadata:

- `skill_id`: `git-repo-publish`
- `scope`: `shared`
- `template_types`: `single-repo`
- `introduced_in`: `1.1.0`
- `changed_in`: `1.6.1`
- `depends_on`: `env-github-auth`, `git-branch-pr-status`

## Workflow

1. Confirm validation already passed.
2. Confirm branch state is correct for publishing.
3. Stage intended files only.
4. Create a logical commit.
5. Push the branch.
6. Prepare the PR title and body in a file-safe form before publishing.
7. Use `gh pr create --body-file <path>` or `gh pr edit --body-file <path>` by default instead of inline shell body strings.
8. Open a ready-for-review PR with `gh` by default.
9. Open a draft PR only when the user explicitly requests one or the repo explicitly documents a draft-first publish flow.

## PR Body Safety

- Treat inline shell backticks in PR body arguments as unsafe because the shell may execute them as command substitution.
- Prefer a quoted heredoc or temporary markdown file for PR bodies.
- If the PR body needs command examples, keep them in the body file rather than interpolating them into the shell command itself.
- If a PR body is malformed after creation, correct it with `gh pr edit --body-file <path>`.

## Output

Return:

- branch published or blocked
- commit and push status
- PR status or next required action
