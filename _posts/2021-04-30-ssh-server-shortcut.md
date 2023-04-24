---
title: SSH server shortcut
author: Sanh Doan
date: 2021-04-30 09:00:00 +0700
categories: [SSH]
tags: [SSH]
---

Edit file ~/.ssh/config (create if not exist)

```
Host myserver
	Hostname 192.168.1.100 (or server domain: abc.com)
	User root
	Port 4444
```

- Host: Any name you want, easy to remember (ex: project name)
- Hostname: IP server (or server domain)
- User: username to access server
- IdentityFile: SSH public key, default is ~/.ssh/id_rsa
- Port: port ssh of server, default is 22
- ServerAliveInterval: server connect timeout
- ProxyCommand: special command when connect to server