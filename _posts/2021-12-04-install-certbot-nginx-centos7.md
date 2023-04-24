---
title: Install Certbot for Nginx in Centos 7
author: Sanh Doan
date: 2021-12-04 13:38:00 +0700
categories: [Certbot, Nginx, Centos]
tags: [Certbot, Nginx, Centos]
---

### 1. (Optional) Run with sudo user
```shell
sudo su -
```

### 2. Install needed packages and certbot
```shell
yum install epel-release

yum update

yum -y install certbot-nginx
```

### 3. Generate certificate
```shell
certbot --nginx -d redmine.sanhdoan.xyz
```

### 4. Create cronjob to auto renew
```shell
crontab -e

# Run cronjob auto renew at every 23h59. Do nothing if the certificate is not expire
59 23 * * * /usr/bin/certbot renew --quiet
```

### 5. (Optional) Update Diffie-Hellman to make certificate stronger
```shell
openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
```

Paste this line at anywhere in `server` block (in file **/etc/nginx/nginx.conf**)
```shell
ssl_dhparam /etc/ssl/certs/dhparam.pem;
```


