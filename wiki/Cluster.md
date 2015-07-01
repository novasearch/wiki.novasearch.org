---
title: Cluster
permalink: wiki/Cluster/
layout: wiki
---

We are very fortunate to have a powerful computing cluster to aid in
research and development. Currently this cluster is composed by 4
identical rack-mounted (4u) computing nodes with GPGPU capability and an
additional tower computer that serves as the master node. The latter is
used for issuing jobs or tasks, to be processed in the cluster, and for
management, coordination and distribution of said jobs or tasks. It is
also used occasionally to host internet-facing demos of our work.

Our nodes are named after characters in Science-Fiction works. Flavio
Martins unilaterally decided to start with the characters from the
Christopher Nolan movie "Inception".

Network
-------

To access the cluster you need to log on to the SSH server on
193.136.122.72.

All the nodes are interconnected using a high-performance Gigabit
switch.

Master node
-----------

### Network

Host: 193.136.122.72

Internal: ariadne.novasearch.org (192.168.1.1)

### Software

Ubuntu 12.04.2 LTS + 14.04 Hardware Enablement Stack

The Hardware Enablement Stack contains backported kernels and Xorg
packages from Ubuntu 14.04.

### Hardware

|     |                                                                                      |
|-----|--------------------------------------------------------------------------------------|
| MB  | Intel DX58SO                                                                         |
| CPU | Intel Core i7-920 Processor (4 cores, 8 threads, 8M Cache, 2.66 GHz, up to 2.93 GHz) |
| RAM | 12 GB DDR3 (1066Mhz)                                                                 |

Computing nodes
---------------

### Network

arthur (192.168.1.10)

cobb (192.168.1.20)

mal (192.168.1.30)

saito (192.168.1.40)

### Software

Ubuntu 12.04.2 LTS + 12.10 Hardware Enablement Stack

The Hardware Enablement Stack contains backported kernels and Xorg
packages from Ubuntu 12.10.

### Hardware

|     |                                                                                         |
|-----|-----------------------------------------------------------------------------------------|
| MB  | ASUS P9X79 PRO                                                                          |
| CPU | Intel Core i7-3930K Processor (6 cores, 12 threads, 12M Cache, 3.2 GHz, up to 3.80 GHz) |
| RAM | 64 GB DDR3 (1333Mhz)                                                                    |
| GPU | 2 x AMD Radeon HD 7950 3 GB                                                             |

Security
--------

The cluster has Single Sign-On configured using a combination of LDAP
and Kerberos. User account and groups management is handled by LDAP on
the master node.

Kerberos allows users who authenticate with the master node to obtain
tickets to access other all the other nodes with SSH.

Users homes are also mounted on all the computing nodes with NFS
allowing you to have access to your files on any node. Do however take
in mind that if you're doing any intensive IO work it is always better
to use a local folder on the computing node. Usually the norm is to use
the root directory /tmp however all the files in this directory are
removed upon reboot, so consider creating a new folder with your
username inside the root directory /localstore and use that instead if
you want your data to persist.

For users using key-based authentication, additional steps must be
performed to ensure that the tickets are available and renewed on each
machine:

-   On Ariadne run:

  
  
`kinit -r 14d`

-   On the remaining machines run:

  
  
`krenew -b -K 120`
