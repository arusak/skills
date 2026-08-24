---
name: ar-implement
description: "Implement a piece of work based on a spec or plan."
disable-model-invocation: true
---

Implement the work described by the user in the spec.

If the spec is split by phases, use subagents to implement each phase. You may also want subagents for tasks such as exploration, running tests or code review. Be wise about spawning agents, choose context carefully, feel free to run them in parallel if that sounds reasonable.

If the spec doesn't have explicit phases, split the work into phases yourself first. If unsure in that phase split, ask me for approval. After each phase report estimated amount of remaining jobs and effort as a proportion: "Finished 5 of 12 tasks, about 30% done".

Use the "tdd" skill where possible and reasonable, at pre-agreed seams.

Run typechecking and tests for involved files after each phase.

Run full test suite and lint once at the end.

Once done, use /code-review to review the work.

Commit your work to the current branch.

Create a report file named similarly to spec or plan. Report briefly to chat about what you did and how you used subagents. Chat in Russian, files in English.
