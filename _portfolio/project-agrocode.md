---
title: "Agrocode Project"
date: 2021-11-18
excerpt: "Predicting the disease(s) of cows by a given textual description. My solution to Agro Code Contest."
categories: machine-learning
tags: natural-language-processing classification multi-label catboost transformer pytorch python featured
sidebar:
  - title: "Period"
    text: "Nov 2021"
  - title: "Technologies"
    text: "**NLP**, **CatBoost**, **Transformer**, **PyTorch**, **Python**"
---

In November 2021 there was a **Machine Learning contest** in Russia.

The task was to predict the disease(s) of cows by a given textual
description of it in natural language (in russian language).

Organizers provided some baseline, as a python notebook,
where they used CatBoostClassifier, treating words as **tokens**,
without analysis of word's forms or meanings.

I tried two different approaches to solve the task.

First, the **Transformer** architecture, in particular, its encoding part.
But the performance was very poor in comparison with the baseline.
I believe, the poor performance of Transformer architecture is due to the small training dataset,
which has only 294 records!

Then I tried a different approach and managed to achieve good results.
I used **CatBoostClassifier**, based on Random Forest Algorithm,
but applied it to **word embeddings** (in contrast to the baseline variant, which used word tokens).
This made my model robust, as it is capable to work with texts and words,
**which it has never seen before**.

## Challenges

The first challenge is that russian language has a lot of
[**grammatical cases**](https://en.wikipedia.org/wiki/Grammatical_case){:target="_blank"},
[**diminutives**](https://en.wikipedia.org/wiki/Diminutive){:target="_blank"} and
[**augmentatives**](https://en.wikipedia.org/wiki/Augmentative){:target="_blank"}.
Thus treating words as a set of unique tokens is very bad idea.

Instead of using tokens I decided to utilize
[**word embeddings**](https://en.wikipedia.org/wiki/Word_embedding){:target="_blank"}.
An important feature of embeddings is that words which are often used together,
will have their embeddings located **nearby** in the multidimensional space.

The second challenge was that there were only 294 samples for both training and validation set.

I believe, this is the reason why Transformer architecture failed.
That is why I used CatBoostClassifier together with word embeddings,
so that it learns about semantics of a text, not about its particular words.

Next, there was an obstacle, as CatBoostClassifier was not designed
to get a sequence of embeddings of **arbitrary length** as the input.

So I came up with an idea of how to convert text of an arbitrary length into
a set of numerical features of a fixed length.

Another challenge was that there could be several diseases for some texts in the training set.
Hence, it is a **Multi-Label Classification** problem.

The solution I ended up with is to use multiple CatBoostClassifier instances, one for each disease.

More technical details can be found in this post:

[Read the Full Story]({% post_url 2021-11-18-agrocode-contest %}){: .btn .btn--info}

[View Project on Github](https://github.com/diovisgood/agrocode/){: .btn .btn--primary target="_blank"}
