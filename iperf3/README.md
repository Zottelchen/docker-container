# iperf3

A [iperf3](https://iperf.fr/) image. See [iperf3's documentation](https://iperf.fr/iperf-doc.php) for more information.

For more information about the image, see the [GitHub page](https://github.com/Zottelchen/docker-container/tree/main/iperf3) or look at the [Dockerfile](https://github.com/Zottelchen/docker-container/tree/main/iperf3/Dockerfile).

[GitHub Container Registry](https://github.com/users/Zottelchen/packages/container/package/iperf3) | [Docker Hub](https://hub.docker.com/r/zottelchen/iperf3)

## Usage:

- Run the container like a command:

```bash
docker run --rm -ti -p 5201:5201 zottelchen/iperf3 --help
```

- or from Github Registry:

```bash
docker run --rm -ti -p 5201:5201 ghcr.io/zottelchen/iperf3 --help
```

- or create an alias to use:

```bash
alias iperf="docker run --rm -ti -p 5201:5201 zottelchen/iperf3"
```

## Supported Platforms

- linux/amd64
- linux/arm64

## Stats

[![GitHub Workflow Status (with event)](https://img.shields.io/github/actions/workflow/status/zottelchen/docker-container/wmill_docker.yml?logo=github)](https://github.com/Zottelchen/docker-container/actions/workflows/wmill_docker.yml)
[![Docker Pulls](https://img.shields.io/docker/pulls/zottelchen/iperf3?logo=docker)](https://hub.docker.com/r/zottelchen/iperf3)
[![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/iperf3/latest?logo=docker)](https://hub.docker.com/r/zottelchen/iperf3)
[![Docker Stars](https://img.shields.io/docker/stars/zottelchen/iperf3?label=%E2%AD%90%20docker%20stars)](https://hub.docker.com/r/zottelchen/iperf3)
[![GHCR Image Size](https://ghcr-badge.egpl.dev/zottelchen/iperf3/size)](https://github.com/users/Zottelchen/packages/container/package/iperf3)
