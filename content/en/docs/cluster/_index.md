---
title: "Using GPUs"
weight: 20
bookFlatSection: true
---

# Using GPUs

Please follow the steps below to run your jobs on GPUs:

## Check usage status

Make sure no one else is using the resource you want to use.

- Check the [#use_computer](https://omuiserver.slack.com/archives/C07CEM8HT1D) channel
- Run `nvidia-smi` command on the server and check the usage status
- Check the [GPU monitoring tool](/docs/cluster/monitoring)

## Declare when you use

Send a message in the [#use_computer](https://omuiserver.slack.com/archives/C07CEM8HT1D) channel and declare your usage.
    
{{< hint info >}}
**Message format**

using `[nodename] (device: [device ID])` for `[term]`

**Example**

using `igpu01 (device: 0)` for a while
{{</ hint >}}

## When you finished running your jobs

Please click the *released* emoji on your message.