# Docker Containers

These images mostly exist for my personal use, but others are free to use it.

I am constantly looking for improving these images, so if you have any suggestions, please open an issue.

The core principles of these images are:

1. Try to cover at least arm64 & amd64 - more are welcome though
2. Be as small & secure as possible, use distroless where possible
3. Be available on Docker Hub & GitHub Container Registry

## Images

| Image                                                  | Source Repo                                      | Description                                                                                                                                    | Size                                                                                                                                                                              | Docker Hub                                                                                | GitHub Container Registry                                                                                                    |
| ------------------------------------------------------ | ------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| [BreezeWiki](breezewiki/README.md)                     | [Gitdab](https://gitdab.com/cadence/breezewiki)  | BreezeWiki makes wiki pages on Fandom readable                                                                                                 | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/breezewiki/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/breezewiki)                   | [zottelchen/breezewiki](https://hub.docker.com/r/zottelchen/breezewiki)                   | [ghcr.io/zottelchen/breezewiki](https://github.com/users/Zottelchen/packages/container/package/breezewiki)                   |
| [Nitter](nitter/README.md)                             | [GitHub](https://github.com/zedeus/nitter)       | A free and open source alternative Twitter front-end focused on privacy and performance.                                                       | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/nitter/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/nitter)                           | [zottelchen/nitter](https://hub.docker.com/r/zottelchen/nitter)                           | [ghcr.io/zottelchen/nitter](https://github.com/users/Zottelchen/packages/container/package/nitter)                           |
| [Nitter (PrivacyDevel)](nitter-privacydevel/README.md) | [GitHub](https://github.com/privacydevel/nitter) | A fork of the alternative Twitter frontend, which also enables NSFW content, at the price of having & setting a Twitter account in the config. | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/nitter-privacydevel/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/nitter-privacydevel) | [zottelchen/nitter-privacydevel](https://hub.docker.com/r/zottelchen/nitter-privacydevel) | [ghcr.io/zottelchen/nitter-privacydevel](https://github.com/users/Zottelchen/packages/container/package/nitter-privacydevel) |
