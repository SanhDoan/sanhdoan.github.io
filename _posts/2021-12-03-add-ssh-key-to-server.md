---
title: Add ssh key to remote server
author: Sanh Doan
date: 2021-12-03 22:42:00 +0700
categories: [SSH]
tags: [SSH]
---

### 1. Copy ssh key to server
```
ssh-copy-id -i ~/.ssh/id_rsa.pub root@1.2.3.4
```
It will ask your password. Please input it

### 2. (Optional) Disable password authentication for SSH
Find `PasswordAuthentication` in file `/etc/ssh/sshd_config` and change value from `yes` to `no`
```
PasswordAuthentication no
```
```
service ssh restart
```
