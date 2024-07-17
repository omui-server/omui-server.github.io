---
title: "Login"
weight: 11
---

# Login

{{< hint warning >}}
Please make sure that your client PC is connected to teacher segments or research group segments of the graduate school of informatics in OMU network.
{{</ hint >}}

Let's login to the server:

```bash
$ ssh [username]@172.26.43.2
```

## Change your password

{{< hint info >}}
It is recommended to change the initial password.
{{</ hint >}}

If you want to change the password, run the following command on the server:

```bash
$ passwd
```

## (Optional) SSH Public Key Authentication

{{< hint danger >}}
If you are connecting from a shared PC, do not do the following.
It may allow others to login with your credentials.
{{</ hint >}}

SSH public key authentication allows you to login to the server without entering your password everytime.

First, create a public/private key pair on the client PC.
You will be asked to set a passphrase.
If you don't want to login with your password, leave it blank and press `Enter`.

```bash
$ ssh-keygen
```

Next, copy the public key to the server.

```bash
$ ssh-copy-id [username]@172.26.43.2
```

Let's check if it works.
Run the following command and confirm that you can login without entering a password.

```bash
$ ssh [username]@172.26.43.2
```