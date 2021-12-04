---
title: Install nginx in Centos 7
author: Sanh Doan
date: 2021-12-04 10:44:00 +0700
categories: [Nginx, Centos]
tags: [Nginx, Centos]
---

### 1. (Optional) Run with sudo user
```shell
sudo su -
```

### 2. Install needed packages and nginx
```shell
yum install epel-release

yum update

yum -y install nginx
```

### 3. Start nginx
```shell
systemctl enable nginx

systemctl start nginx

systemctl status nginx
```

### Some useful commands
```shell
systemctl stop nginx

systemctl restart nginx

# Reload nginx after configuration is changed
systemctl reload nginx

# Turn off auto-start when restart VPS
systemctl disable nginx
```



