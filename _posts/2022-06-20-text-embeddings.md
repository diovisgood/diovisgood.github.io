---
date: 2022-06-20
title: "Text Embeddings Explained"
excerpt: "Did some research and experiments on how to compare texts. Sharing my knowledge here."
category: machine-learning
tags: nlp embedding transformers
---

## Introduction

This is "yet another explanation of text embeddings for beginners".

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

> **Thermos Ads**
> <br/>
> ![Thermos](/assets/img/text-embed-thermos.jpg){:width="167"}
> <br/>
> Introducing the Adventure Thermos – your ideal companion for outdoor excursions!
> Engineered for durability and optimum insulation, this thermos keeps your beverages hot or cold in any terrain.
> Whether you're hiking, camping, or simply enjoying the great outdoors,
> trust PeakPro to keep your drinks at the perfect temperature throughout your adventure.
> Upgrade your outdoor experience with the Adventure Thermos – where every sip is an exploration in refreshment.

> **How to become an Uber driver**
> <br/>
> ![Driver](/assets/img/text-embed-driver.jpg){:width="167"}
> <br/>
> Embark on a flexible and rewarding journey by becoming an Uber driver today!
> Getting started is easy – simply visit the Uber website or download the app to begin your driver application.
> Provide the required documents, including a valid driver's license, insurance, and vehicle registration,
> and undergo a straightforward background check.
> Once approved, you're ready to hit the road, set your own schedule, and earn money on your terms.
> Join the community of Uber drivers and turn your car into a source of income and independence.

> **Crypto vs S&P500**
> <br/>
> ![Crypto](/assets/img/text-embed-crypto.jpg){:width="167"}
> <br/>
> Amidst a correction in the S&P index, the cryptocurrency market remains remarkably stable,
> showcasing its resilience in the face of traditional market fluctuations.
> Investors find solace in the consistent performance of cryptocurrencies,
> highlighting their potential as a diversification strategy.
> As the S&P undergoes correction, the crypto market's steadiness prompts a reevaluation of
> investment portfolios in the ever-evolving financial landscape.

> **Used boots for sale**
> <br/>
> ![Used boots](/assets/img/text-embed-shoes.jpg){:width="167"}
> <br/>
> For sale: Gently-used rubber boots in excellent condition!
> These reliable boots are ready for their next adventure, offering comfort and durability.
> Don't miss the chance to snag a great pair at a fantastic price!

> **EU central bank fights inflation**
> <br/>
> ![EU central bank](/assets/img/text-embed-ecb.jpg){:width="167"}
> <br/>
> In a bold move to tackle inflationary pressures, the European Union's central bank has announced
> an increase in its key interest rate.
> This strategic measure aims to curb rising inflation and maintain economic stability within the EU.
> Investors and economists will closely monitor the impacts of this decision on financial markets
> and the broader economic landscape.

> **VW tries to resurrect the Bus**
> <br/>
> ![VW electric bus](/assets/img/text-embed-vw-bus.jpg){:width="167"}
> <br/>
> Volkswagen is making waves with the revival of the iconic VW Bus, now featuring a state-of-the-art electric engine.
> Combining nostalgia with environmental consciousness,
> the electric VW Bus aims to redefine road-tripping for the modern era.
> Get ready to experience the classic charm of the VW Bus with a sustainable twist,
> as Volkswagen pioneers a new chapter in electric mobility.

### Measure one dimension: Physical product vs. Service

First we can start by "measuring" how each of these texts is related to Physical Product vs Service.
Where:
- -1 means: a text is about a physical product,
- 0 means: text is not about a physical product or service,
- 1 means: text is about a service.

![](/assets/img/text-embed-1.jpg)

> Note: it is sometimes hard to explicitly tell a text is about a product or a service!

### Add another dimension: Relation to Travel

Then we can add another dimension: Relation of a text to Travel, where:
- -1 means: a text is not related to travelling,
- 0 means: text is not about a physical product or service,
- 1 means: text is related to travelling.

![](/assets/img/text-embed-2.jpg)


### Add many more dimensions

Then we can add many more dimensions:
- Relation to Finance
- Relation to News
- etc.

![](/assets/img/text-embed-3.jpg)

Now for each text we get a list of N numbers. It is called: **text embedding**.

This list defines the coordinates of a text in N-dimensional space.
Texts with related content are located nearby in this space.


### How to choose dimensions?

In the examples above we have specified the meaning of dimensions manually:
1. Physical vs Service
2. Relation to Travel
3. Relation to Finance
4. Relation to News
5. etc.

While in practice we allow a computer algorithm to choose the meaning of the coordinate axes **algorithmically**.
The semantic space we obtain in this way is better suited for our purpose:
to determine whether two texts are similar or not. (See:
[Sentence Transformers](http://www.sbert.net/){:target="_blank"}).

### Euclidean vs Cosine Distances

Now that we have computed the vector embeddings for all texts,
we can measure the distance between them to compare their similarity. 

We are used to understanding the distance as the Euclidean distance.
Meanwhile, there are many other measures which can be computed of two vectors.

In fact, for the task of text-embedding comparison the **cosine similarity** measure is more appropriate.

![](/assets/img/text-embed-5.jpg)

### From Cosine Distance to Dot Product

One minor addition here is the fact, that when using the **cosine similarity**,
it is better to keep embedding vectors normalized (to the unit length).
As this measure does not depend on the length of vectors, but only on their directions.
This helps to slightly decrease the computations when working with a large amount of embeddings.

![](/assets/img/text-embed-6.jpg)

## Computing Text Embeddings

Here are described several methods of how text embeddings can be computed:

1. Text Classification
2. Zero-Shot Classification
3. Sentence Transformers

### 1. Text Classification

[TODO]

### 2. Zero-Shot Classification

[TODO]

### 3. Sentence Transformers

[TODO]

## Additional Notes

### Dealing With Long Texts

Most of attention-based models have limitation of only 512 input tokens.
Because self-attention approach has a quadratic complexity O(n²) in terms of the sequence length n.
This is roughly equivalent to nearly 200 words.

![](/assets/img/text-embed-7.jpg)

Typical approaches are:
1. Use only one part of a text to compute embeddings (first, middle or last).
2. Split text into chunks, process each of them individually and combine the results back together.
3. Use chunks (as in option 2) but feed the output token for each chunk to another network to produce the final result.

Processing Long Texts by Chunks looks like this:

![](/assets/img/text-embed-8.jpg)


## Pros and Cons of Text Embeddings

### Pros

1. Text embeddings estimate the true semantic relationship between texts.
   This works much better than any of keywords search or words statistics comparison.
   This provides the possibility to search for similar texts and to compare texts.

### Cons

1. Sometimes text embedding methods struggle to deal with negation.
   For example: `I like coffee` and `I do not like coffee` can produce text embeddings,
   which are located very close to each other in the embeddings space,
   despite having an opposite meaning.

2. The number of dimensions of embeddings is fixed.
   We still do not know what is the optimal dimensionality to describe the world,
   nor how to add new dimensions to already pre-trained word embeddings, if we find out it is not enough.
   A typical NLP system lacks any tools to change embeddings dimensionality.

3. Text embedding are fixed.
   Because they are produced by a model with fixed weights on the base of word embeddings, which are also fixed.
   A typical NLP system lacks any tools to adjust model weights to new information.
   This is different from how human brain is changing when it grasps new ideas and concepts.


## Conclusion

Text embeddings revolutionized text comparison and processing.

Yet I believe this is not the end stop, as there are ways for improvement.
A better and adjustable solution is yet to be discovered.