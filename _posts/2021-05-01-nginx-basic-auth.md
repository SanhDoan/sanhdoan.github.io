---
title: Nginx basic authentication
author: Sanh Doan
date: 2021-05-01 09:30:00 +0700
categories: [Nginx]
tags: [Nginx]
---


## 1. Install tool
```bash
sudo apt-get install apache2-utils # (Debian, Ubuntu)
sudo yum install -y httpd-tools # (RHEL/CentOS/Oracle Linux)
```

## 2. Create password
```bash
sudo htpasswd /etc/nginx/.htpasswd user1 # Then type password at the prompt
```
Note: use `-c` for create the whole .htpasswd file from scratch


## 3. Nginx configuration
### Inside a location that you are going to protect
```bash
location /admin {
    auth_basic "Basic Auth"; # anything you want -> show in dialog user/password
    auth_basic_user_file /etc/nginx/.htpasswd; # File location store your password
    #...
}
```
### Limit access whole website but some areas
```bash
server {
    ...
    auth_basic           "Basic Auth";
    auth_basic_user_file /etc/nginx/.htpasswd; 

    location /public/ {
        auth_basic off;
    }
}
```

## 4. Reload nginx
```bash
sudo service nginx reload
```

---
## Use IP Address for Access Restriction
```bash
location /api {
    #...
    deny  192.168.1.2;
    allow 192.168.1.1/24;
    allow 127.0.0.1;
    deny  all;
}
```

## Combine Basic authentication and IP Address
```bash
location /api {
    #...
    satisfy all;    

    deny  192.168.1.2;
    allow 192.168.1.1/24;
    allow 127.0.0.1;
    deny  all;

    auth_basic           "Administrator’s Area";
    auth_basic_user_file conf/htpasswd;
}
```
- satisfy
    - all: access is granted if a client satisfies both conditions
    - any: access is granted if if a client satisfies at least one condition



Ref source: [Nginx doc](https://docs.nginx.com/nginx/admin-guide/security-controls/configuring-http-basic-authentication/)