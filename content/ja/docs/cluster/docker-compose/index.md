---
title: "Docker Compose"
weight: 41
bookFlatSection: true
---

# Docker Composeを用いた環境構築

ここでは、CUDA v.11.7.1とcuDNN v8、PyTorch、Ubuntu 22.04を使ったGPU環境の構築を行います。


## Docker Composeファイルの作成

次に、`docker-compose.yml`ファイルを作成します。このファイルには、使用するDockerイメージとコンテナの設定を記述します。

```yaml
version: '3.8'

services:
  gpu-service:
    image: nvidia/cuda:11.7.1-cudnn8-runtime-ubuntu20.04
    container_name: test-container
    ports:
      - "1888:1888"
    volumes:
      - ~/data:/code
    deploy:
      resources:
        reservations:
          devices:
            - capabilities: [gpu]
    environment:
      - NVIDIA_VISIBLE_DEVICES=all
      - NVIDIA_DRIVER_CAPABILITIES=compute,utility
```

## Docker Composeによるコンテナの起動

`docker-compose.yml`ファイルを作成したディレクトリで、以下のコマンドを実行してコンテナを起動します。

```sh
docker compose up -d

# Creating network "your_project_default" with the default driver
# Pulling gpu-service (nvidia/cuda:11.7.1-cudnn8-runtime-ubuntu20.04)...
# 11.7.1-cudnn8-runtime-ubuntu20.04: Pulling from nvidia/cuda
# ...
# Successfully built
# Successfully tagged your_project_gpu-service:latest
# Creating test-container ... done
```

## コンテナの確認

コンテナが正しく起動しているか確認するには、以下のコマンドを使用します。

```sh
docker compose ps

# Name              Command             State               Ports
# ----------------------------------------------------------------------------
# test-container    "/bin/sh -c 'while t …"   Up      0.0.0.0:1888->1888/tcp
```

## コンテナに接続

コンテナ内で作業を行いたい場合は、以下のコマンドでコンテナに接続できます。

```sh
docker exec -it test-container /bin/bash
```

## Docker Composeファイルのオプション説明

- **`version`**: Docker Composeファイルのバージョンを指定します。ここでは`3.8`を使用しています。
- **`services`**: 一つ以上のサービス（コンテナ）の設定を記述します。
- **`image`**: 使用するDockerイメージを指定します。ここでは`nvidia/cuda:11.7.1-cudnn8-runtime-ubuntu20.04`を使用しています。
- **`container_name`**: コンテナに名前を付けます。ここでは`test-container`という名前を使用しています。
- **`ports`**: ローカルマシンのポートとコンテナのポートをマッピングします。例ではローカルのポート`1888`をコンテナのポート`1888`にマッピングしています。
- **`volumes`**: ホストマシンのディスク領域をコンテナ内のディレクトリにマウントします。例では、ホストマシンの`~/data`ディレクトリがコンテナ内の`/code`ディレクトリと対応します。
- **`deploy`**: リソースの予約や制限を設定します。例では、GPUを使用するように設定しています。
- **`environment`**: 環境変数を設定します。ここでは、すべてのGPUを見えるようにし、必要なドライバー機能を有効にしています。