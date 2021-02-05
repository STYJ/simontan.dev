---
title: HDB Resale Price Dashboard
date: 2021-01-19
tags:
  - projects
  - data analytics
layout: layouts/post.njk
---

<img src="/img/hdb-resale-price.png" alt="A screenshot of the HDB Resale Price dashboard"/>

_Simon: I have deactivated UpTimeRobot for this app so if you want to try out the app, please be aware that it will take a little longer than normal to load since the dynos are starting up. If it still doesn't work, refresh the browser and it should work._

## What is this project about?

The HDB Resale Price dashboard is a simple dashboard to show users some statistics regarding the resale price of HDBs in Singapore over the last 5 years (Jan 2015 - Nov 2020).

## Why did I do this?

I wanted to learn more about creating interactive charts so I decided to play around with the [plotly](https://plotly.com/) library.

## How did I do it?

As mentioned earlier, I used plotly for creating the charts. The frontend is done with another plotly application called [Dash](https://plotly.com/dash/). The dataset is sourced from [data.gov.sg](https://data.gov.sg/dataset/resale-flat-prices). The entire application is hosted on Heroku but since I'm on the hobby price plan, I had to also rely on something like [UpTimeRobot](https://uptimerobot.com/) to ping the website every 5 minutes to prevent it from sleeping.

## Extras

The source code for the dashboard can be found in this [github repo](https://github.com/STYJ/hdb-resale-price-deployment-files). The website is running [here](https://hdb-resale-price.herokuapp.com). If you're looking for a new HDB or planning to sell your own, I hope that this dashboard will be useful for you! 