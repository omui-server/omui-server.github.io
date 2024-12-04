---
title: "Proxy Settings"
weight: 22
---

# Proxy Settings

Due to the policy of the University's Information Infrastructure Center, the OMUI Server requires a proxy server to access the Internet.
Here, we explain how to set up a proxy for Git and Docker, which are often used when using the server.

## Git

When communicating with remote repositories such as GitHub, you need to go through a proxy.
There are two ways to communicate with GitHub: HTTPS and SSH, and the proxy settings are different for each.

### HTTPS

Environment variables are set for all users in advance (pre-configured in `/etc/environment`), so no additional settings are required.

### SSH

If you want to access a remote repository via SSH, add the following settings to `$HOME/.ssh/config`.

```text
Host github.com
  HostName github.com
  User [GitHub username]
  Port 443
  ProxyCommand connect -H http://proxy11.omu.ac.jp:8080 %h %p
```

## Docker

You need to go through a proxy when using Docker.
The proxy settings are different when pulling Docker Images, building them, and accessing the Internet within a Docker container, so refer to the following methods to set them up.

### Pulling Docker Images

Proxy settings are automatically configured when running `rootless-docker-install`, so no additional settings are required.

{{< hint warning >}}
If you ran `rootless-docker-install` before 2024/11/25, stop Docker with `systemctl --user stop docker.service` and run `rootless-docker-install` again.
{{< /hint >}}

### Building Docker Images and Accessing the Internet in Docker Containers

There are two ways to set up a proxy.
One way is to pass environment variables as options to the `docker container run` command or write environment variables in a Dockerfile or `docker-compose.yml`.
The other way is to write proxy settings in Docker's user configuration file.
Here, we introduce the second method.

You can access the Internet through a proxy by adding the following to `$HOME/.docker/config.json`.

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
We are planning to configure the settings automatically in the future.
{{< /hint >}}

## Environment Variables

The following environment variables are set for all users to use, so please use them.

```env
http_proxy="http://proxy.omu.ac.jp:8080/"
HTTP_PROXY="http://proxy.omu.ac.jp:8080/"
https_proxy="http://proxy.omu.ac.jp:8080/"
HTTPS_PROXY="http://proxy.omu.ac.jp:8080/"
no_proxy="localhost,127.0.0.1"
```

## References

- [Qiita - httpプロキシサーバがわかればGitHubは使える](https://qiita.com/n_slender/items/30db800aad7eb193c07e)
- [Zenn - Docker のプロキシ設定は割と地獄](https://zenn.dev/wsuzume/articles/f9935b47ce0b55)
