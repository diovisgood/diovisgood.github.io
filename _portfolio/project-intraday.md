---
date: 2021-09-29
title: "Intraday Project"
excerpt: "I created a gym compatible environment for reinforcement learning to train agents for intraday trading for different assets like stocks or cryptocurrencies."
categories: machine-learning
tags: gym numpy pandas pyglet python binance reinforcement-learning featured
sidebar:
  - title: "Period"
    text: "Jun 2021 - Sep 2021"
  - title: "Technologies"
    text: "**Gym**, **Numpy**, **Pandas**, **Pyglet**, **Python**, **Binance**"
---

I created a package which provides gym compatible environment to **simulate intraday trading**
based on stream of trades, either historical or real-time.

![gif animation of trained agent](/assets/img/intraday_ethusdt_trained2.gif)

This project was inspired by [TensorTrade](https://github.com/tensortrade-org/tensortrade){:target="_blank"},
but it was written from scratch, and it is a completely original source code.

The main idea was to go deeper from candles to the actual stream of trades.
Because candles lose a lot of information, for example:

- How many trades during a period were initiated by buyers or by sellers?
- At what price did most of the trades happen during a period?
- At what price there were almost no activity?
- Were there many trades with small amounts or less trades with big amounts?
- etc.

A lot of trained models seem to perform good during training,
but often fail to show any positive result in real trading.
I believe one of the reasons is that they do not take into account some important details, like:
- orders are executed with delays
- there is always a spread between bid and ask prices
- limit orders may not execute even if price *touches* them
- accounts are liquidated if they go bankrupt
- trades commissions

This project tries to simulate trading environment as realistically as possible.
This allows to train trading bots using reinforcement learning algorithms.

[Read the Full Story]({% post_url 2021-09-29-intraday %}){: .btn .btn--info}

[View Project on Github](https://github.com/diovisgood/intraday/){: .btn .btn--primary target="_blank"}
