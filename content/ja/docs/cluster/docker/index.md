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

