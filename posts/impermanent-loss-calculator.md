---
title: Impermanent Loss Calculator
date: 2020-10-18
tags:
  - projects
  - uniswap
layout: layouts/post.njk
---

<img src="/img/impermanent-loss-calculator.png" alt="A screenshot of the user interface of my impermanent loss calculator app" style="width: 50%;"/>

## What is this project about?

I built an impermanent loss (IL) calculator to help others and myself to calculate the [impermanent loss](https://finematics.com/impermanent-loss-explained/) of supplying liquidity to constant product market makers like [Uniswap](https://uniswap.org/) and [Balancer](https://balancer.finance/).

## Why did I do this?

I was once burnt by impermanent loss when I was farming for sushi tokens with the ETH/BAND pair on uniswap. There was a sudden dump in the overall crypto market and my profits from farming sushi was barely enough to cover my losses. I decided that if I wanted to consider providing liquidity as a means of diversification then I need to better understand how IL works.

## How did I do it?

I tried to keep it as simple as possible so I only used [sapper](https://sapper.svelte.dev/) as my frontend framework. The math behind the impermanent loss calculation can be found in these articles written by [pintail](https://pintail.medium.com/uniswap-a-good-deal-for-liquidity-providers-104c0b6816f2) and [balancer](https://medium.com/balancer-protocol/calculating-value-impermanent-loss-and-slippage-for-balancer-pools-4371a21f1a86).

## Extras

This IL calculator works for any 2 pools with different weighting as opposed to the default 50:50. Moreoever, it allows you to specify actual prices (token A in terms of token B) instead of just percentage changes. Based on the initial token supplied, initial price and current price, it can also calculate the remaining inventory after you subtract away impermanent loss!

Note that I limited it to 2 pools because that is the most common combination. Moreover, calculating remaining inventory after impermanent loss for more than 2 pools is really hard... (T＿T) Anyway, unlike my other projects, I don't think this project will break because there are almost no dependencies involved. I guess as long as netlify doesn't go down, all is good. Try out the calculator [here](https://impermanent-loss-calculator.netlify.app/) and let me know what you think!