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
- `changed_in`: `1.1.2`
- `depends_on`: `env-github-auth`, `git-branch-pr-status`

## Workflow

1. Confirm validation already passed.
2. Confirm branch state is correct for publishing.
3. Stage intended files only.
4. Create a logical commit.
5. Push the branch.
6. Open a ready-for-review PR with `gh` by default.
7. Open a draft PR only when the user explicitly requests one or the repo explicitly documents a draft-first publish flow.

## Output

Return:

- branch published or blocked
- commit and push status
- PR status or next required action
