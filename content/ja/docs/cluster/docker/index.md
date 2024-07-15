---
title: "Docker"
weight: 40
bookFlatSection: true
---

# Dockerを用いた環境構築

ここでは、CUDA v.11.7.1とcudnn v8、pytorch、ubuntu22.04を使ったGPU環境の構築を行います。

{{< hint info >}}
Dockerとは何か？についてはここでは深く扱いません。
概要の把握にはこちらの[解説記事](https://knowledge.sakura.ad.jp/13265/)を参考にしてください
{{</ hint >}}

## rootless-docker-installのインストール(初回ログイン時のみ)

```sh
rootless-docker-install
```

## 使用するDocker imageの確認

NVIDIA公式が公開しているDocker Hubから、今回対象とするDocker imageを検索します。
今回は[このサイト](https://hub.docker.com/layers/nvidia/cuda/11.7.1-cudnn8-runtime-ubuntu20.04/images/sha256-2028e3ca7cf0f77554c352d9b3eabe4c2a8a46d0843dc3ed514ea6f1df77b7eb?context=explore) で公開されているイメージを使います。


![alt text](<img/tag_list.png>)

右側にコマンドがあるので、それをそのままコピーして使用します。

```sh
docker pull nvidia/cuda:11.7.1-cudnn8-runtime-ubuntu20.04

# kakehi@igpu01:~$ docker pull nvidia/cuda:11.7.1-cudnn8-runtime-ubuntu20.04
# 11.7.1-cudnn8-runtime-ubuntu20.04: Pulling from nvidia/cuda
# 96d54c3075c9: Pull complete
# de0e511d4373: Pull complete
# 90edf2d312fb: Pull complete
# 06c0c9b8f03c: Pull complete                                                                                                                                                                                                       de5c517a4a38: Pull complete                                                                                                                                                                                                       c3b1e2de66ed: Pull complete
# d60ce4d201dd: Pull complete                                                                                                                                                                                                       a3cdd5646806: Pull complete
# 224f8359e493: Pull complete
# a1b532915622: Pull complete
# Digest: sha256:1433088e22d58d19222adbfd05b81d751d5a9f6098e39ee6c9b537709d78e362
# Status: Downloaded newer image for nvidia/cuda:11.7.1-cudnn8-runtime-ubuntu20.04
# docker.io/nvidia/cuda:11.7.1-cudnn8-runtime-ubuntu20.04
```

取得したイメージの確認には次のコマンドを使用します

```sh
docker images -a

# kakehi@igpu01:~$ docker images -a
# REPOSITORY    TAG                                 IMAGE ID       CREATED         SIZE
# nvidia/cuda   11.7.1-cudnn8-runtime-ubuntu20.04   c2342e6e8bfe   8 months ago    2.92GB
```

## 取得したDockerイメージからDockerコンテナの作成

```sh
docker run -it -v ~/data:/code --gpus all --name test-container nvidia/cuda:11.7.1-cudnn8-runtime-ubuntu20.04
```

オプションについて：

- **`-v ~/data:/code`**：ホストマシンのディスク領域をコンテナ内の`/code`ディレクトリにマウントします。例えば、ホストマシンの`~/data`ディレクトリがコンテナ内の`/code`ディレクトリと対応します。
- **`--name test-container`**：コンテナに名前を付けます。ここでは`test-container`という名前を使用しています。
- **`--gpus all`**：コンテナがホストマシンのすべてのGPUを使用できるようにします。