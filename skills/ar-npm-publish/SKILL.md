---
name: ar-npm-publish
description: Safely version, validate, tag, and publish an npm package
  when the user requests an npm release or publish. Stops before
  publishing whenever package, registry, version, tag, contents,
  credentials, or Git state is uncertain.
disable-model-invocation: true
---

# Publish an npm package

Treat `npm publish` as irreversible. Fail closed: a warning, ambiguity,
failed check, unexpected diff, or missing evidence stops the release.
Never weaken a check or guess release metadata to make publishing
proceed.

## 1. Establish the release target

Keep this stage read-only.

1.  Resolve exactly one package directory and its workspace root. Read
    its `package.json`, lockfile, scripts, publish configuration, and
    Git history.
2.  Require a committed, clean working tree on a named branch. Stop for
    unrelated changes, an existing target tag, or an already-published
    target version.
3.  Determine the package name, current version, registry, npm dist-tag,
    version increment, and Git tag name. The version increment defaults
    to `patch`; all other values must come from repository convention or
    the user.
4.  Query configuration and authentication without displaying tokens or
    raw `.npmrc` contents. Verify the active identity and registry with
    scoped npm commands such as `npm whoami --registry <registry>` and
    `npm view`.
5.  Stop if the package is private, the registry or tag convention is
    ambiguous, credentials are unavailable, the target version is not
    newer, or the user has not authorized that exact package and
    registry.

Present the resolved package, old and proposed versions, registry, npm
dist-tag, and Git tag. Obtain confirmation before changing versions.

## 2. Bump and inspect

Run `npm version <increment-or-version> --no-git-tag-version` at the
correct package or workspace scope. Use `patch` when the user did not
choose a version.

Inspect the diff immediately. It may contain only the intended package
version and the corresponding lockfile updates. Stop on any other
change; leave the state visible and ask before attempting recovery.

## 3. Build and validate the final package

Run the repository's required build and tests, then all three package
gates from the package directory:

```bash
npx --yes publint
npm pack --dry-run --json
npx --yes @arethetypeswrong/cli --pack .
```

Use already-installed binaries when available instead of adding
dependencies. Review the dry-pack JSON, not just its exit code: confirm
the package identity, version, filename, size, and complete file list;
confirm every `main`, `module`, `types`, and `exports` target exists in
the packed contents. Secrets, unrelated files, missing build output,
warnings, or any failed gate stop the release.

Do not suppress publint or ATTW findings unless the user explicitly
accepts the specific finding and its consumer impact.

## 4. Commit and tag

Stage only the expected version and lockfile changes. Create the release
commit, then create an annotated Git tag using the confirmed repository
convention. Verify the tag points to the release commit and the working
tree is clean.

Never replace, move, or force an existing tag. Do not push commits or
tags unless the user separately requests it.

## 5. Final publish gate

Immediately before publishing, show:

- package name and version;
- registry, npm dist-tag, and any access setting;
- Git commit and tag;
- the dry-pack filename and contents summary;
- every validation result;
- the exact `npm publish` command.

Require explicit confirmation of that summary. Publish with explicit
package scope, registry, and dist-tag rather than relying on ambient npm
defaults. Do not publish if anything changed after validation.

After publishing, verify the exact version from the same registry with
`npm view`. A publish or verification failure stops the process: report
the observed state and wait. Never retry, unpublish, change tags, or
repair Git history automatically.
