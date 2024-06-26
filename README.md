Dockerhub: https://hub.docker.com/r/tlan16/qbittorrent-enhanced

Dockerfile: https://github.com/tlan16/docker-qbittorrent-enhanced-edition/blob/main/Dockerfile

Docker compose:

```yaml
---
version: "3.9"
services:
  qbittorrent:
    image: tlan16/qbittorrent-enhanced:latest
    container_name: qbittorrent
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - WEBUI_PORT=8080
    volumes:
      - /path/to/appdata/config:/config
      - /path/to/downloads:/downloads
    ports:
      - "8080:8080"
      - "6881:6881"
      - "6881:6881/udp"
    restart: unless-stopped
```

This image is based on [linuxserver/docker-qbittorrent](https://github.com/linuxserver/docker-qbittorrent) and adds [qBittorrent-Enhanced-Edition](https://api.github.com/repos/c0re100/qBittorrent-Enhanced-Edition).

Alternative UI [VueTorrent](https://github.com/WDaan/VueTorrent) is available at path `/vuetorrent`. Enable it by setting `tools` --> `options` --> `Web UI` --> `[✔️] Use alternative Web UI` to `Files location:` `/vuetorrent`. Note if you have CSP enforced (e.g. in reverse proxy), you may need up update the CSP. 

---

<!-- DO NOT EDIT THIS FILE MANUALLY -->
<!-- Please read https://github.com/linuxserver/docker-qbittorrent/blob/master/.github/CONTRIBUTING.md -->
[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)](https://linuxserver.io)

[![Blog](https://img.shields.io/static/v1.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=linuxserver.io&message=Blog)](https://blog.linuxserver.io "all the things you can do with our containers including How-To guides, opinions and much more!")
[![Discord](https://img.shields.io/discord/354974912613449730.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=Discord&logo=discord)](https://discord.gg/YWrKVTn "realtime support / chat with the community and the team.")
[![Discourse](https://img.shields.io/discourse/https/discourse.linuxserver.io/topics.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&logo=discourse)](https://discourse.linuxserver.io "post on our community forum.")
[![Fleet](https://img.shields.io/static/v1.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=linuxserver.io&message=Fleet)](https://fleet.linuxserver.io "an online web interface which displays all of our maintained images.")
[![GitHub](https://img.shields.io/static/v1.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=linuxserver.io&message=GitHub&logo=github)](https://github.com/linuxserver "view the source for all of our repositories.")
[![Open Collective](https://img.shields.io/opencollective/all/linuxserver.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=Supporters&logo=open%20collective)](https://opencollective.com/linuxserver "please consider helping us by either donating or contributing to our budget")

The [LinuxServer.io](https://linuxserver.io) team brings you another container release featuring:

* regular and timely application updates
* easy user mappings (PGID, PUID)
* custom base image with s6 overlay
* weekly base OS updates with common layers across the entire LinuxServer.io ecosystem to minimise space usage, down time and bandwidth
* regular security updates

Find us at:

* [Blog](https://blog.linuxserver.io) - all the things you can do with our containers including How-To guides, opinions and much more!
* [Discord](https://discord.gg/YWrKVTn) - realtime support / chat with the community and the team.
* [Discourse](https://discourse.linuxserver.io) - post on our community forum.
* [Fleet](https://fleet.linuxserver.io) - an online web interface which displays all of our maintained images.
* [GitHub](https://github.com/linuxserver) - view the source for all of our repositories.
* [Open Collective](https://opencollective.com/linuxserver) - please consider helping us by either donating or contributing to our budget

# [linuxserver/qbittorrent](https://github.com/linuxserver/docker-qbittorrent)

The [qBittorrent-Enhanced-Edition](https://api.github.com/repos/c0re100/qBittorrent-Enhanced-Edition) project aims to provide an open-source software alternative to µTorrent. qBittorrent is based on the Qt toolkit and libtorrent-rasterbar library.

[![qbittorrent](https://github.com/linuxserver/docker-templates/raw/master/linuxserver.io/img/qbittorrent-icon.png)](https://www.qbittorrent.org/)

## Supported Architectures

- [x] ARM
- [x] amd64

## Application Setup

The web UI is at `<your-ip>:8080` and a temporary password for the `admin` user will be printed to the container log on startup.

You must then change username/password in the web UI section of settings. If you do not change the password a new one will be generated every time the container starts.

If you are running a very old (3.x) kernel you may run into [this issue](https://github.com/linuxserver/docker-qbittorrent/issues/103) which can be worked around using [this method](https://github.com/linuxserver/docker-qbittorrent/issues/103#issuecomment-831238484)

### WEBUI_PORT variable

Due to issues with CSRF and port mapping, should you require to alter the port for the web UI you need to change both sides of the -p 8080 switch AND set the WEBUI_PORT variable to the new port.

For example, to set the port to 8090 you need to set -p 8090:8090 and -e WEBUI_PORT=8090

## Usage

To help you get started creating a container from this image you can either use docker-compose or the docker cli.

## Parameters

Containers are configured using parameters passed at runtime (such as those above). These parameters are separated by a colon and indicate `<external>:<internal>` respectively. For example, `-p 8080:80` would expose port `80` from inside the container to be accessible from the host's IP on port `8080` outside the container.

|      Parameter       | Function                                                                                                       |
|:--------------------:|----------------------------------------------------------------------------------------------------------------|
|      `-p 8080`       | WebUI                                                                                                          |
|      `-p 6881`       | tcp connection port                                                                                            |
|    `-p 6881/udp`     | udp connection port                                                                                            |
|    `-e PUID=1000`    | for UserID - see below for explanation                                                                         |
|    `-e PGID=1000`    | for GroupID - see below for explanation                                                                        |
|   `-e TZ=Etc/UTC`    | specify a timezone to use, see this [list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List). |
| `-e WEBUI_PORT=8080` | for changing the port of the web UI, see below for explanation                                                 |
|     `-v /config`     | Contains all relevant configuration files.                                                                     |
|   `-v /downloads`    | Location of downloads on disk.                                                                                 |

## Environment variables from files (Docker secrets)

You can set any environment variable from a file by using a special prepend `FILE__`.

As an example:

```bash
-e FILE__MYVAR=/run/secrets/mysecretvariable
```

Will set the environment variable `MYVAR` based on the contents of the `/run/secrets/mysecretvariable` file.

## Umask for running applications

For all of our images we provide the ability to override the default umask settings for services started within the containers using the optional `-e UMASK=022` setting.
Keep in mind umask is not chmod it subtracts from permissions based on it's value it does not add. Please read up [here](https://en.wikipedia.org/wiki/Umask) before asking for support.

## User / Group Identifiers

When using volumes (`-v` flags), permissions issues can arise between the host OS and the container, we avoid this issue by allowing you to specify the user `PUID` and group `PGID`.

Ensure any volume directories on the host are owned by the same user you specify and any permissions issues will vanish like magic.

In this instance `PUID=1000` and `PGID=1000`, to find yours use `id your_user` as below:

```bash
id your_user
```

Example output:

```text
uid=1000(your_user) gid=1000(your_user) groups=1000(your_user)
```

## Docker Mods

[![Docker Mods](https://img.shields.io/badge/dynamic/yaml?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=qbittorrent&query=%24.mods%5B%27qbittorrent%27%5D.mod_count&url=https%3A%2F%2Fraw.githubusercontent.com%2Flinuxserver%2Fdocker-mods%2Fmaster%2Fmod-list.yml)](https://mods.linuxserver.io/?mod=qbittorrent "view available mods for this container.") [![Docker Universal Mods](https://img.shields.io/badge/dynamic/yaml?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&label=universal&query=%24.mods%5B%27universal%27%5D.mod_count&url=https%3A%2F%2Fraw.githubusercontent.com%2Flinuxserver%2Fdocker-mods%2Fmaster%2Fmod-list.yml)](https://mods.linuxserver.io/?mod=universal "view available universal mods.")

We publish various [Docker Mods](https://github.com/linuxserver/docker-mods) to enable additional functionality within the containers. The list of Mods available for this image (if any) as well as universal mods that can be applied to any one of our images can be accessed via the dynamic badges above.

## Support Info

* Shell access whilst the container is running:

    ```bash
    docker exec -it qbittorrent /bin/bash
    ```

* To monitor the logs of the container in realtime:

    ```bash
    docker logs -f qbittorrent
    ```

* Container version number:

    ```bash
    docker inspect -f '{{ index .Config.Labels "build_version" }}' qbittorrent
    ```

* Image version number:

    ```bash
    docker inspect -f '{{ index .Config.Labels "build_version" }}' lscr.io/linuxserver/qbittorrent:latest
    ```

## Updating Info

Most of our images are static, versioned, and require an image update and container recreation to update the app inside. With some exceptions (ie. nextcloud, plex), we do not recommend or support updating apps inside the container. Please consult the [Application Setup](#application-setup) section above to see if it is recommended for the image.

Below are the instructions for updating containers:

### Via Docker Compose

* Update images:
    * All images:

        ```bash
        docker-compose pull
        ```

    * Single image:

        ```bash
        docker-compose pull qbittorrent
        ```

* Update containers:
    * All containers:

        ```bash
        docker-compose up -d
        ```

    * Single container:

        ```bash
        docker-compose up -d qbittorrent
        ```

* You can also remove the old dangling images:

    ```bash
    docker image prune
    ```

### Via Docker Run

* Update the image:

    ```bash
    docker pull lscr.io/linuxserver/qbittorrent:latest
    ```

* Stop the running container:

    ```bash
    docker stop qbittorrent
    ```

* Delete the container:

    ```bash
    docker rm qbittorrent
    ```

* Recreate a new container with the same docker run parameters as instructed above (if mapped correctly to a host folder, your `/config` folder and settings will be preserved)
* You can also remove the old dangling images:

    ```bash
    docker image prune
    ```

### Via Watchtower auto-updater (only use if you don't remember the original parameters)

* Pull the latest image at its tag and replace it with the same env variables in one run:

    ```bash
    docker run --rm \
      -v /var/run/docker.sock:/var/run/docker.sock \
      containrrr/watchtower \
      --run-once qbittorrent
    ```

* You can also remove the old dangling images: `docker image prune`

**warning**: We do not endorse the use of Watchtower as a solution to automated updates of existing Docker containers. In fact we generally discourage automated updates. However, this is a useful tool for one-time manual updates of containers where you have forgotten the original parameters. In the long term, we highly recommend using [Docker Compose](https://docs.linuxserver.io/general/docker-compose).

### Image Update Notifications - Diun (Docker Image Update Notifier)

**tip**: We recommend [Diun](https://crazymax.dev/diun/) for update notifications. Other tools that automatically update containers unattended are not recommended or supported.

## Building locally

If you want to make local modifications to these images for development purposes or just to customize the logic:

```bash
git clone https://github.com/linuxserver/docker-qbittorrent.git
cd docker-qbittorrent
docker build \
  --no-cache \
  --pull \
  -t lscr.io/linuxserver/qbittorrent:latest .
```

The ARM variants can be built on x86_64 hardware using `multiarch/qemu-user-static`

```bash
docker run --rm --privileged multiarch/qemu-user-static:register --reset
```

Once registered you can define the dockerfile to use with `-f Dockerfile.aarch64`.

## Versions

* **25.12.23:** - Only pull stable releases of qbittorrent-cli.
* **07.10.23:** - Install unrar from [linuxserver repo](https://github.com/linuxserver/docker-unrar).
* **10.08.23:** - Bump unrar to 6.2.10.
* **17.06.23:** - Deprecate armhf as per [https://www.linuxserver.io/armhf](https://www.linuxserver.io/armhf).
* **10.06.23:** - Bump unrar to 6.2.8.
* **23.02.23:** - Add qt6-qtbase-sqlite to support SQLite database for resume files.
* **29.11.22:** - Add openssl1.1-compat for qbittorrent-cli.
* **31.10.22:** - Add libtorrentv1 branch.
* **31.08.22:** - Rebase to Alpine Edge again to follow latest releases.
* **12.08.22:** - Bump unrar to 6.1.7.
* **16.06.22:** - Rebase to Alpine 3.16 from edge.
* **25.05.22:** - Fetch qbitorrent-cli from upstream repo.
* **02.03.22:** - Add unrar, 7zip, and qbitorrent-cli.
* **01.03.22:** - Add python for search plugin support.
* **23.02.22:** - Rebase to Alpine Edge, install from Alpine repos.
* **19.02.22:** - Add jq to build-stage
* **07.01.22:** - Rebase to Alpine, build from source.
* **06.01.22:** - Deprecate unstable branch.
* **10.02.21:** - Rebase to focal.
* **20.01.21:** - Deprecate `UMASK_SET` in favor of UMASK in baseimage, see above for more information.
* **12.11.20:** - Stop creating /config/data directory on startup
* **03.04.20:** - Fix adding search engine plugin
* **02.08.19:** - Add qbitorrent-cli for processing scripts.
* **23.03.19:** - Switching to new Base images, shift to arm32v7 tag.
* **14.01.19:** - Rebase to Ubuntu, add multi arch and pipeline logic.
* **25.09.18:** - Use buildstage type build, bump qbitorrent to 4.1.3.
* **14.08.18:** - Rebase to alpine 3.8, bump libtorrent to 1.1.9 and qbitorrent to 4.1.2.
* **08.06.18:** - Bump qbitorrent to 4.1.1.
* **26.04.18:** - Bump libtorrent to 1.1.7.
* **02.03.18:** - Bump qbitorrent to 4.0.4 and libtorrent to 1.1.6.
* **02.01.18:** - Deprecate cpu_core routine lack of scaling.
* **19.12.17:** - Update to v4.0.3.
* **09.02.17:** - Rebase to alpine 3.7
* **01.12.17:** - Update to v4.0.2.
* **27.11.17:** - Update to v4 and use cpu_core routine to speed up builds.
* **16.09.17:** - Bump to 3.3.16, Add WEBUI_PORT variable and notes to README to allow changing port of webui.
* **01.08.17:** - Initial Release.
* **12.02.18:** - Initial Release.
