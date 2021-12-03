---
title: Install docker in Centos 7
author: Sanh Doan
date: 2021-12-03 23:27:00 +0700
categories: [Server, Centos]
tags: [Server, Docker, Centos]
---

### 1. Run with sudo user
```shell
sudo su -
```

### 2. Install needed packages and docker
```shell
yum -y update

yum -y install yum-utils device-mapper-persistent-data lvm2

yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

yum -y install docker-ce
```

### 3. Start docker
```shell
systemctl start docker

systemctl enable docker

systemctl status docker
```

### 4. Install docker compose
```shell
curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose

ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

docker-compose --version
```
