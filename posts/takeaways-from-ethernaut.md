---
title: Top 3 takeaways from Ethernaut
date: 2020-04-10
tags:
  - ethereum
  - solidity
  - security
layout: layouts/post.njk
---

There are many tools to help new Solidity developers learn more about writing secure smart contracts, one of which is [Ethernaut](https://ethernaut.openzeppelin.com/).

Ethernaut is a series of challenges represented as levels and at each level, you are given a contract that you need to claim ownership of in order to complete the level. You must use whatever means possible to exploit the bug in the contract. These levels get progressively harder the higher you go.

Since I finally managed to beat every level of Ethernaut (but I am ashamed for taking so long!), I thought it might be a good idea to share my top 3 takeaways from completing this activity!

## 1. Examine all options thoroughly

Like they say...
> Don't play with fire if you don't want to get burned.

<img class="center" src="/img/floor-is-lava.gif" alt="A gif of a kid being carried on a rotating machine." style="width: 50%;">
<a href="https://media.giphy.com/media/60dMMoZ2Tc5IQ/giphy.gif">GIPHY</a>

This quote is especially applicable to new developers who might be frustrated with the limitations of Solidity and are looking for alternatives like [inline assembly](https://solidity.readthedocs.io/en/latest/assembly.html) without first considering all possible workarounds to the current constraints.

Solidity is a high level language like Python and Java so understandably, there are many well intended restrictions put in place to reduce the risk of an unintended bug in your smart contract. Yet despite all these, there are [many cool things](https://blog.polymath.network/solidity-tips-and-tricks-to-save-gas-and-reduce-bytecode-size-c44580b218e6) that you can do with Solidity that even an experienced developer might not be aware of!

While inline assembly gives you very fine-grained control and it is really [very cool](https://blog.ricmoo.com/wisps-the-magical-world-of-create2-5c2177027604), there are much fewer resources and help online. If you do decide to use it, be extra careful, verify your logic multiple times and don't forget to [KISS](https://en.wikipedia.org/wiki/KISS_principle)!

## 2. Keep up to date with best practices

When you learn about Solidity for the first time, chances are you would have stumbled upon what is known as "[solidity best practices](https://consensys.github.io/smart-contract-best-practices/recommendations/)". This is a community curated list of coding habits that are deemed to be safer.

It is imperative to remember that these best practices are not set in stone and might potentially change with each network upgrade. For example, prior to the Instanbul hardfork, `.send()` and `.transfer()` were considered the safer way to send ETH however, this is no longer true. It is now better to use `.call()` since it forwards all remaining gas to the receiving address. You can read more about this [here](https://diligence.consensys.net/blog/2019/09/stop-using-soliditys-transfer-now/). In fact, what is mentioned in this paragraph may no longer be relevant by the time you read this article!

## 3. Verify ALL assumptions regularly
My biggest takeaway from this activity is to try your best to identify all assumptions made and to verify them regularly. Let me give you a real life example to better illustrate my point.

Fulcrum was probably the next big lending platform in the DeFi space but unfortunately for the bZx team, they were on the receiving end of a [flash loan "attack"](https://bzx.network/blog/mea-culpa).

Essentially what happened was that a risk that the team assumed to be unlikely to happen due to high initial capital costs were negated by the introduction of flash loans. Flash loans allowed anyone to easily take out a huge loan without any credit history as long as you pay back the full loan amount + interest in a single transaction.

While the risk was identified and verified to be true prior to the release of flash loans, the team did not validate their assumptions again. That said however, everything is always correct in hindsight and we must be aware that even if the bZx team were to check their assumptions after the release of flash loans, it is not guaranteed to have prevented this incident. Nonetheless, we must still try our very best and to never be complacent.

This incident serves as a good reminder for all smart contract developers that even the most capable can make mistakes. But regardless of the short term damage, we will always bounce back and find a way to come out stronger than ever!

Thanks for reading and tread forward cautiously!