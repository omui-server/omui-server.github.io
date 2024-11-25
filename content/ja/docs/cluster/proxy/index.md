---
title: "プロキシの設定"
weight: 25
---

# プロキシの設定

OMUI Serverでは、インターネットにアクセスするためにプロキシサーバーを経由する必要があります。

DockerやGitなど、インターネットにアクセスする際に接続に失敗する場合は、以下のプロキシサーバーを設定してください。

```text
http://proxy.omu.ac.jp:8080
```

また、すべてのユーザが使用可能な環境変数として以下を設定していますので、ご利用ください。

```env
http_proxy="http://proxy.omu.ac.jp:8080/"
HTTP_PROXY="http://proxy.omu.ac.jp:8080/"
https_proxy="http://proxy.omu.ac.jp:8080/"
HTTPS_PROXY="http://proxy.omu.ac.jp:8080/"
no_proxy="localhost,127.0.0.1"
```
