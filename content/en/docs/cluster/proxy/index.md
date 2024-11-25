---
title: "Proxy Settings"
weight: 25
---

# Proxy Settings

OMUI Server requires a proxy server to access the Internet.

If you fail to connect when accessing the Internet, such as Docker and Git, please set the following proxy server.

```text
http://proxy.omu.ac.jp:8080
```

In addition, the following environment variables are set for all users to use, so please use them.

```env
http_proxy="http://proxy.omu.ac.jp:8080/"
HTTP_PROXY="http://proxy.omu.ac.jp:8080/"
https_proxy="http://proxy.omu.ac.jp:8080/"
HTTPS_PROXY="http://proxy.omu.ac.jp:8080/"
no_proxy="localhost,127.0.0.1"
```
