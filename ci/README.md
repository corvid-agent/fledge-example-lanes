# CI Lane

Continuous integration pipeline that validates code quality and builds the project.

## Lanes

### `ci` — Full CI pipeline

Runs lint and format checks in parallel, then tests, then builds the release binary.

```
fledge lane run ci --dry-run

Lane: ci — Full CI pipeline
  1. [parallel] lint, fmt-check
  2. test (task)
  3. build (task)
```

### `ci-quick` — Quick CI check

Runs just lint and test, skipping the release build. Useful for fast feedback during development.

## Usage

```bash
cd ci/
fledge lane run ci
fledge lane run ci-quick
```
