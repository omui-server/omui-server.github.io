---
title: "Docker"
weight: 21
---

# Docker

{{< hint warning >}}
OMUI ServerにはPythonがあらかじめインストールされています。
そのため、Dockerを使わなくてもvenvなどを使って仮想環境を作ることができますが、Pythonのバージョンが古い可能性があるためおすすめしません。
{{</ hint >}}

ここでは、Dockerの基本的な使い方を説明します。
Dockerについて詳しく知りたい場合は [公式ドキュメント](https://docs.docker.com/) などを確認してください。

## Rootless Dockerの設定

{{< hint info >}}
一度のみ行ってください。インストール済みの場合は不要です
{{</ hint >}}

OMUI Serverでは [Rootless Docker](https://docs.docker.com/engine/security/rootless/) を導入しています。
Rootless Dockerを使うことで、ユーザーごとにDockerコンテナやDockerイメージの管理が可能になります。
以下のコマンドを実行し、Rootless Dockerの設定を行ってください。

```bash
$ rootless-docker-install
```

## Docker コンテナ

```bash
$ docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]
```
を実行すると、Dockerコンテナを新規作成し、コンテナ内で `[COMMAND]` を実行します。

代表的なオプションとして次のようなものがあります。
```bash
# コンテナ終了時に、自動的に削除
--rm

# SRCをDSTにバインドマウントする
--volume SRC:DST

# コンテナ内の作業ディレクトリのパス
--workdir PATH

# GPUの割り当て
--gpus DEVICE
```

以下の例は、 [Docker Hub](https://hub.docker.com/) で公開されている `nvidia/cuda:12.5.1-cudnn-devel-ubuntu22.04` というDockerイメージを用い、コンテナ内で `nvidia-smi` コマンドを実行する例です。

```bash
$ docker container run \
  --rm \
  --gpus '"device=0"' \
  nvidia/cuda:12.5.1-cudnn-devel-ubuntu22.04 \
  nvidia-smi
```

## Docker イメージ

Dockerイメージを用意するには、Dockerfileを使って自分で一からDockerイメージを作成するか、Dockerレジストリから取得する必要があります。
代表的なレジストリとして、 [Docker Hub](https://hub.docker.com/) や [NVIDIA NGC カタログ](https://catalog.ngc.nvidia.com/containers) があります。

{{< hint warning >}}
CUDA Toolkitが含まれるDockerイメージを選ぶ際は、イメージに含まれるCUDA Toolkitのバージョンに注意してください。
サーバー上で `nvidia-smi` コマンドを実行したときに右上に表示されるバージョンが、対応しているCUDA Toolkitの最新のバージョンです。

( `nvidia-smi` で表示されるバージョン ≦ CUDA Toolkitのバージョン)
{{</ hint >}}

取得済のイメージの確認には次のコマンドを使用します

```bash
$ docker images

REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    35a88802559d   5 weeks ago   78.1MB
```

Dockerイメージを削除するには次のコマンドを実行します。

```bash
$ docker image rm IMAGE
```

{{< hint warning >}}
使用しなくなったイメージは適宜削除するようにお願いします。
{{</ hint >}}

## 参考

- [Docker入門（第一回）～Dockerとは何か、何が良いのか～](https://knowledge.sakura.ad.jp/13265/)
- [実践 Docker - ソフトウェアエンジニアの「Docker よくわからない」を終わりにする本](https://zenn.dev/suzuki_hoge/books/2022-03-docker-practice-8ae36c33424b59)