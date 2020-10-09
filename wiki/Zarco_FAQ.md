---
title: Zarco/FAQ
permalink: wiki/Zarco/FAQ/
layout: wiki
redirect_from:
 - wiki/Cluster/FAQ
---

Working storage
---------------

### Where to store your files

📖 **Important: User homes are NFS mounted and shared by all nodes.**

```bash
/home/USER
```

#### Storage space on head node

```bash
/state/partition1/USER
```

#### Storage space on computing nodes

```bash
/state/partition1/USER
```

#### Storage space on computing nodes for experiments

📖 **Important: Fast SSD storage for IO-intensive workloads.**

```bash
/scratch/USER
```

Dataset storage
---------------

📖 **Important: These are NFS mounted and shared by all nodes.**

```bash
/nas/Public
/nas/Datasets
/nas/wamse
```

### PubMed Central Open-Access (Snapshot)

```bash
/nas/pmc
```

GPUs
----

### Why is Condor required to get GPUs/CUDA acceleration?

In essence, Condor allows sharing the GPU resources between all the users
and, as configured, is the only sanctioned way to use GPU acceleration (CUDA)
(i.e., processes launched directly via the command-line run on the CPU only).

We know it might take you a little bit of time to get acquainted with Condor,
however after a bit of trial and error you will appreciate it.
Here is a simple template for `condor_submit` to help you get started.

📖 **Important: Note the use of request_GPUs = 1.**

```bash
Universe  =  vanilla
GetEnv = True

Remote_Initialdir = /home/user/workspace
Executable = bin/myprogram
Arguments = -l 0.025 -dummy 0

RequestMemory = 2048
RequestCpus = 1
request_GPUs = 1

Output =  /home/user/workspace/myprogram.out
Error =  /home/user/workspace/myprogram.err

Queue
```

If the job is [H]eld or [I]dle when you check `condor_q`
use `condor_q -analyze JOB_ID` to get debug information.


Software
--------

Check for the availability of software with `module avail`.
