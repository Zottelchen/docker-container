# Docker Containers

These images mostly exist for my personal use, but others are free to use it. Most of them are considered nightly versions and may contain bugs.

I am constantly looking for improving these images, so if you have any suggestions, please open an issue.

The core principles of these images are:

1. Try to cover at least arm64 & amd64 - more are welcome though
2. Be as small & secure as possible, use distroless where possible
3. Be available on Docker Hub & GitHub Container Registry

## Images

| Image                                                  | Source Repo                                       | Size                                                                                                                                                                                              | Docker Hub                                                                                | GitHub Container Registry                                                                                                    |
| ------------------------------------------------------ | ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| [BreezeWiki](breezewiki/README.md)                     | [Gitdab](https://gitdab.com/cadence/breezewiki)   | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/breezewiki/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/breezewiki)                   | [zottelchen/breezewiki](https://hub.docker.com/r/zottelchen/breezewiki)                   | [ghcr.io/zottelchen/breezewiki](https://github.com/users/Zottelchen/packages/container/package/breezewiki)                   |
| [Nitter](nitter/README.md)                             | [GitHub](https://github.com/zedeus/nitter)        | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/nitter/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/nitter)                           | [zottelchen/nitter](https://hub.docker.com/r/zottelchen/nitter)                           | [ghcr.io/zottelchen/nitter](https://github.com/users/Zottelchen/packages/container/package/nitter)                           |
| [Nitter (PrivacyDevel)](nitter-privacydevel/README.md) | [GitHub](https://github.com/privacydevel/nitter)  | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/nitter-privacydevel/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/nitter-privacydevel) | [zottelchen/nitter-privacydevel](https://hub.docker.com/r/zottelchen/nitter-privacydevel) | [ghcr.io/zottelchen/nitter-privacydevel](https://github.com/users/Zottelchen/packages/container/package/nitter-privacydevel) |
| [Sonic](sonic/README.md)⚠                              | [GitHub](https://github.com/valeriansaliou/sonic) | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/sonic/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/sonic)                             | [zottelchen/sonic](https://hub.docker.com/r/zottelchen/sonic)                             | [ghcr.io/zottelchen/sonic](https://github.com/users/Zottelchen/packages/container/package/sonic)                             |
| [Calckey](calckey/README.md)⚠‼                         | [Codeberg](https://codeberg.org/calckey/calckey)  | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/calckey/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/calckey)                         | [zottelchen/calckey](https://hub.docker.com/r/zottelchen/calckey)                         | _not available_                                                                                                              |

- _⚠: This image is not available for both (arm64/amd64) platforms._
- _‼: This image is only temporarily available (e.g. until the official image is available)._
