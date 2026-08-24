---
name: ar-feat-plan
description: Create an approved, implementation-ready feature plan from a free-form introduction and repository-grounded interview. Use for new capabilities or significant behavior changes; use ar-fix-plan for bugs.
---

# Feature Plan

Create an approved, implementation-ready feature plan from a free-form introduction. Chat in Russian and write files in English.

## Contract

- Work plan-only: investigate read-only and create only the approved plan file. Do not change code, tests, dependencies, generated files, configuration, git state, or external systems.
- Preserve unrelated worktree changes. Do not stage or commit unless asked.
- If no feature introduction is supplied, ask for one. Accept any amount of free-form detail and resolve material gaps through investigation and interview.
- Read repository instructions and only documents clearly related through the introduction, relevant code, or an explicit reference. Do not browse historical plans speculatively.
- Read and apply `$ar-grilling` for the decision interview. Do not create the plan until it reaches shared understanding and the user explicitly authorizes writing it.
- Recommend exploration agents for potentially broad work or independent research that can run in parallel. Give each agent a bounded question and the minimum relevant context.

## Workflow

1. **Scope.** Identify the user-visible outcome, repository, affected workflow, and likely boundaries. Distinguish features from bug fixes and redirect bugs to `$ar-fix-plan`.
2. **Explore.** Trace the relevant current behavior, ownership, interfaces, tests, conventions, and constraints. Before the interview, briefly report established facts, assumptions, affected components, and open decisions.
3. **Decide.** Apply `$ar-grilling` to resolve applicable product behavior, scope, lifecycle and failure semantics, state ownership, integrations, compatibility or migration, and verification. Revisit the repository when an answer opens a new factual branch.
4. **Confirm.** Summarize the agreed outcome and approach, then wait for explicit authorization to create the plan. Imperatives such as "create it" or "go" count.
5. **Write.** Follow an obvious repository-local plan convention. Otherwise use `docs/plans/YYYY-MM-DD-<concise-feature>-plan.md`. Use the current date and never overwrite an existing file without permission.
6. **Validate.** Check the plan against the contract below and confirm it is the only change introduced by this workflow. Do not run application suites merely to validate Markdown unless repository instructions require it.

## Plan contract

Give another engineer enough context to implement without rediscovery:

- title, date, `Ready for implementation` status, scope, and non-goals;
- acceptance criteria covering the intended outcome, applicable lifecycle and edge cases, and behavior that must remain unchanged;
- concise current-state context and confirmed implementation decisions, including ownership, interfaces, invariants, compatibility, and migration where relevant;
- ordered phases and subphases with concrete paths, symbols, responsibilities, dependencies, and documentation or generated-code effects;
- explicit labels for independent work that can run in parallel;
- for a potentially large phase, a recommendation to delegate it plus a bounded prompt template containing its goal, scope, dependencies, constraints, and expected handoff;
- verification mapped to acceptance criteria, with exact automated commands and separate manual or full-stack gates where relevant;
- risks, factual unknowns with a concrete resolution step and action branch, and binary completion criteria. Do not leave product or technical decisions unresolved.

The final implementation phase must require:

- an implementation report at `docs/reports/YYYY-MM-DD-<feature>-report.md` covering completed work, deviations from the plan, verification results, and remaining risks;
- when manual verification is needed, a separate guide at `docs/reports/YYYY-MM-DD-<feature>-manual-test.md` covering prerequisites, test steps, expected results, and test-data cleanup.

Hand off with a link to the plan, its phases, the central decisions, validation performed, confirmation that production files were untouched, and the plan file's git state. Do not repeat the plan in chat.
