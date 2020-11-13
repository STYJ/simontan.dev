---
title: Private Messenger
date: 2019-07-03
tags:
  - projects
  - privacy
layout: layouts/post.njk
---

<img class="center" src="/img/private-messenger.png" alt="A screenshot of the user interface of the private messenger"/>

_Edit (6th Nov 2020): It seems like the messenger app is also no longer working since the "Connect Metamask" button broke from an upgrade on metamask's end..._ 😩 _I will get around to fixing it one of these days!_

## What is this project about?

I built a peer-to-peer messenging web app that focuses on privacy - more specifically, using your ethereum address as a unique identifier to your user and that none of the conversations are saved anywhere.

## Why did I do this?

I recently completed a [frontend course on udemy](https://www.udemy.com/course/the-complete-web-development-bootcamp/) (no, I'm not paid to promote this!) and I was curious to see how much I managed to absorb from the course.

I also wanted to build something that is related to privacy because of an increasing concern with digital privacy. It is quite scary how much our digital footprints reveal about us but yet, we put the safety and security of our data on the back burner because of the many benefits that we derive from using the internet.

## How did I do it?

This proof of concept web app was hacked together over a few weeks using:

- [metamask](https://metamask.io/) for connecting the app to your ethereum address
- [web3.js](https://web3js.readthedocs.io/en/latest/) for accessing your ethereum address programmatically
- [peerjs](https://peerjs.com/) for handling the peer-to-peer connection
- [vue.js](https://vuejs.org/) is the frontend framework used
- [veutify](https://vuetifyjs.com/en/) for its prebuilt UI components

## Extras

You can try out the demo [here](https://styj.github.io/private-messenger/) but I highly recommend running it locally instead i.e. clone the repo, spin up a local instance and voilà! The source code for this proof of concept can be found on [github](https://github.com/STYJ/private-messenger).
