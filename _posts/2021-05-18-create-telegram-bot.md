---
title: Create telegram bot to send service notification/alert
author: Sanh Doan
date: 2021-05-18 09:00:00 +0700
categories: [Telegram]
tags: [Telegram, Bot]
---


## 1. Search for BotFather in search box
![telegram-search-botfather](https://i.imgur.com/zaIRWbe.png)


## 2. Create a new bot
Note 1: You can type `/start` for get all commands
- Type `/newbot` in a message box
- Type your bot name (whatever you want)
- Type your bot username (must have suffix `_bot`)
![telegram-create-newbot](https://i.imgur.com/QEinMMY.png)


## 3. Create a channel
Create a channel so that your bot can send alert/notification to telegram

### 3.1 Set your bot as an admin
![telegram-set-bot-admin](https://i.imgur.com/mKVL2q1.png)

### 3.2 How to get your channel id
1. Go to [here](https://web.telegram.org?target=_blank)
2. Click on your channel
3. Look at the URL and find the part that looks like `c1234567890_1234567890123456789`
4. Get the string before underscore --> `c1234567890`
5. Remove the prefixed letter --> `1234567890`
6. Add prefix with a `-100` --> your channel id is `-1001234567890`


Now you can use your
- Bot ID
- Bot username
- Channel ID
and [Telegram API](https://core.telegram.org) to receive message/notification/alert from your services
