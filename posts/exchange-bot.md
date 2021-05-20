---
title: Exchange bot
date: 2018-06-19
tags:
  - projects
  - bots
layout: layouts/post.njk
---

<img src="/img/exchange-bot.png" alt="A screenshot of the user interface of my exchange bot" style="width: 50%;"/>

## What is this project about?

I built a telegram bot to find the exchanges that offer the specified cryptocurrency as a trading pair. The bot will also return the 24 hour rolling volume for each exchange, sort the results according to price and also find the top traded pairs for each exchange.

## Why did I do this?

I was spending too much time trying to figure out which exchanges offer the trading pairs I am interested in since this process is entirely manual.

## How did I do it?

A friend (Jingkai) of mine recommended the [PythonTelegramBot](https://github.com/python-telegram-bot/python-telegram-bot) library to build the telegram bot. I had to also rely on web scraping via [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) because [CoinMarketCap](https://coinmarketcap.com/) (the website that I was pulling data from) did not offer free APIs that provided this.

## Extras

My exchange bot actually worked for a bit but because CoinMarketCap kept changing their frontend code structure, my web scraping algorithm would often break. It got to a point where almost every upgrade broke the bot and I was really annoyed so after a few months of usage (and declining interests in purchasing cryptocurrencies), I decided that I will no longer maintain the bot.

The [repo](https://github.com/STYJ/Exchange-Bot) is currently archived but you can fork the repo if you want to use it. Do note that it is **very** unlikely to work out of the box. You probably also want to first check if newer APIs have been introduced to CoinMarketCap or CoinGecko!
