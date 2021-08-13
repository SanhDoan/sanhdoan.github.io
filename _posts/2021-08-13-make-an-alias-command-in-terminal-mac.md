---
title: Make an alias command in MacOS
author: Sanh Doan
date: 2021-08-13 13:19:00 +0700
categories: [Terminal]
tags: [Terminal, MacOS]
---

Make an alias command in MacOS

### 1. Edit file
```bash
nano ~/.bash_profile
```
or
```bash
nano ~/.zshrc
```

### 2. Add this line to make an alias
```bash
alias <alias>='<actual command>'
```
For example
```bash
alias k='kubectl'
```

### 3. Refresh the shell environment
```bash
source ~/.bash_profile
```
or
```bash
source ~/.zshrc
```
