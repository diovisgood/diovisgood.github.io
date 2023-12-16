---
date: 2022-06-20
title: "Text Embeddings Explained"
excerpt: "Did some research and experiments on how to compare texts. Sharing my knowledge here."
category: machine-learning
tags: nlp embedding transformers
---

## Introduction

This is "yet another explanation of text embeddings for beginners",
with some code examples, though.

Sometimes I have to explain potential clients the concept of text embeddings.
That is why I have created this article.

The task of comparing texts often arises in many areas. Just a few examples:
- You need to recognize user interests by studying the webpages, he visited.
  This is to find out if user might be interested in a certain product or services,
  for the task of [online advertisement]({% link _portfolio/indata-webpages-semantic-analysis.md %}).
- Given some user query you need to find relevant documents in your database.
  This is when you build a search tool over some knowledge base.
- You are building a recommendation system and need to compare descriptions of products or services (or movies).
  Using a vector representation simplified the task.
- etc.
  

Working with raw texts is not very practical if you need to process and compare them programmatically:
- They can be of arbitrary lengths.
- Words can have different meaning depending on the context.
- Two different phrases can mean the same.

### Long history of text analysis. Briefly.

The history of text analysis, especially in the comparison of two texts,
has been evolving over many years, starting from simple statistical approaches
to more sophisticated techniques like text embeddings.

1. 19th Century: Word Frequency Analysis:
   One of the earliest forms of text analysis based on counting word frequencies.

