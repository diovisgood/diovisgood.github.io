---
date: 2022-06-22
title: Text Embeddings Computation
excerpt: Did some research and experiments on how to compare texts. Sharing my knowledge here.
category: machine-learning
tags: nlp embedding transformers
---

## Introduction

This is a second article on text embeddings for beginners.
You are encouraged to read the [First Part]({% post_url 2022-06-20-text-embeddings-explanation %}){:target=_blank}.

Here you may find several ways of how to compute text embeddings with code samples.

## Computing Text Embeddings

Here are described several methods of how text embeddings can be computed:

1. Text Classification
2. Zero-Shot Classification
3. Sentence Transformers

### 1. Text Classification

The task of text classification is as easy as it sounds:
given a text we somehow assign one of pre-defined labels to it.

In the simplest case of [Sentiment Analysis](https://huggingface.co/blog/sentiment-analysis-python){:target=_blank}
there are only two classes: `positive` and `negative`. Sentiment Analysis is used, for example,
to compute the [Bitcoin Sentiment](https://www.augmento.ai/bitcoin-sentiment/)
or to programmatically find negative comments about some company in a social network.

Of course, any number of classes can be used.
As it has been described earlier, the more numbers we have - the better we can describe a text.

For example lets have a look at the model [cssupport/bert-news-class](https://huggingface.co/cssupport/bert-news-class){:target=_blank}. 
It is trained to categorize text for 41 classes:

| Classes       | Classes        | Classes       | Classes        | Classes       | Classes        |
|---------------|----------------|---------------|----------------|---------------|----------------|
| Arts          | Arts & Culture | Black Voices  | Business       | College       | Comedy         |
| Crime         | Culture & Arts | Education     | Entertainment  | Environment   | Fifty          |
| Food & Drink  | Good News      | Green         | Healthy Living | Home & Living | Impact         |
| Latino Voices | Media          | Money         | Parenting      | Parents       | Politics       |
| Queer Voices  | Religion       | Science       | Sports         | Style         | Style & Beauty |
| Taste         | Tech           | The Worldpost | Travel         | U.S. News     | Weddings       |
| Weird News    | Wellness       | Women         | World News     | Worldpost     |                |


This particular model uses [bert-base-uncased](https://huggingface.co/bert-base-uncased){:target=_blank}
model under the hood.

BERT is acronym for: Bidirectional Encoder Representations from Transformers.
Today **BERT-based** models are the de facto standard for
[text classification](https://huggingface.co/docs/transformers/tasks/sequence_classification){:target=_blank}
tasks. 

A text in such model is processed in multiple stages:

1. First text is tokenized (split into words or parts or words).
2. Special tokens `[CLS]` and `[SEP]` are added to the text.
3. Each token is substituted by corresponding token embedding using a pre-trained table.
4. Those token embeddings are passed into the model.
5. The information passes through multiple **Transformer Encoder layers**, and is processed in each layer.
6. At the output of a final layer only the first computed value, at the position of the `[CLS]` token, is used.
7. It is passed into a small classifier network, which computes the final probabilities for the required classes.

TODO: image here

It is possible to use a model for text classification in a slightly different way to obtain text embeddings.

Typically, such models are based on BERT-based architecture.

First you need to install required libraries:
```bash
pip install transformers
```

```python
from transformers import AutoTokenizer, AutoModelForSequenceClassification

model_name = 'cssupport/bert-news-class'
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForSequenceClassification.from_pretrained(model_name)

labels = "Arts,Arts & Culture,Black Voices,Business,College,Comedy,Crime,Culture & Arts,Education,Entertainment,Environment,Fifty,Food & Drink,Good News,Green,Healthy Living,Home & Living,Impact,Latino Voices,Media,Money,Parenting,Parents,Politics,Queer Voices,Religion,Science,Sports,Style,Style & Beauty,Taste,Tech,The Worldpost,Travel,U.S. News,Weddings,Weird News,Wellness,Women,World News,Worldpost".split(',')
print(f'Have: {len(labels)} labels in total')

texts = {
    'Thermos Ads': 'Introducing the Adventure Thermos – your ideal companion for outdoor excursions! Engineered for durability and optimum insulation, this thermos keeps your beverages hot or cold in any terrain. Whether you’re hiking, camping, or simply enjoying the great outdoors, trust PeakPro to keep your drinks at the perfect temperature throughout your adventure. Upgrade your outdoor experience with the Adventure Thermos – where every sip is an exploration in refreshment.',
    'How to become an Uber driver': 'Embark on a flexible and rewarding journey by becoming an Uber driver today! Getting started is easy – simply visit the Uber website or download the app to begin your driver application. Provide the required documents, including a valid driver’s license, insurance, and vehicle registration, and undergo a straightforward background check. Once approved, you’re ready to hit the road, set your own schedule, and earn money on your terms. Join the community of Uber drivers and turn your car into a source of income and independence.',
    'Crypto vs S&P500': 'Amidst a correction in the S&P index, the cryptocurrency market remains remarkably stable, showcasing its resilience in the face of traditional market fluctuations. Investors find solace in the consistent performance of cryptocurrencies, highlighting their potential as a diversification strategy. As the S&P undergoes correction, the crypto market’s steadiness prompts a reevaluation of investment portfolios in the ever-evolving financial landscape.',
    'Used boots for sale': 'For sale: Gently-used rubber boots in excellent condition! These reliable boots are ready for their next adventure, offering comfort and durability. Don’t miss the chance to snag a great pair at a fantastic price!',
    'EU central bank fights inflation': 'In a bold move to tackle inflationary pressures, the European Union’s central bank has announced an increase in its key interest rate. This strategic measure aims to curb rising inflation and maintain economic stability within the EU. Investors and economists will closely monitor the impacts of this decision on financial markets and the broader economic landscape.',
    'VW tries to resurrect the Bus': 'Volkswagen is making waves with the revival of the iconic VW Bus, now featuring a state-of-the-art electric engine. Combining nostalgia with environmental consciousness, the electric VW Bus aims to redefine road-tripping for the modern era. Get ready to experience the classic charm of the VW Bus with a sustainable twist, as Volkswagen pioneers a new chapter in electric mobility.',
}


```


### 2. Zero-Shot Classification


### 3. Sentence Transformers


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

3. Text embeddings are fixed.
   Because they are produced by a model with fixed weights on the base of word embeddings, which are also fixed.
   A typical NLP system lacks any tools to adjust model weights to new information.
   This is different from how human brain is changing when it grasps new ideas and concepts.


## Conclusion

Text embeddings revolutionized text comparison and processing.

Yet I believe this is not the end stop, as there are ways for improvement.
A better and adjustable solution is yet to be discovered.
