# Docker Containers

These images mostly exist for my personal use, but others are free to use it. Most of them are considered nightly versions and may contain bugs.

I am constantly looking for improving these images, so if you have any suggestions, please open an issue.

The core principles of these images are:

1. Try to cover at least arm64 & amd64 - more are welcome though
2. Be as small & secure as possible, use distroless where possible
3. The images should be built automatically on every push to the main branch as well as every 12 hours
4. Be available on Docker Hub & GitHub Container Registry
5. The contents of this repository are licensed under the MIT License - the contents of the images follow their respective licenses of the projects

## Web Images

| Image                               | Source Repo                                       | Size                                                                                                                                                                              | Docker Hub                                                                | GitHub Container Registry                                                                                    |
| ----------------------------------- | ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| [BreezeWiki](breezewiki/README.md)  | [Gitdab](https://gitdab.com/cadence/breezewiki)   | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/breezewiki/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/breezewiki)   | [zottelchen/breezewiki](https://hub.docker.com/r/zottelchen/breezewiki)   | [ghcr.io/zottelchen/breezewiki](https://github.com/users/Zottelchen/packages/container/package/breezewiki)   |
| [OpenResume](open-resume/README.md) | [GitHub](https://github.com/xitanggg/open-resume) | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/open-resume/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/open-resume) | [zottelchen/open-resume](https://hub.docker.com/r/zottelchen/open-resume) | [ghcr.io/zottelchen/open-resume](https://github.com/users/Zottelchen/packages/container/package/open-resume) |
| [Sonic](sonic/README.md)            | [GitHub](https://github.com/valeriansaliou/sonic) | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/sonic/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/sonic)             | [zottelchen/sonic](https://hub.docker.com/r/zottelchen/sonic)             | [ghcr.io/zottelchen/sonic](https://github.com/users/Zottelchen/packages/container/package/sonic)             |

<!-- - _🅰: This image is only available for amd64._
- _🅱: This image is only available for arm64._ -->

## Tool Images

_These images are not to be exposed to the network and are therefore not as optimized as much (e.g. they could not use distroless)._

| Image                                                  | Source Repo                                                                                              | Size                                                                                                                                                                                        | Docker Hub                                                                          | GitHub Container Registry                                                                                              |
| ------------------------------------------------------ | -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| [FediFetcher](fedifetcher/README.md)                   | [GitHub](https://github.com/nanos/FediFetcher)                                                           | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/fedifetcher/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/fedifetcher)           | [zottelchen/fedifetcher](https://hub.docker.com/r/zottelchen/fedifetcher)           | [ghcr.io/zottelchen/fedifetcher](https://github.com/users/Zottelchen/packages/container/package/fedifetcher)           |
| [iperf3](iperf3/README.md)                             | [GitHub](https://github.com/nanos/iperf3)                                                                | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/iperf3/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/iperf3)                     | [zottelchen/iperf3](https://hub.docker.com/r/zottelchen/iperf3)                     | [ghcr.io/zottelchen/iperf3](https://github.com/users/Zottelchen/packages/container/package/iperf3)                     |
| [Minecraft Overviewer](overviewer/README.md)           | [GitHub](https://github.com/overviewer/Minecraft-Overviewer)                                             | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/overviewer/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/overviewer)             | [zottelchen/overviewer](https://hub.docker.com/r/zottelchen/overviewer)             | [ghcr.io/zottelchen/overviewer](https://github.com/users/Zottelchen/packages/container/package/overviewer)             |
| [The Minecraft Overviewer](overviewer-clone/README.md) | [GitHub](https://github.com/GregoryAM-SP/The-Minecraft-Overviewer)                                       | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/overviewer-clone/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/overviewer-clone) | [zottelchen/overviewer-clone](https://hub.docker.com/r/zottelchen/overviewer-clone) | [ghcr.io/zottelchen/overviewer-clone](https://github.com/users/Zottelchen/packages/container/package/overviewer-clone) |
| [wmill CLI](wmill-cli/README.md)                       | [GitHub](https://github.com/windmill-labs/windmill) / [Docs](https://www.windmill.dev/docs/advanced/cli) | [![Docker Image Size (tag)](https://img.shields.io/docker/image-size/zottelchen/wmill-cli/latest?logo=docker&label=%E2%80%8B)](https://hub.docker.com/r/zottelchen/wmill-cli)               | [zottelchen/wmill-cli](https://hub.docker.com/r/zottelchen/wmill-cli)               | [ghcr.io/zottelchen/wmill-cli](https://github.com/users/Zottelchen/packages/container/package/wmill-cli)               |

### Retired Images

- Scribe (too much work to maintain a custom image)
- Enhanced TTVDropBot (broken by Twitch)
- Nitter & Nitter Privacydevel ([died](https://github.com/zedeus/nitter/issues/1155#issuecomment-1913361757). RIP. Use Mastodon instead. Screw X/Twitter/Musk.)
