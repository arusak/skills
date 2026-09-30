# AR favorite skills

This is a personal collection of agentic skills. They should be used together with the superb skill set by Matt Pocock.

These skills partially override Matt's; they are also designed for the specific process I use in my projects.

## Installation

These skills extend Matt Pocock's skills, so install Matt's set first. The examples target Codex; replace `codex` with `claude-code` or another supported agent, or pass multiple names with `--agent codex claude-code`.

### Project installation

Run these commands from the repository where you want to use the skills:

```bash
npx skills@latest add mattpocock/skills --skill '*' --agent codex
npx skills@latest add arusak/skills --skill '*' --agent codex
```

Then run `/setup-matt-pocock-skills` in your agentic harness once for that repository.

### Global installation

Run these commands from any directory to make the skills available across all your repositories:

```bash
npx skills@latest add mattpocock/skills --skill '*' --agent codex --global
npx skills@latest add arusak/skills --skill '*' --agent codex --global
```

For either installation scope, use `--copy` if your environment does not support symlinks. See the [skills CLI documentation](https://github.com/vercel-labs/skills#options) for available options.

## Skills

| Skill                  | Use it for                                                                                           |
| ---------------------- | ---------------------------------------------------------------------------------------------------- |
| `$ar-feat-plan`        | Turning a new capability or significant behavior change into an approved, implementation-ready plan. |
| `$ar-fix-plan`         | Investigating a bug and preparing an evidence-based fix plan.                                        |
| `$ar-grilling`         | Stress-testing a plan, decision, or idea through a structured interview.                             |
| `$ar-implement`        | Implementing an approved specification or plan, with phased verification and review.                 |
| `$ar-npm-publish`      | Versioning, validating, tagging, and safely publishing an npm package.                               |
| `$ar-phase-plan`       | Planning the next phase of an existing design through the feature-planning workflow.                 |
| `$ar-pr`               | Creating or updating an accurate GitHub pull request for a pushed branch.                            |
| `$ar-review-leftovers` | Checking a branch for debug residue, bypassed checks, configuration drift, and unintended changes.   |
| `$ar-tailwind-format`  | Formatting and grouping Tailwind classes in React components while preserving behavior.              |
