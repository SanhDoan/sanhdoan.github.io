---
title: Multiple GIT remote repositories
author: Sanh Doan
date: 2021-04-30 11:33:00 +0700
categories: [Git]
tags: [Git]
---

## Context
You want to working with multiple Git repositories on one local source code.

## Config
For example: There are 2 repos
- Github: git@github.com:PhuSanh/test-a.git
- Gitlab: git@gitlab.com:dpsanh2348/test-b.git

Assuming that you already have github repo on your local machine
```bash
git clone git@github.com:PhuSanh/test-a.git
```

---
### Option 1: Config 1 remote for multiple repos
1. Create a new git remote `all`
```bash
git remote add all git@github.com:PhuSanh/test-a.git
```
- It can be any name
- Origin remote can be used as well


2. Register your push URLs
```bash
git remote set-url --add --push all git@github.com:PhuSanh/test-a.git
git remote set-url --add --push all git@gitlab.com:dpsanh2348/test-b.git
```

##### Result
- CHECK: `git remote -v`
![git-multiple-remote-all](https://i.imgur.com/X8GyHWE.png)
- PUSH: Now you can push to 2 repos at the same time
```bash
git push all <your branch>
```
![git-multiple-remote-push-all](https://i.imgur.com/NaGmZfq.png)
- PULL: can not pull from multiple remotes
- FETCH: can fetch all with `git fetch --all`

---
### Option 2: Config multiple remotes for multiple repos
1. Add new remote with `gitlab` and `github` name
Note: we can use existing `origin` remote for github
```bash
git remote add github git@github.com:PhuSanh/test-a.git
git remote add gitlab git@gitlab.com:dpsanh2348/test-b.git
```
- CHECK: `git remote -v`
![git-multiple-remote-check](https://i.imgur.com/gufiuOQ.png)
- PUSH
```bash
git push origin <your branch>
git push github <your branch>
git push gitlab <your branch>
```
- PULL
```bash
git pull origin <your branch>
git pull github <your branch>
git pull gitlab <your branch>
```
