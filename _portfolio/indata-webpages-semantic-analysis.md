---
title: "Webpages Semantic Analysis for Ads Campaigns"
date: 2022-11-20
excerpt: "Semantic analysis of webpages and browsing history to better understand the interests of a user for showing only relevant Ads"
category: machine-learning
tags: nlp transformers pytorch python aws featured
sidebar:
  - title: "Period"
    text: "May 2022 - Dec 2022"
  - title: "Technologies"
    text: "**Transformers**, **PyTorch**, **Python**, **AWS**"
  - title: "Role"
    text: "Data Scientist, Team Lead, System Architect"
  - title: "Responsibilities"
    text: "Researching the best way to analyze a webpage, designing whole system architecture, writing big data processing pipeline, deploying system on AWS"
---

In the industry of online ads agents need to quickly decide which ads to display on a particular webpage
for a particular user, taking into account the content of a webpage and user interests.

Some time ago we have completed a challenging project for a fast-growing company
which is exploring new ways to target an audience.
NDA forbids me to reveal any details.
But one thing I can say with confidence is that the most critical objective in this industry
is accurately determining a user's interests,
and a significant amount of efforts is concentrated to achieving this.

First I solely implemented and proved the idea during the PoC phase.
Then, during the second phase me and a team of other engineers created MVP.
I researched different approaches for web-scraping and semantic analysis,
investigated the feasibility of small response timings.

The challenge was to deploy this system on the AWS cloud platform,
as there are many ways to do this,
so you need to choose wisely to reach a balance between an optimal cost and performance.

I designed the loosely coupled architecture of the whole system and implemented
a crucial part of it related to the stream processing of large amounts of data.
Also, I deployed our models in AWS SageMaker.

This project involved multiple aspects:
- data retrieving and preprocessing from variety of public sources
- solution for web-scraping and text extraction from HTML
- solution to detect if a particular webpage has ads on it or not
- verifying different approaches to compute text embeddings: Zero-Shot Classification and Sentence Transformers
- solution to expand a query using pre-trained language models (GloVe, Word2Vec, etc.)
- solution to expand a query using pre-trained language models in the autocomplete mode
- solution to expand a query using existing knowledge graphs of Google, Microsoft, Wikidata and Xlore
- set of tools to search for scraped webpages with a query and to compare webpages by their embeddings

I learned a lot of new things about advertisement industry.
I tried to summarize my experience in the following post:

[Introduction to Online Ads Industry]({% post_url 2022-11-20-online-ads-is-complicated %}){: .btn .btn--info}
