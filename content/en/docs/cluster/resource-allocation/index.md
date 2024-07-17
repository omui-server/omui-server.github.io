---
title: "Resource Allocation"
weight: 22
---

# Resource allocation

The `docker container run` command provides options for allocating compute resources.

## GPU allocation

You can specify the GPUs to be used.
By default (no specification), no GPUs are allocated.
Please check the device IDs by running the `nvidia-smi` command on the server.
For example, `igpu01` has four GPUs, each assigned a device ID from 0 to 4.

{{< hint warning >}}
To avoid resource conflicts, please use device IDs to specify GPUs.
Use `--gpus all` only if you want to use all GPUs.
{{</ hint >}}

```bash
--gpus [Device ID of the GPU to be used / all]
# e.g. Single GPU (device 0 is specified)
--gpus '"device=0"'
# e.g. Multi-GPUs (specify device 0 and 2)
--gpus '"device=0,2"'
# e.g. When using all GPUs
--gpus all
```

## Shared memory allocation

Shared memory is used for pre-processing and other processes that do not use the GPUs.
The default (no specification) allocates only 64 MB, which often results in insufficient memory, so it is recommended to specify this.

```bash
--shm-size [memory size]
# e.g.
--shm-size 16gb
```

## CPU allocation

You can allocate the required amount of CPUs.
The default (unspecified) will use all CPUs.

```bash
--cpus [amount of CPUs]
# e.g.
--cpus 2
```

## Timeout time

You can set a timeout period (in seconds) before the container is stopped.

```bash
--stop-timeout [timeout time]
# e.g. Stops in 1 hour
--stop-timeout 3600
```