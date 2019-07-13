---
title: Zarco/FAQ
permalink: wiki/Zarco/FAQ/
layout: wiki
redirect_from:
 - wiki/Cluster/FAQ
---

Software
--------

OpenJDK 1.8

GNU Compilers 7.2.0

GNU Tools 2.69

cmake 3.12.1

ffmpeg-static 4.1.4

OpenCV 3.2.0

CoreNLP 2018-10-05

trec_eval 9.0.6

Check for the availability of other software with `module avail`.

JupyterHub
----------

### Setup your own conda environment

```bash
conda env create -n myenv python=3.7 ipykernel
source activate myenv
```

Install the packages you need

```bash
conda install numpy scipy scikit-learn
```

Make it available in JupyterHub

```bash
python -m ipykernel install --user
```

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
