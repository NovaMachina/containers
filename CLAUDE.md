# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Homelab Docker images built and published to `ghcr.io` via GitHub Actions. Each image lives in `images/<name>/` and is built independently.

## Local build

```sh
# Build a single image locally
docker build -t <name>:local images/<name>/

# Test it
docker run --rm <name>:local
```

No global build command — each image is standalone.

## Adding a new image

1. Copy `images/_template/` to `images/<name>/`
2. Edit `Dockerfile`, `.dockerignore`, `README.md`
3. Replace `NovaMachina` in labels/docs with actual GitHub username
4. PR triggers `pr-validate` (build only, no push)
5. Merge to `main` triggers `build-and-push` (publishes to `ghcr.io/<owner>/<name>:latest` and `:<sha>`)

## CI behavior

Both workflows detect changed images by diffing `images/**` — only dirs that changed are rebuilt. Dirs prefixed with `_` (like `_template`) are excluded from CI builds.

## Conventions

- Base on `alpine:3.21` unless a specific base is needed
- Use `COPY rootfs/ /` pattern for config files
- OCI labels: `org.opencontainers.image.source` and `.description` required
- `ENTRYPOINT` preferred over `CMD` for single-purpose images
