---
name: ar-implement
description: "Implement a piece of work based on a spec or plan."
disable-model-invocation: true
---

Implement the work described by the user in the spec.

If the spec is split into phases, use subagents to implement each phase. You may also want to use subagents for tasks such as exploration, running tests, or code review. Be thoughtful about spawning agents, choose their context carefully, and feel free to run them in parallel if that seems reasonable.

If the spec doesn't have explicit phases, split the work into phases yourself first. If you're unsure about the phase split, ask me for approval. After each phase, report the estimated amount of remaining work and overall progress as a proportion: "Finished 5 of 12 tasks, about 30% done." Completion percentage should be evaluation of time left, not a fraction of executed tasks.

Use the "tdd" skill where possible and reasonable, at pre-agreed seams.

Run type checking and focused tests for the affected files after each phase.

## Final check and report

Prefer using a subagent for the final check. Run the full test suite and lint once at the end. Once done, run a suitable code review skill.

Create a report file with a name similar to that of the spec or plan. Write a brief report in chat. Put the report file in a dedicated project directory, or propose creating one.

The report should follow this template:

1. What was the task? (briefly)
2. What was your analysis?
3. What changes were made?

Don't report successful checks unless a long-standing issue came up during them.

Commit your work to the current branch, including the report and the spec file if it hasn't been committed yet.
