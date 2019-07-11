---
title: Cluster/Admin
permalink: wiki/Cluster/Admin/
layout: wiki
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
