---
title: "Managing Storage"
weight: 32
---

# Managing storage

## Storage usage (per user)

To find out how much storage is being used by a particular user, run the following command.
You can find out the total capacity of a given directory.

```bash
sudo ncdu /home/[username]
```

## Storage usage (system-wide)

To check the system-wide storage usage, run the following command:

```bash
sudo df -h
```