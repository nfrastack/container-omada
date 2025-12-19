# nfrastack/container-omada

## About

This repository will build a container for [Omada Software controller](https://www.omadanetworks.com/ca/business-networking/omada/controller/). A flexible network management architrecture.

## Maintainer

- [Nfrastack](https://www.nfrastack.com)

## Table of Contents

- [About](#about)
- [Maintainer](#maintainer)
- [Table of Contents](#table-of-contents)
- [Installation](#installation)
  - [Prebuilt Images](#prebuilt-images)
  - [Quick Start](#quick-start)
  - [Persistent Storage](#persistent-storage)
- [Environment Variables](#environment-variables)
  - [Base Images used](#base-images-used)
  - [Core Configuration](#core-configuration)
- [Users and Groups](#users-and-groups)
  - [Networking](#networking)
- [Maintenance](#maintenance)
  - [Shell Access](#shell-access)
- [Support & Maintenance](#support--maintenance)
- [License](#license)

## Installation

### Prebuilt Images

Feature limited builds of the image are available on the [Github Container Registry](https://github.com/nfrastack/container-omada/pkgs/container/container-omada) and [Docker Hub](https://hub.docker.com/r/nfrastack/omada).

To unlock advanced features, one must provide a code to be able to change specific environment variables from defaults. Support the development to gain access to a code.

To get access to the image use your container orchestrator to pull from the following locations:

```
ghcr.io/nfrastack/container-omada:(image_tag)
docker.io/nfrastack/omada:(image_tag)
```

Image tag syntax is:

`<image>:<optional tag>-<optional_distribution>_<optional_distribution_variant>`

Example:

`ghcr.io/nfrastack/container-omada:latest` or

`ghcr.io/nfrastack/container-omada:1.0` or optionally

`ghcr.io/nfrastack/container-omada:1.0-alpine` or optinally

`ghcr.io/nfrastack/container-omada:alpine`

- `latest` will be the most recent commit
- An optional `tag` may exist that matches the [CHANGELOG](CHANGELOG.md) - These are the safest
- If it is built for multiple distributions there may exist a value of `alpine` or `debian`
- If there are multiple distribution variations it may include a version - see the registry for availability

Have a look at the container registries and see what tags are available.

#### Multi-Architecture Support

Images are built for `amd64` only.

### Quick Start

- The quickest way to get started is using [docker-compose](https://docs.docker.com/compose/). See the examples folder for a working [compose.yml](examples/compose.yml) that can be modified for your use.

- Map [persistent storage](#persistent-storage) for access to configuration and data files for backup.
- Set various [environment variables](#environment-variables) to understand the capabilities of this image.

### Persistent Storage

The following directories are used for configuration and can be mapped for persistent storage.

| Directory | Description |
| --------- | ----------- |
| `/config` | (optional) Configuration Files |
| `/data` | Data Files
| `logs` | Log Files |
### Environment Variables

#### Base Images used

This image relies on a customized base image in order to work.
Be sure to view the following repositories to understand all the customizable options:

| Image                                                   | Description |
| ------------------------------------------------------- | ----------- |
| [OS Base](https://github.com/nfrastack/container-base/) | Base Image  |

Below is the complete list of available options that can be used to customize your installation.

- Variables showing an 'x' under the `Advanced` column can only be set if the containers advanced functionality is enabled.

#### Core Configuration

| Parameter | Description | Default | Advanced |
| --------- | ----------- | ------- | -------- |
| `OMADA_SETUP_MODE`          | Setup Mode                 | `AUTO`           |          |
| `OMADA_USER`                | Omada User                 | `omada`          |          |
| `OMADA_GROUP`               | Omada Group                | `omada`          |          |

| `DATA_PATH` | Data Location | `/data/` | |
| `LOG_PATH` | Log Files Location | `/loca/` | |
| `CACHE_PATH`                | Cache Location             | `/cache/`        |          |
| `WORK_PATH`                 | Work Directory             | `${DATA_PATH}/data/work/`    |          |
| `LOG_TYPE`                  | Log Type                   | `FILE`           |          |
| `DB_PORT`                   | Database Port              | `27017`          |          |
| `LISTEN_MANAGE_HTTP_PORT`   | HTTP Management Port       | `8088`           |          |
| `LISTEN_MANAGE_HTTPS_PORT`  | HTTPS Management Port      | `8043`           |          |
| `LISTEN_PORTAL_HTTP_PORT`   | HTTP Portal Port           | `8888`           |          |
| `LISTEN_PORTAL_HTTPS_PORT`  | HTTPS Portal Port          | `8843`           |          |
| `LISTEN_APP_DISCOVERY_PORT` | App Discovery Port         | `27001`          |          |
| `LISTEN_ADOPT_V1_PORT`      | Adopt v1 Port              | `29812`          |          |
| `LISTEN_UPGRADE_V1_PORT`    | Upgrade v1 Port            | `29813`          |          |
| `LISTEN_MANAGER_V1_PORT`    | Manager v1 Port            | `29811`          |          |
| `LISTEN_MANAGER_V2_PORT`    | Manager v2 Port            | `29814`          |          |
| `LISTEN_DISCOVERY_PORT`     | Discovery Port             | `29810`          |          |
| `LISTEN_TRANSFER_V2_PORT`   | Transfer v2 Port           | `29815`          |          |
| `LISTEN_RTTY_PORT`          | RTTY Port                  | `29816`          |          |
| `LISTEN_OLT_DISCOVERY_PORT` | OLT Discovery Port         | `19810`          |          |
| `LISTEN_DEVICE_MONITOR_PORT`| Device Monitor Port        | `29817`          |          |

## Users and Groups

| Type  | Name      | ID   |
| ----- | --------- | ---- |
| User  | `omada` | 1000 |
| Group | `omada` | 1000 |

### Networking

| Port  | Protocol | Description    |
| ----- | -------- | -------------- |
| 8088   | tcp      | HTTP Management Port  |
| 8043   | tcp      | HTTPS Management Port |
| 8888   | tcp      | HTTP Portal Port      |
| 8843   | tcp      | HTTPS Portal Port     |
| 29810  | udp      | Discovery Port        |
| 27001  | udp      | App Discovery Port    |
| 29811  | tcp      | Manager v1 Port       |
| 29812  | udp      | Adopt v1 Port         |
| 29813  | udp      | Upgrade v1 Port       |
| 29814  | tcp      | Manager v2 Port       |
| 29815  | udp      | Transfer v2 Port      |
| 19810  | udp      | OLT Discovery Port    |
| 29816  | udp      | RTTY Port             |
| 29817  | udp      | Device Monitor Port   |

* * *

## Maintenance

### Shell Access

For debugging and maintenance, `bash` and `sh` are available in the container.

## Support & Maintenance

- For community help, tips, and community discussions, visit the [Discussions board](/discussions).
- For personalized support or a support agreement, see [Nfrastack Support](https://nfrastack.com/).
- To report bugs, submit a [Bug Report](issues/new). Usage questions will be closed as not-a-bug.
- Feature requests are welcome, but not guaranteed. For prioritized development, consider a support agreement.
- Updates are best-effort, with priority given to active production use and support agreements.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
