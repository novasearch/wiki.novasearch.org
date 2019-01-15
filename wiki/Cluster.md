---
title: Cluster
permalink: wiki/Cluster/
layout: wiki
---

We are very fortunate to have a powerful computing cluster to aid in
research and development. Currently this cluster is composed by 4
identical rack-mounted (4u) computing nodes with GPGPU capability and an
additional Supermicro head node that serves as the frontend node. The
latter is used for issuing jobs or tasks, to be processed in the
cluster, and for management, coordination and distribution of said jobs
or tasks.

Software
--------

Rocks Cluster Distribution 6.2 (CentOS 6.10)

Network
-------

To access the cluster you need to log on to the SSH server on
193.136.122.132.

All the nodes are interconnected using a Gigabit switch (.local) and a
10GBit switch (.fast).

Master node
-----------

### Network

Host: 193.136.122.132

Internal: zarco.novasearch.org (10.1.1.1)

`         zarco.novasearch.org (10.10.1.1)`

### Hardware

|     |                                                                                    |
|-----|------------------------------------------------------------------------------------|
| MB  | Supermicro X9 Series                                                               |
| CPU | Intel Xeon E5-2620v2 CPU @ (6 cores, 12 threads, 15M cache 2.10GHz, up to 2.6 GHz) |
| RAM | 32 GB DDR3 ECC (1600Mhz)                                                           |

Computing nodes
---------------

### Network

compute-0-{0,1,2,3} (10.1.1.\*) (10.10.1.\*)

### Hardware

compute-0-0

|       |                                                                                         |
|-------|-----------------------------------------------------------------------------------------|
| MB    | ASUS P9X79 PRO                                                                          |
| CPU   | Intel Core i7-3930K Processor (6 cores, 12 threads, 12M cache, 3.2 GHz, up to 3.80 GHz) |
| RAM   | 64 GB DDR3 (1333Mhz)                                                                    |
| GPU 0 | NVIDIA GeForce GTX 1080 Ti 11GB                                                         |
| GPU 1 | NVIDIA GeForce GTX TITAN X 12GB                                                         |

compute-0-1

|       |                                                                                         |
|-------|-----------------------------------------------------------------------------------------|
| MB    | ASUS P9X79 PRO                                                                          |
| CPU   | Intel Core i7-3930K Processor (6 cores, 12 threads, 12M cache, 3.2 GHz, up to 3.80 GHz) |
| RAM   | 64 GB DDR3 (1333Mhz)                                                                    |
| GPU 0 | NVIDIA GeForce GTX 1080 Ti 11GB                                                         |
| GPU 1 | NVIDIA GeForce TITAN Xp 12GB                                                            |

compute-0-2

|       |                                                                                         |
|-------|-----------------------------------------------------------------------------------------|
| MB    | ASUS P9X79 PRO                                                                          |
| CPU   | Intel Core i7-3930K Processor (6 cores, 12 threads, 12M cache, 3.2 GHz, up to 3.80 GHz) |
| RAM   | 64 GB DDR3 (1333Mhz)                                                                    |
| GPU 0 | NVIDIA GeForce GTX 1080 Ti 11GB                                                         |
| GPU 1 | NVIDIA GeForce TITAN Xp 12GB                                                            |

compute-0-3

|       |                                                                                         |
|-------|-----------------------------------------------------------------------------------------|
| MB    | ASUS P9X79 PRO                                                                          |
| CPU   | Intel Core i7-3930K Processor (6 cores, 12 threads, 12M cache, 3.2 GHz, up to 3.80 GHz) |
| RAM   | 64 GB DDR3 (1333Mhz)                                                                    |
| GPU 0 | NVIDIA GeForce GTX 1080 Ti 11GB                                                         |
| GPU 1 | NVIDIA GeForce GTX TITAN X 12GB                                                         |

Security
--------

The cluster uses Rocks and its Single Sign-On solution.

Users homes are also mounted on all the computing nodes with NFS
allowing you to have access to your files on any node. Do however take
in mind that if you're doing any intensive IO work it is always better
to use a local folder on the computing node. Usually the norm is to use
the root directory /tmp however all the files in this directory are
removed upon reboot, so consider creating a new folder with your
username inside the root directory /state/partition1 and use that
instead if you want your data to persist.
