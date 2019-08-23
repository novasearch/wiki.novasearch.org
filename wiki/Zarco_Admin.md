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

📖 **Important: Make sure /state/partition1/home is mounted before.**

```bash
mount nas-0-0.fast:/usr0 /state/partition1/home
```

```bash
adduser USER
passwd USER
```

Certain things are barred to users unless they are part of the `zarco-users` group.

```bash
usermod -a -G zarco-users USER
```

Admins need to be part of the `admin` group as well.

```bash
usermod -a -G admin USER
```

Finally you can make it official to the whole cluster by issuing

```bash
rocks sync users
```

The `rocks sync users` also takes care of configuring the `automount` mount points for the user home. It does not know about the 10GbE network `.fast` so the NFS mounts for homedirs will go through the FastEthernet network `.local` initially. You can edit `/etc/auto.home` and change to the `.fast` network. Don't forget to then run `rocks sync users` again.

NVIDIA and CUDA Drivers
-----------------------

📖 **Info: [NVIDIA repo mirror based on sdsc/cuda-roll](https://github.com/nscr/cuda-roll).**

### Re-create the repository roll with up-to-date packages

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

### Keeping the head node up-to-date

```bash
yum check-update --enablerepo=base,updates,epel,nodesource-el6,WANdisco-git,WANdisco-svn
yum update --enablerepo=base,updates,epel,nodesource-el6,WANdisco-git,WANdisco-svn
```

### Keeping the computing nodes up-to-date

Try updating one of the computing nodes first. Say `compute-0-0`:

```bash
ssh compute-0-0
yum check-update --enablerepo=base,updates,epel,nodesource-el6,WANdisco-git,WANdisco-svn
yum update --enablerepo=base,updates,epel,nodesource-el6,WANdisco-git,WANdisco-svn
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
