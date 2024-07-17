---
title: "Docker"
weight: 21
---

# Docker

{{< hint warning >}}
**It is recommended to use Docker.**
You can create your virtual environment with venv since Python is pre-installed on the OMUI Server.
However, this is not recommended because the Python version may be out of date.
{{</ hint >}}

This page explains the basic usage of Docker.
To learn more, check [the official documentation](https://docs.docker.com/).

## Rootless Docker Configuration

{{< hint info >}}
Do this only once. Not required if already installed.
{{</ hint >}}

You can use [Rootless Docker](https://docs.docker.com/engine/security/rootless/) on the OMUI Server.
Rootless Docker enables you to manage Docker containers or images for individual users.

Please run the following command to configure Rootless Docker:

```bash
$ rootless-docker-install
```

## Docker Container

The following command creates a new Docker container and run `[COMMAND]` in the container:
```bash
$ docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

Typical options include:
```bash
# Remove the container automatically when you stop the container
--rm

# Bind-mount the SRC to the DST
--volume SRC:DST

# Set the working directory in the container
--workdir PATH

# GPU allocation
--gpus DEVICE
```

This example creates a Docker container using `nvidia/cuda:12.5.1-cudnn-devel-ubuntu22.04` image downloaded from [Docker Hub](https://hub.docker.com/), and runs `nvidia-smi` command in the container.

```bash
$ docker container run \
  --rm \
  --gpus '"device=0"' \
  nvidia/cuda:12.5.1-cudnn-devel-ubuntu22.04 \
  nvidia-smi
```

## Docker Image

To prepare a Docker image, create your own Docker image from scratch using a Dockerfile or download it from the Docker registry.
[Docker Hub](https://hub.docker.com/) and [NVIDIA NGC Catalog](https://catalog.ngc.nvidia.com/containers) are the popular Docker registries.

{{< hint warning >}}
When selecting a Docker image that includes the CUDA Toolkit, please check the CUDA Toolkit version included in the image.
You can check the supported CUDA Toolkit version by running the `nvidia-smi` command on the server.
The version displayed in the upper right corner is the latest version of the supported CUDA Toolkit.

( Version displayed in `nvidia-smi` ≦ CUDA Toolkit version you use)
{{</ hint >}}

You can check the loaded images by running:

```bash
$ docker images

REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    35a88802559d   5 weeks ago   78.1MB
```

You can remove Docker images by running:

```bash
$ docker image rm IMAGE
```

{{< hint warning >}}
Please remove images that are no longer in use.
{{</ hint >}}

## Reference

- [Docker入門（第一回）～Dockerとは何か、何が良いのか～](https://knowledge.sakura.ad.jp/13265/)
- [実践 Docker - ソフトウェアエンジニアの「Docker よくわからない」を終わりにする本](https://zenn.dev/suzuki_hoge/books/2022-03-docker-practice-8ae36c33424b59)