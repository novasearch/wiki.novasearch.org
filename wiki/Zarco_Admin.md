---
title: Zarco/Admin
permalink: wiki/Zarco/Admin/
layout: wiki
redirect_from:
 - wiki/Cluster/Admin
---

Users
-----


### Add a new user

📖 **Important: Make sure /state/partition1/usr0 is mounted.**

```bash
adduser USER
passwd USER
rocks sync users
```

NVIDIA and CUDA Drivers
-----------------------

📖 **Info: [NVIDIA repo mirror based on sdsc/cuda-roll](https://github.com/nscr/cuda-roll).**

### Update the packages available in the repository

```bash
cd /state/partition1/zarco/cuda-roll
make mirrorrepo
make createroll
rocks remove roll cuda-rhel6
rocks add roll cuda-rhel6-*.x86_64.disk1.iso
cd /export/rocks/install/
rocks create distro
```

### Update all computing nodes

```bash
rocks run host 'hostname && yum check-update'
rocks run host 'hostname && yum update'
rocks run host 'hostname && reboot'
```

#### Reboot if needed

```bash
rocks run host 'hostname && reboot'
```

Maintenance CentOS 6.x
----------------------

### Keeping the head node updated

```bash
yum check-update --enablerepo=base,updates,epel,nodesource-el6,WANdisco-git,WANdisco-svn
yum update --enablerepo=base,updates,epel,nodesource-el6,WANdisco-git,WANdisco-svn
```

### Keeping computing nodes updated

Try updating one of the computing nodes first. Say `compute-0-0`:

```bash
ssh compute-0-0
yum check-update --enablerepo=base,updates
yum update --enablerepo=base,updates
```

If everything is working proceed to the other nodes:

```bash
rocks run host 'hostname && yum check-update --enablerepo=base,updates,epel,nodesource-el6,WANdisco-git,WANdisco-svn'
rocks run host 'hostname && yum update --enablerepo=base,updates,epel,nodesource-el6,WANdisco-git,WANdisco-svn'
```

#### Reboot if needed

```bash
rocks run host 'hostname && reboot'
```
