# Deploy Lane

Deployment pipeline for containerized applications with Docker and Kubernetes.

## Lanes

### `deploy` — Full deploy pipeline

Runs tests, builds and pushes a Docker image, runs database migrations, restarts the Kubernetes deployment, and sends a Slack notification.

```
fledge lane run deploy --dry-run

Lane: deploy — Full deploy pipeline
  1. test (task)
  2. build (task)
  3. push (task)
  4. migrate (task)
  5. kubectl rollout restart deployment/myapp (inline)
  6. notify (task)
```

### `deploy-quick` — Deploy without migrations

Same as full deploy but skips database migrations. Useful for code-only changes.

### `rollback` — Rollback to previous deployment

Reverts to the previous Kubernetes deployment and sends a notification.

## Usage

```bash
cd deploy/
fledge lane run deploy
fledge lane run rollback
```
