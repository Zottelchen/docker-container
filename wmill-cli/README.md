# wmill (Windmill) CLI

A [wmill CLI](https://github.com/windmill-labs/windmill) image. See [wmill CLI's documentation](https://www.windmill.dev/docs/advanced/cli) for more information.

For more information about the image, see the [GitHub page](https://github.com/Zottelchen/docker-container/wmill-cli).

[GitHub Container Registry](https://github.com/users/Zottelchen/packages/container/package/wmill-cli) | [Docker Hub](https://hub.docker.com/r/zottelchen/wmill-cli)

## Usage:

- Run the container like a command:

```bash
docker run --rm -ti -v '${PWD}:${PWD}' -w '${PWD}' zottelchen/wmill-cli --help
```

- or from Github Registry:

```bash
docker run --rm -ti -v '${PWD}:${PWD}' -w '${PWD}' ghcr.io/zottelchen/wmill-cli --help
```

- or create an alias to use:

```bash
alias wmill="docker run --rm -ti -v '${PWD}:${PWD}' -w '${PWD}' zottelchen/wmill-cli"
```

## Supported Platforms

- linux/amd64
- linux/arm64

## Stats

[![GitHub Workflow Status (with event)](https://img.shields.io/github/actions/workflow/status/zottelchen/docker-container/wmill-cli_docker.yml?logo=github)](https://github.com/Zottelchen/docker-container/actions/workflows/wmill-cli_docker.yml)
[![Docker Pulls](https://img.shields.io/docker/pulls/zottelchen/wmill-cli?logo=docker)](https://hub.docker.com/r/zottelchen/wmill-cli)
[![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/wmill-cli/latest?logo=docker)](https://hub.docker.com/r/zottelchen/wmill-cli)
[![Docker Stars](https://img.shields.io/docker/stars/zottelchen/wmill-cli?label=%E2%AD%90%20docker%20stars)](https://hub.docker.com/r/zottelchen/wmill-cli)
[![GHCR Image Size](https://ghcr-badge.egpl.dev/zottelchen/wmill-cli/size)](https://github.com/users/Zottelchen/packages/container/package/wmill-cli)
