---
title: Watch command in MacOS terminal
author: Sanh Doan
date: 2021-08-10 18:03:00 +0700
categories: [Terminal]
tags: [Terminal, MacOS]
---

You want to follow command result continuously. Use `watch`

## 1. Install
```bash
brew install watch
```

## 2. Usage
```bash
watch -n <number_of_seconds> <command>
```
For example
```bash
watch -n 5 kubectl get all -o wide
```
The result of "kubectl get all -o wide" command will be reload every 5 seconds

![watch](https://imgur.com/CHMTYAX.png)
