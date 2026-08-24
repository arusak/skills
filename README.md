# AR favorite skills

This is a personal collection of agentic skills. They should be used together with the superb skill set by Matt Pocock.

These skills partially override Matt's; they are also designed for the specific process I use in my projects.

And yeah, they speak Russian.

## Installation

Install these skills in each target repository. They extend Matt Pocock's skills, so install and configure Matt's set first. The commands below install editable project-local copies; run them from the repository where you want to use the skills.

```bash
npx skills@latest add mattpocock/skills --skill '*' --agent codex|claude-code|whatever-you-use
npx skills@latest add arusak/skills --skill '*' --agent codex|claude-code|whatever-you-use
```

Then run `/setup-matt-pocock-skills` in your agentic harness once for that repository.

To install the skills globally instead, add `--global` to each command. Use `--copy` if your environment does not support symlinks.

## Skills

| Skill            | Use it for                                                                                           |
| ---------------- | ---------------------------------------------------------------------------------------------------- |
| `$ar-feat-plan`  | Turning a new capability or significant behavior change into an approved, implementation-ready plan. |
| `$ar-fix-plan`   | Investigating a bug and preparing an evidence-based fix plan.                                        |
| `$ar-grilling`   | Stress-testing a plan, decision, or idea through a structured interview.                             |
| `$ar-implement`  | Implementing an approved specification or plan, with phased verification and review.                 |
| `$ar-phase-plan` | Planning the next phase of an existing design through the feature-planning workflow.                 |
| `$ar-pr`         | Creating or updating an accurate GitHub pull request for a pushed branch.                            |
