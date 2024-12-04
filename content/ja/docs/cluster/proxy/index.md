---
title: "プロキシの設定"
weight: 22
---

# プロキシの設定

大学の情報基盤センターのポリシーにより、OMUI Serverではインターネットにアクセスする際にプロキシサーバーを経由する必要があります。
ここでは、サーバー利用時によく使用するGitやDockerにおけるプロキシの設定方法を説明します。

## Git

GitHubなどのリモートリポジトリと通信する際にプロキシを経由する必要があります。
GitHubとの通信方法にはHTTPSとSSHがありますが、それぞれプロキシの設定方法が異なりますので、以下の方法を参考に設定してください。

### HTTPS

全ユーザに対してあらかじめ環境変数を設定しています ( `/etc/environment` に記載 ) ので、追加の設定は不要です。

### SSH

SSH経由でリモートリポジトリにアクセスする場合は、　`$HOME/.ssh/config` に以下の設定を追加してください。

```text
Host github.com
  HostName github.com
  User [GitHubのユーザ名]
  Port 443
  ProxyCommand connect -H http://proxy11.omu.ac.jp:8080 %h %p
```

## Docker

Dockerを使用する際にプロキシを経由する必要があります。
Docker Imageのpull、ビルド時、Dockerコンテナ内でのインターネットアクセスでプロキシ設定が異なりますので、以下の方法を参考に設定してください。

### Docker Imageのpull

`rootless-docker-install` 実行時に自動的にプロキシ設定が行われますので、追加の設定は不要です。

{{< hint warning >}}
2024/11/25以前に `rootless-docker-install` を実行した場合は、 `systemctl --user stop docker.service` でDockerを停止し、 `rootless-docker-install` を再度実行してください。
{{< /hint >}}

### Docker Imageのビルド時およびDockerコンテナ内でのインターネットアクセス

2通りの方法でプロキシを設定できます。
一つは、 `docker container run` コマンドのオプションで環境変数を渡す方法や、Dockerfileまたは`docker-compose.yml`に環境変数を記述する方法です。
もう一つは、Dockerのユーザ設定ファイルにプロキシ設定を記述する方法です。
ここでは、二つ目の方法を紹介します。

`$HOME/.docker/config.json` に以下を記述することでプロキシを経由してインターネットにアクセスできます。

```json
{
 "proxies": {
   "default": {
     "httpProxy": "http://proxy11.omu.ac.jp:8080",
     "httpsProxy": "http://proxy11.omu.ac.jp:8080",
     "noProxy": "localhost,127.0.0.0/8"
   }
 }
}
```

{{< hint info >}}
将来的には、ユーザがログイン時に自動的に設定されるようになる予定です。
{{< /hint >}}

## 環境変数

全てのユーザが使用可能な環境変数として以下をあらかじめ設定していますので、ご利用ください。

```env
http_proxy="http://proxy11.omu.ac.jp:8080/"
HTTP_PROXY="http://proxy11.omu.ac.jp:8080/"
https_proxy="http://proxy11.omu.ac.jp:8080/"
HTTPS_PROXY="http://proxy11.omu.ac.jp:8080/"
no_proxy="localhost,127.0.0.1"
```

## 参考

- [Qiita - httpプロキシサーバがわかればGitHubは使える](https://qiita.com/n_slender/items/30db800aad7eb193c07e)
- [Zenn - Docker のプロキシ設定は割と地獄](https://zenn.dev/wsuzume/articles/f9935b47ce0b55)