2. 1960s: [Key Word in Context (KWIC)](https://en.wikipedia.org/wiki/Key_Word_in_Context){:target="_blank"}:
   With the advent of computers, researchers developed tools like KWIC to analyze concordances,
   displaying words in context. This helped in understanding how words were used within a given text.
   
3. 1960s - 1970s: [Vector Space Models (VSM)](http://mlwiki.org/index.php/Vector_Space_Models){:target="_blank"}:
   Represented documents as vectors in a high-dimensional space based on term frequencies.
   [Term Frequency-Inverse Document Frequency (TF-IDF)](http://mlwiki.org/index.php/TF-IDF){:target="_blank"}
   is the most well-known example of such method.
   It measures the importance of terms in a document relative to importance of these terms in a corpus.

4. 1980s - 1990s: [Latent Semantic Analysis (LSA)](http://mlwiki.org/index.php/Latent_Semantic_Analysis){:target="_blank"}:
   Introduced the concept of capturing latent semantic relationships between terms.
   It uses [Singular Value Decomposition (SVD)](https://en.wikipedia.org/wiki/Singular_value_decomposition){:target="_blank"}
   algorithm to reduce the dimensionality of the term-document matrix,
   enabling the discovery of hidden relationships between words.
   
5. Late 20th Century - Early 21st Century: Machine Learning Approaches:
   Algorithms like [Naive Bayes](https://en.wikipedia.org/wiki/Naive_Bayes_classifier){:target="_blank"},
   [Support Vector Machines (SVM)](http://mlwiki.org/index.php/Support_Vector_Machines){:target="_blank"},
   and [k-means clustering](http://mlwiki.org/index.php/K-Means){:target="_blank"} were applied
   to compare and analyze texts based on their content.

6. 2010 - 2018: Word Embeddings and Neural Networks:
   Algorithms like [Word2Vec](https://en.wikipedia.org/wiki/Word2vec){:target="_blank"}
   and [GloVe](https://en.wikipedia.org/wiki/GloVe){:target="_blank"},
   represented words as dense vectors in a continuous vector space, capturing semantic relationships.
   This allowed for more nuanced text comparisons.
   Combined with neural network architectures like
   [Recurrent Neural Networks (RNNs)](https://en.wikipedia.org/wiki/Recurrent_neural_network){:target="_blank"}
   and [Long Short-Term Memory networks (LSTMs)](https://en.wikipedia.org/wiki/Long_short-term_memory){:target="_blank"}
   they became popular for processing texts, language translation, etc.
   
7. 2018 - now: [Transformer](https://en.wikipedia.org/wiki/Transformer_(machine_learning_model)){:target="_blank"} architectures:
   After the paper [Attention Is All You Need](https://arxiv.org/abs/1706.03762){:target="_blank"}
   there is an ongoing blossom of models for text semantic processing and text generation.
   These models use attention mechanisms to capture contextual relationships between words.
   It revolutionized natural language processing tasks, including text comparison,
   by considering the entire context of a word within a sentence.

## Text Embeddings Step-by-Step

Now I'm going to walk you through the idea of how to represent a text (of arbitrary length)
as a list of numbers (of fixed length).

### Sample texts

Here are six texts to be used throughout this article. I tried to make them as short as possible, because... well,
nobody likes long texts nowadays.

> ### Thermos Ads
> ![Thermos](/assets/img/text-embed-thermos.jpg){:width="167"}
> <br/>
> Introducing the Adventure Thermos – your ideal companion for outdoor excursions!
> Engineered for durability and optimum insulation, this thermos keeps your beverages hot or cold in any terrain.
> Whether you're hiking, camping, or simply enjoying the great outdoors,
> trust PeakPro to keep your drinks at the perfect temperature throughout your adventure.
> Upgrade your outdoor experience with the Adventure Thermos – where every sip is an exploration in refreshment.

> ### How to become an Uber driver
> ![Driver](/assets/img/text-embed-driver.jpg){:width="167"}
> <br/>
> Embark on a flexible and rewarding journey by becoming an Uber driver today!
> Getting started is easy – simply visit the Uber website or download the app to begin your driver application.
> Provide the required documents, including a valid driver's license, insurance, and vehicle registration,
> and undergo a straightforward background check.
> Once approved, you're ready to hit the road, set your own schedule, and earn money on your terms.
> Join the community of Uber drivers and turn your car into a source of income and independence.

> ### Crypto vs S&P500
> ![Crypto](/assets/img/text-embed-crypto.jpg){:width="167"}
> <br/>
> Amidst a correction in the S&P index, the cryptocurrency market remains remarkably stable,
> showcasing its resilience in the face of traditional market fluctuations.
> Investors find solace in the consistent performance of cryptocurrencies,
> highlighting their potential as a diversification strategy.
> As the S&P undergoes correction, the crypto market's steadiness prompts a reevaluation of
> investment portfolios in the ever-evolving financial landscape.

> ### Used boots for sale
> ![Used boots](/assets/img/text-embed-shoes.jpg){:width="167"}
> <br/>
> For sale: Gently-used rubber boots in excellent condition!
> These reliable boots are ready for their next adventure, offering comfort and durability.
> Don't miss the chance to snag a great pair at a fantastic price!

> ### EU central bank fights inflation
> ![EU central bank](/assets/img/text-embed-ecb.jpg){:width="167"}
> <br/>
> In a bold move to tackle inflationary pressures, the European Union's central bank has announced
> an increase in its key interest rate.
> This strategic measure aims to curb rising inflation and maintain economic stability within the EU.
> Investors and economists will closely monitor the impacts of this decision on financial markets
> and the broader economic landscape.

> ### VW tries to resurrect the Bus
> ![VW electric bus](/assets/img/text-embed-vw-bus.jpg){:width="167"}
> <br/>
> Volkswagen is making waves with the revival of the iconic VW Bus, now featuring a state-of-the-art electric engine.
> Combining nostalgia with environmental consciousness,
> the electric VW Bus aims to redefine road-tripping for the modern era.
> Get ready to experience the classic charm of the VW Bus with a sustainable twist,
> as Volkswagen pioneers a new chapter in electric mobility.

## Pros and Cons of Text Embeddings

### Pros

1. Text embeddings estimate the true semantic relationship between texts.
   This works much better than any of keywords search or words statistics comparison.
   This provides the possibility to search for similar texts and to compare texts.

### Cons

1. The number of dimensions of embeddings is fixed.
   We still do not know what is the optimal dimensionality to describe the world,
   nor how to add new dimensions to already pre-trained word embeddings, if we find out it is not enough.
   A typical NLP system lacks any tools to change embeddings dimensionality.

2. The number of words is fixed in a vocabulary, used to process a text.
   Meanwhile, new words appear every year.
   Also, the semantic meaning of old words slowly changes over time.
   A typical NLP system lacks any tools to add new words or adjust the semantic meaning of old words.

3. Text embedding are fixed.
   Because they are produced by a model with fixed weights on the base of word embeddings, which are also fixed.
   A typical NLP system lacks any tools to adjust model weights to new information.
   This is different from how human brain is changing when it grasps new ideas and concepts.
