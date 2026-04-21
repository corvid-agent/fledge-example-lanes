# fledge-example-lanes

Example repository showcasing **fledge lanes** — composable workflow pipelines for your development lifecycle.

## What are lanes?

Lanes are named pipelines defined in `fledge.toml` that chain multiple tasks into repeatable workflows. They support:

- **Sequential steps** — tasks run one after another
- **Parallel groups** — tasks inside `{ parallel = [...] }` run concurrently
- **Inline commands** — run arbitrary shell commands with `{ run = "..." }`
- **Fail-fast control** — stop on first failure (default) or continue and report all

## Examples in this repo

| Directory | Lane | Description |
|-----------|------|-------------|
| `ci/` | `ci` | Lint, test, and build pipeline |
| `deploy/` | `deploy` | Build, push, and deploy pipeline |
| `release/` | `release` | Test, version, changelog, and publish pipeline |
| `quality/` | `quality` | Lint, format check, and audit pipeline |

## Quick start

```bash
# Install fledge
cargo install fledge

# List lanes in any example directory
cd ci && fledge lane list

# Run a lane
fledge lane run ci

# Dry-run to preview execution plan
fledge lane run ci --dry-run
```

## Lane syntax

Lanes live in `fledge.toml` alongside your task definitions:

```toml
[tasks.lint]
run = "cargo clippy -- -D warnings"

[tasks.test]
run = "cargo test"

[tasks.build]
run = "cargo build --release"

# Sequential lane — steps run in order
[lanes.ci]
description = "Full CI pipeline"
steps = ["lint", "test", "build"]

# Parallel group — lint and fmt run at the same time
[lanes.check]
description = "Quick quality check"
steps = [
  { parallel = ["lint", "fmt"] },
  "test"
]

# Inline commands mixed with task references
[lanes.release]
description = "Build and publish a release"
steps = [
  "test",
  { run = "cargo build --release" },
  "publish"
]

# Continue on failure
[lanes.audit]
description = "Run all audits"
fail_fast = false
steps = ["deps-audit", "license-check", "security-scan"]
```

### Step types

| Type | Format | Description |
|------|--------|-------------|
| Task reference | `"task_name"` | Runs a task defined in `[tasks]` |
| Inline command | `{ run = "command" }` | Runs a shell command directly |
| Parallel group | `{ parallel = ["a", "b"] }` | Runs referenced tasks concurrently |

## Importing lanes

You can import lanes from this repo (or any GitHub repo) into your own project:

```bash
# Import all lanes from a repo
fledge lane import corvid-agent/fledge-example-lanes

# Import from a specific version
fledge lane import corvid-agent/fledge-example-lanes@v1.0.0
```

## Learn more

- [fledge documentation](https://github.com/corvid-agent/fledge)
