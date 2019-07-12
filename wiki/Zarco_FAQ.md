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
