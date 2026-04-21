# Quality Lane

Code quality pipeline covering linting, formatting, dependency auditing, and documentation checks.

## Lanes

### `quality` — Full quality gate

Runs all quality checks with `fail_fast = false`, so every check runs even if earlier ones fail. This gives a complete picture of all issues.

```
fledge lane run quality --dry-run

Lane: quality — Full quality gate
  1. [parallel] lint, fmt-check
  2. [parallel] deps-audit, license-check
  3. outdated (task)
  4. doc-check (task)
```

### `lint` — Quick lint check

Runs just clippy and format checking in parallel.

### `fix` — Auto-fix formatting then verify

Runs `cargo fmt` to fix formatting, then runs clippy to verify.

## Usage

```bash
cd quality/
fledge lane run quality
fledge lane run lint
fledge lane run fix
```
