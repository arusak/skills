---
name: ar-pr
description: Create or update accurate GitHub pull requests for pushed branches with concise titles, brief bullets, significant changes, and reasoning. Use when the user asks to create, open, draft, or update a PR, including across multiple repositories.
---

# Create PR

## Preflight

- Read repository instructions.
- Identify the repository, current branch, upstream branch, and default base.
- Confirm the branch is pushed and is not the base branch.
- Inspect `git status`; never describe uncommitted changes as part of the PR.
- Compare `base...HEAD`, including commits, changed files, and material diff hunks.
- Stop if the branch already has an open PR; never create a duplicate. Surface this to the user.
## Build the PR

- Derive the title and body from the pushed diff, not conversation claims.
- Title should use a conventional commit format with a prefix containing the task number (if you know it or can borrow it from the branch name) or a feature name.
- Keep the title imperative, specific, and aligned with repository conventions.
- Use brief bullets and no emoji.
- Explain significant behavioral or architectural changes and why they were made.
- Mention issue links or dependency ordering when supported by repository evidence.
- For multiple repositories, inspect and create each PR independently; cross-link related PRs.

Use this body shape unless the repository template requires another:

```markdown
<outcome>

💡<change> — <reason>
```

## Create safely

- Write the body to a temporary Markdown file; use `gh pr create --body-file` or `gh pr edit --body-file`.
- Avoid interpolated shell strings for Markdown containing backticks, dollar signs, or substitutions.
- Supply `--base` and `--head` explicitly when ambiguity is possible.
- Create a draft only when requested or when repository guidance requires it.
- Do not commit, push, add reviewers, labels, or assignees unless requested or required by repository instructions.

## Verify

- Query the PR after creation or update.
- Confirm repository, URL, base, head, title, state, and rendered body.
- Report the PR URL and any omitted or blocked action concisely.
