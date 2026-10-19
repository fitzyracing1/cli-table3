# patch-cloud build of cli-table3@0.6.5

This tarball was built by patch-cloud from [fitzyracing1/cli-table3@patch-cloud](https://github.com/fitzyracing1/cli-table3/tree/patch-cloud),
a fork of [cli-table/cli-table3](https://github.com/cli-table/cli-table3). It is **not** an official upstream release.
Package name and version are unchanged from upstream (`cli-table3@0.6.5`, base `tag v0.6.5`).

## Fix

A rowSpan that extends past the last row is clamped instead of crashing with "TypeError: Cannot read properties of undefined (reading 'length')".

- Upstream PR: https://github.com/cli-table/cli-table3/pull/359
- Credit: @spokodev (PR #359 author; Co-authored-by in the fork commit)

## Exactly what changed vs upstream

- src/layout-manager.js: stop inserting RowSpanCells once the target row does not exist (PR #359, applied cleanly).
- test/issues/rowspan-overflow-test.js: regression test from the PR (not shipped in the package).
- Added this `PATCH-CLOUD.md` and a `_patchCloud` field in `package.json` (metadata only).

## Verification

- new Table().push([{ content: 'aaaa bbbb', rowSpan: 2 }]); table.toString() renders; upstream 0.6.5 throws.
- Upstream jest suite: 292 passed, 1 skipped, 1 failed; the failure (original-cli-table 'test table colors') fails identically on unmodified 0.6.5 in this environment.

## Opting out

Remove the patch-cloud `registry=` override and reinstall from registry.npmjs.org to get the upstream tarball.

## GitHub Packages (scoped name)

The same patched build can be published to GitHub Packages as `@fitzyracing1/cli-table3@0.6.5`
(GitHub Packages only accepts names scoped to the repo owner). The unscoped name `cli-table3`
is what the patch-cloud registry serves; the scoped name is what GitHub Packages serves.

```ini
# .npmrc (project or ~/.npmrc). GitHub Packages npm needs a token even for public packages:
@fitzyracing1:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}   # a token with read:packages
```

```bash
# keep require('cli-table3') / import 'cli-table3' working via an npm alias:
npm install cli-table3@npm:@fitzyracing1/cli-table3@0.6.5
# or install under the scoped name:
npm install @fitzyracing1/cli-table3@0.6.5
```
