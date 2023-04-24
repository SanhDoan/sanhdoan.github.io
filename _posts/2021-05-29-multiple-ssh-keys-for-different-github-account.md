---
title: Setup multiple SSH keys for different Github account
author: Sanh Doan
date: 2021-05-29 07:27:00 +0700
categories: [Git]
tags: [Git, SSH]
---

For example: you have a repo in private organization `myteamprivate` with url `git@github.com:myteamprivate/repo-api.git`

## 1. Create ssh key on your machine

```bash
$ ssh-keygen -t rsa -C "your_email@youremail.com"
```

- Your email can be the same email with other accounts
- File name format: `id_rsa_[private organization]`
  ![ssh-keygen](https://i.imgur.com/ENKFiuk.png)

## 2. Modify ssh config

```bash
$ vi ~/.ssh/config
```

Then add below config

```bash
# "myteam" can be whatever, it'll be used when you clone repo
Host github.com-myteam
	HostName github.com
  AddKeysToAgent yes
	IdentityFile ~/.ssh/id_rsa_myteamprivate
  IdentitiesOnly yes
	User git
```

## 3. Copy public key and paste it in Github SSH Key

```bash
$ cat ~/.ssh/id_rsa_myteamprivate.pub | pbcopy
```

Then go to Github setting and paste it in `Key` input
![paste-ssh-github](https://i.imgur.com/mlIMWeH.png)

### Now you can clone the repo with SSH

```bash
$ git clone git@github.com-myteam:myteamprivate/repo-api.git
# "myteam" here is what you defined in ssh config Host
```

Note: you can change your config for repo by

```bash
$ git config user.name "Sanh Doan"
$ git config user.email "dpsanh@troodonlabs.com"
```

### Note: If the ssh-key not auto added, you need to add ssh-agent manually

```bash
$ eval $(ssh-agent)
$ ssh-add ~/.ssh/id_rsa_myteamprivate
```
