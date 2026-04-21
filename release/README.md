# Release Lane

Release pipeline that validates, versions, builds, and publishes a Rust crate.

## Lanes

### `release` — Full release pipeline

Runs lint and tests in parallel, bumps the version, generates a changelog, builds the release binary, publishes to crates.io, tags the release, and pushes tags.

```
fledge lane run release --dry-run

Lane: release — Full release pipeline
  1. [parallel] lint, test
  2. version (task)
  3. changelog (task)
  4. build (task)
  5. publish (task)
  6. tag (task)
  7. git push --follow-tags (inline)
```

### `release-dry` — Dry release

Everything up to and including the build, but does not publish or push. Useful for verifying the release process.

## Usage

```bash
cd release/
fledge lane run release
fledge lane run release-dry
```
