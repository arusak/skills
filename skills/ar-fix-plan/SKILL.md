---
name: ar-fix-plan
description: Create an approved, implementation-ready bug-fix plan grounded in the current repository.
---

# Fix Plan

Create an approved, implementation-ready bug-fix plan grounded in the current repository.

## Contract

- Work plan-only: investigate read-only and create only the approved plan file. Do not change code, tests, dependencies, generated files, configuration, git state, or external systems.
- Preserve unrelated worktree changes. Do not stage or commit unless asked.
- If the user switches to implementation, stop and confirm the new scope before editing application files.

## Supporting skills

Read and apply:

- `diagnosing-bugs` for investigation;
- `ar-grilling` for the decision interview;
- `codebase-design` when ownership, interface, seam, or adapter design matters.

No productive files should change during this session. If you need to create tests for red loop, they must be removed afterwards. If you need to change productive files to check a hypothesis, make sure to revert those changes.

## Workflow

1. **Scope.** If no bug is supplied, ask for it. Otherwise identify each user-visible symptom and affected repository/workflow. Read applicable repository instructions, feature docs, ADRs, prior decisions, plan conventions, and git status.
2. **Diagnose.** Apply `diagnosing-bugs` within the contract above. Before the interview, report current flow, evidence, hypotheses with confidence, current and proposed ownership, feedback-loop gaps, and open decisions. Keep facts, hypotheses, and recommendations distinct; a green baseline is not bug reproduction.
3. **Decide.** Delegate interview language, batching, recommendations, and fact-versus-decision handling to `ar-grilling`. Use `codebase-design` where applicable. Summarize the resulting behavior and architecture, then wait for explicit authorization to create the file. "Create it", "go", and equivalent imperatives count.
4. **Write.** Follow the repository's feature-local convention. Otherwise use `docs/plans/YYYY-MM-DD-<concise-scope>-plan.md`. Use the current date and never overwrite without permission.
5. **Validate.** Check the file and its structure, then confirm it is the only change introduced by this workflow. Do not run application suites merely to validate Markdown unless repository instructions require it.

## Plan contract

Give another engineer enough context to implement without rediscovery:

- metadata: title, date, `Ready for implementation`, scope, and non-goals;
- acceptance contract: outcome for every symptom, lifecycle and edge-case semantics, and behavior that must remain unchanged;
- diagnosis: current flow and owners, evidence versus hypotheses, confidence, unknowns, and why existing coverage misses the bugs;
- design: confirmed decisions, state lifetime, invariants, interfaces, and seams;
- execution: ordered file-by-file changes with paths, symbols, responsibilities, interface effects, and documentation/generated-code implications;
- verification: red-first coverage for every symptom, adjacent safeguards, exact commands, and separate manual/browser/full-stack gates;
- risks and binary completion criteria, including honest full-suite and operational-gate status.

Prefer durable paths and symbols over line numbers. Start execution with the regression test, then ownership/interface correction, behavior, necessary caller integration, and cleanup/documentation. Reject vague steps, unsupported verification claims, unjustified interface growth, or missing lifecycle cases.

Hand off with the plan link, central design decision, validation performed, confirmation that production code was untouched, and the file's git state. Do not repeat the plan in chat.
