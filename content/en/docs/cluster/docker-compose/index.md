---
title: "Docker Compose"
weight: 25
---

# Docker Compose

{{< hint info >}}
Under construction...
{{</ hint >}}

## `docker-compose.yml` の作成

`docker-compose.yml`ファイルを作成します。このファイルには、使用するDockerイメージと、作成するコンテナの設定を記述します。

```yaml
# docker-compose.yml

services:
  project:
    image: nvidia/cuda:12.5.1-cudnn-devel-ubuntu22.04
    container_name: experiment
    volumes:
      - $PWD:$PWD
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              device_ids: ['0']
              capabilities: [gpu]
```

## コンテナの起動

`docker-compose.yml` を作成したディレクトリで、以下のコマンドを実行してコンテナを起動します。

```bash
$ docker compose up
```

代表的なオプションとして次のようなものがあります。
```bash
# デタッチ (バックグラウンドで実行)
-d
```

## コンテナの確認

コンテナが正しく起動しているか確認するには、以下のコマンドを使用します。

```sh
docker compose ps

# Name              Command             State               Ports
# ----------------------------------------------------------------------------
# test-container    "/bin/sh -c 'while t …"   Up      0.0.0.0:1888->1888/tcp
```

## コマンドの実行

```bash
$ docker compose exec [options] [-e KEY=VAL...] [--] SERVICE COMMAND [ARGS...]
```