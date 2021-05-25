---
title: Analysing $STAKE token transfers
date: 2021-01-30
tags:
  - projects
  - data analytics
layout: layouts/post.njk
draft: true
---

<img src="/img/breakdown-top-20-stake-holders.png" alt="A breakdown of the top 20 stake holders by application."/>

## What is this project about?

This project contains a _somewhat_ in depth analysis of the STAKE token tranfers. I analysed the distribution of STAKE tokens over time and across applications and aggregated overall holdings.

## Why did I do this?

I am a baghodler of STAKE tokens lol so I wanted to understand more about STAKE to figure out why it keeps dumping in price. Yes, I figured out why it keeps dumping in price.

## How did I do it?

Most of my data comes from pulling the data off the Ethereum blockchain with [web3.py](https://web3py.readthedocs.io/en/stable/overview.html). I also used [plotly](http://plotly.com/) for creating the charts because I wanted to gain more experience with it. Initially I had plans to deploy this as a dashboard but decided to scrap that idea since I don't have enough free dyno hours on Heroku.

## Extras

The source code for this analysis can be found in this [github repo](https://github.com/STYJ/Analysing-STAKE-token-transfers). Follow the instructions on `README.md` if you want to look at the analysis. I am still considering whether or not I should buy a raspi 4 to host it but I will update here if I do host it somewhere.