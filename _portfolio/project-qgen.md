---
date: 2019-05-29
title: "QGEN Project - Competing Genetic Algorithm"
excerpt: "This is a project I made trying new approach to find profitable trading strategies. I could not beat the market, but developed Competing Genetic Algorithm that can be useful for many other problems!"
categories: machine-learning
tags: genetic-algorithm evolution lua
sidebar:
  - title: "Period"
    text: "Apr 2019 - May 2019"
  - title: "Technologies"
    text: "**Genetic-Algorithm**, **Lua**"
---

**QGEN Project** was a project for the task of finding
new profitable _trading strategies_ in a financial market.
During my work on it, I developed the **Competing Genetic Algorithm**,
which can be used in many other areas of machine-learning.

The main idea is to represent in the **genetic code**
a sequence of mathematical operations of arbitrary length,
which would **compute predicted price movement** of some asset.
And then let genetic evolution do the job of **evolving this code**.

I have made some improvement to the classical genetic algorithm.
As it fails to develop more than one "specie" at a time.

My idea is that in most cases there could  be more than one good solution.
Why not search for them simultaneously?

I trained a bunch of trading agents and even tested them on a real broker's account.

[Read the Full Story]({% post_url 2019-05-29-competing-genetic-algorithm %}){: .btn .btn--info}

[View Project on Github](https://github.com/diovisgood/QGEN_Lua/){: .btn .btn--primary target="_blank"}
