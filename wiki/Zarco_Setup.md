---
title: Zarco/Setup
permalink: wiki/Zarco/Setup/
layout: wiki
redirect_from:
 - wiki/Cluster/Setup
---


Anaconda Setup
--------------

### Install latest Anaconda distribution with Python 3.x

Set install directory to /share/apps/anaconda3.x

```bash
bash Anaconda3-xxxx.xx-Linux-x86_64.sh
```

Add new modulefile /share/apps/modulefiles/anaconda/3.x

```bash
#%Module1.0
setenv PYTHONROOT /share/apps/anaconda3.x
prepend-path PATH /share/apps/anaconda3.x/bin
#prepend-path LD_LIBRARY_PATH /share/apps/anaconda3.x/lib
#prepend-path LIBPATH /share/apps/anaconda3.x/lib
```

### JupyterHub Configuration

📖 **Repository: <https://github.com/nscr/zarco-jupyterhub>**

Install the following dependencies to the desired base environment:

```bash
source /share/apps/anaconda3.6/bin/activate
pip install git+https://github.com/jupyterhub/wrapspawner
pip install git+https://github.com/jupyterhub/batchpawner
```

```bash
git clone git@github.com:nscr/zarco-jupyterhub.git /etc/jupyterhub
cd /etc/jupyterhub
make install
```

The last command installs the init script for supervisord. You still need to bring the service up yourself.

```bash
supervisorctl reread
supervisorctl update
```

Check the status of the service with

```bash
supervisorctl status
```

NAS
---

### Adding the NAS as an appliance in Rocks

```bash
#!/bin/sh
#
# Add the QNAP-NAS file server to the cluster
#
echo "Add the QNAP-NAS file server to the cluster"
#rocks add host interface nas-0-0 iface=eth0 subnet=private ip=10.1.1.100 mac=00:08:9b:f6:5d:75
rocks list host | grep -q -w -e 'nas-0-0' || rocks add host nas-0-0
rocks list host interface nas-0-0 | grep -q -w -e 'eth0' || \
    rocks add host interface nas-0-0 iface=eth0
rocks set host interface subnet nas-0-0 iface=eth0 subnet=private
rocks set host interface ip     nas-0-0 iface=eth0 ip=10.1.1.100
rocks set host interface mac    nas-0-0 iface=eth0 mac=00:08:9b:f6:5d:75
#rocks add host interface nas-0-0 iface=eth0 subnet=private ip=10.1.1.100 mac=00:08:9b:f6:5d:75
rocks set host attr nas-0-0 arch x86_64
rocks set host attr nas-0-0 os linux
rocks set host attr nas-0-0 managed false
rocks set host attr nas-0-0 kickstartable no
rocks set host installaction nas-0-0 action=os
rocks set host boot nas-0-0 action=os
rocks sync config
```