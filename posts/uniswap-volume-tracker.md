---
title: Uniswap Volume Tracker
date: 2020-11-26
tags:
  - projects
  - uniswap
layout: layouts/post.njk
---

<img src="/img/uniswap-volume-tracker.png" alt="A screenshot of the uniswap volume tracker in action"/>

## What is this project about?

I wrote a script to monitor the buy and sell volumes on uniswap. It sums the buy / sell volume traded across different intervals and compares between them. This is analogous to moving averages and comparing the MAs.

## Why did I do this?

There's a lot of data on the blockchain that can help provide more information / insight before taking certain positions in a trade. Fundamentally, if buy volume is greater than sell volume for an extended period of time then we should see an appreciate in price. That was the goal behind the project - to compare between the different timeframes e.g. 100 blocks vs 10000 blocks for supplementing one's knowledge before trading.

## How did I do it?

Since I wanted to learn rust, this project was made with rust. I used the [rust-web3](https://github.com/tomusdrw/rust-web3) crate for interacting with the Ethereum blockchain.

## Extras

Since this is just a script, there is no UI deployed anywhere. If you want to try it out, clone the [repo](https://github.com/STYJ/Uniswap-volume-tracker), create your `.env` file and run `cargo run`. There are a few extensions / optimisations that I will consider implementing if there is demand for it.