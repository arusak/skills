---
name: ar-review-leftovers
description: Review a Git branch for accidental development residue, configuration drift, and other unintended changes before merge. Use when asked to check branch hygiene, debug leftovers, bypasses, stale docs, or suspicious configuration.
---

# Review Leftovers

Audit the final branch state for unintended changes that a correctness review may miss. Keep the review read-only.

## Establish scope

1. Use the base ref supplied by the user. Otherwise resolve `origin/HEAD`; fall back to `master` or `main` only if one is unambiguous.
2. Verify the base ref, then inspect `git diff <base>...HEAD`, `git log <base>...HEAD --oneline`, and `git status --short`.
3. Review the three-dot diff and relevant uncommitted changes. Treat commit messages as search hints, not evidence of intent.
4. Read repository instructions and feature-specific guidance for changed paths.

Stop if the base ref is invalid. Report an empty diff when there is nothing to review.

## Audit the changes

Read every changed configuration, workflow, manifest, script, Dockerfile, and documentation file. For application changes, trace affected callers and runtime boundaries enough to judge suspicious lines. Compare changed values even on otherwise ordinary lines.

Look for:

- Debug residue: diagnostic logs, `debugger`, verbose flags, body/header/token dumps, and one-off scripts.
- Disabled gates: `|| true`, `continue-on-error`, skipped tests, ignored build or type errors, constant conditions, and permanent feature-flag overrides.
- Dead code or configuration: commented-out alternatives, disabled workflow steps, obsolete keys, and unused settings.
- Local assumptions: absolute paths, development endpoints, hardcoded addresses, user IDs, host binaries, and temporary certificates.
- Numeric mistakes: invalid ports, extra digits, implausible timeout/retry/memory values, unit mismatches, and unsafe defaults.
- Dependency and lockfile drift: placeholder versions, `latest`, unpinned tools, unused experimental dependencies, broad unrelated resolution changes, and global installs that bypass the pinned package manager.
- Command drift across local scripts, CI, Docker, deployment, and docs.
- CI regressions: removed checks, stale caches, shallow checkout assumptions, shared artifact races, and references to deleted actions.
- Docker drift: stale prebuilt images, missing `COPY` inputs, build/runtime dependency mismatches, and host `node_modules` reuse.
- Security relaxation: disabled TLS, authentication, or validation; wildcard CORS; leaked upstream details; broad permissions; and credentials in arguments or logs.
- Test residue: `.only`, `.skip`, weakened assertions, unconditional mocks, and snapshots that mask behavior.
- Rename residue: stale imports, paths, docs, CODEOWNERS, workflow references, and dynamic imports.
- Documentation residue: temporary-work notes, stale commands/actions/images, incomplete dependency lists, and research snapshots presented as current instructions.
- Unrelated product or API changes, merge markers, whitespace errors, generated reports, and editor files.

Search matches are leads, not findings. Confirm a suspicious line was introduced or materially affected by the branch, and inspect its surrounding behavior. Code and executable configuration are the current source of truth unless the user says otherwise; report stale documentation separately from incorrect executable behavior.

Trace operational chains where relevant: workflow command to package script to framework default; Dockerfile to package script to environment and output; manifest to lockfile to runtime tool version; and renamed or deleted files to all references.

## Validate cheaply

Run only relevant, non-mutating checks available in the repository, such as JSON parsing, shell syntax checks, configuration validation, and `git diff --check`. Do not install dependencies or run a full build for this audit. State what was and was not validated.

## Report

Write in the user's language. Rank findings by severity. For each finding, give the file and line, concrete evidence, why it appears accidental or temporary, and the smallest corrective action. Separate confirmed leftovers from intent-dependent suspicions. Omit style preferences, untouched pre-existing problems, and legitimate matches. Say whether common bypasses and debug residue were searched for and found.
