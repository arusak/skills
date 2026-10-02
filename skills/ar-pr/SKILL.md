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
- Compare the net `base...HEAD` changes, including commits, changed files, and material diff hunks. If output is truncated, inspect material hunks in smaller batches until covered.
- Before drafting, make a short inventory of user-facing behavior, state changes, and significant restructuring in that net diff.
- Read repository documents to better understand the reasons for the changes.
- Stop if the branch already has an open PR; never create a duplicate. Surface this to the user.

## Build the PR

- Identify the PR's primary purpose from the inventory and derive the title and body from it. The first or last commit, branch name, or a file move cannot stand in for the full diff.
- Check that the title and every body bullet accurately reflect that purpose and the net changes.
- The title should use a conventional commit format with a prefix containing the task number (if you know it or can derive it from the branch name) or a feature name.
- Keep the title imperative, specific, and aligned with repository conventions.
- Use dashes as bullets.
- Never use emoji.
- Explain significant behavioral or architectural changes and why they were made.
- Don't list the checks performed.
- Mention issue links or dependency ordering when supported by repository evidence.
- For multiple repositories, inspect and create each PR independently; cross-link related PRs.
- Don't add meaningless text such as a generic preamble or signature. Every sentence should be related to code changes.

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
- Let the user confirm the full title and body before publishing.
- Do not commit, push, add reviewers, labels, or assignees unless requested or required by repository instructions.

## Verify

- Query the PR after creation or update.
- Confirm the repository, URL, base, head, title, state, and rendered body.
- Report the PR URL and any omitted or blocked actions concisely.
