# redlib (build only)

This repository contains **no source**. It exists to build
[redlib-org/redlib](https://github.com/redlib-org/redlib) at a **pinned upstream
commit** and publish it as `ghcr.io/bbaldino/redlib`.

## Why this exists

- The official `quay.io/redlib/redlib` image is stale (April) and **fails OAuth
  on startup** — upstream issues #485 / #551.
- Building at deploy time was rejected: every stack in `homelab-stacks` runs a
  pre-built, exactly-pinned image, and the Docker VM that would have compiled it
  is disk-constrained (it hit 0 bytes free on 2026-09-26 and took Komodo's
  MongoDB down with it). Building here keeps that host out of the loop.

## Current pin

```
upstream: redlib-org/redlib @ a4d36e954cf1bd64f209cd8868c5a29edc81b374
dockerfile: Dockerfile.ubuntu
image: ghcr.io/bbaldino/redlib:a4d36e9
```

## Bumping it

Edit `UPSTREAM_SHA` in `.github/workflows/build.yml` and push, or run the
workflow manually with a different `sha` input. Deliberate, not automatic —
upstream moves when Reddit breaks it.

## Consumer

`webfetch` reaches it in-stack at `http://redlib:8080`. It is **not** published
to the LAN.
