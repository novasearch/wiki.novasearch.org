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
