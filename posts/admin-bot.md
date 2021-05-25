---
title: Admin Bot (CryptoSGBob)
date: 2018-11-27
tags:
  - projects
  - bots
layout: layouts/post.njk
draft: true
---

<img src="/img/CSGBob.png" alt="A screenshot of the user interface of CryptoSG Bob bot" style="width: 50%;"/>

## What is this project about?

I built a telegram bot that introduces a decentralised tribunal style approach to banning malicious users in a telegram group.

Instead of relying on a few trusted users with admin privileges, any user can initiate a vote on another member of the group by replying to their message with the `/bob` command. Other members of the community will vote to determine if the kick should be executed. It's fastest fingers first so the option (to kick or to save) that hits the voting threshold first will be executed.

## Why did I do this?

Milodino, the founder of [CryptoSG](https://t.me/cryptosg), first chanced upon [BanOfBot](https://github.com/backmeupplz/banofbot) (Bob) when he was looking for a free solution to decentralise the banning process. Bob worked as expected but it was lacking certain features e.g. limiting the number of bans per day, removing ban requests that are not completed within 24 hours.

## How did I do it?

Similar to my [exchange bot](../exchange-bot/), I used the [PythonTelegramBot](https://github.com/python-telegram-bot/python-telegram-bot) library to build the CryptoSGBob. I used a local variable to manage the current state of each proposal so if you reset the bot, all proposals will be gone since it is stored in memory... 😅

## Extras

If you are looking to introduce a similar bot into your telegram groups, I highly recommend that you use the original [BanOfBot](https://github.com/backmeupplz/banofbot) instead of my modified version.

BanOfBot is still (as of 5th Nov 2020) being upgraded, maintained and works for any groups but CryptoSGBob only works for CryptoSG affiliated groups. That said, the source code for CryptoSGBob can be found [here](https://github.com/Crypto-SG/CSGBob) if you're interested in it.
