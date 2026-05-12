# containers

Homelab Docker images, built and published to ghcr.io via GitHub Actions.

## Images

| Image | Description |
|-------|-------------|
| _(none yet)_ | Add rows as images are added |

## Adding a new image

1. Copy `images/_template/` to `images/<name>/`
2. Update the `Dockerfile`, `.dockerignore`, and `README.md`
3. Replace `OWNER` in labels/docs with your GitHub username
4. Open a PR — the validate workflow builds it
5. Merge to `main` — the build-and-push workflow publishes it to `ghcr.io`

## Workflows

| Workflow | Trigger | Action |
|----------|---------|--------|
| `pr-validate` | PR touching `images/**` | Build changed images (no push) |
| `build-and-push` | Push to `main` touching `images/**` | Build + push to ghcr.io |

Both workflows are path-filtered — only images whose files changed are rebuilt.
