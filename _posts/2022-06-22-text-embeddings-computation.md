---
date: 2022-06-22
title: "Text Embeddings (2/3) - Computation"
excerpt: "Did some research and experiments on how to compare texts. Sharing my knowledge here."
category: machine-learning
tags: nlp embedding transformers pytorch python
---

## Introduction

This is the second of three articles on text embeddings for beginners:
1. [Text Embeddings (1/3) - Explanation]({% post_url 2022-06-20-text-embeddings-explanation %}){:target=_blank}
2. **Text Embeddings (2/3) - Computation** (you are here)
3. [Text Embeddings (3/3) - Conclusion]({% post_url 2022-06-24-text-embeddings-conclusion %}){:target=_blank}

Here you may find several ways of how to compute text embeddings with code samples.

## Computing Text Embeddings

Here are described several methods of how text embeddings can be computed:

1. Word Embeddings
2. Zero-Shot Classification
3. Text Classification
4. Sentence Transformers

<hr/>

### 1. Word Embeddings

#### Description

Since 2010 algorithms like [Word2Vec](https://en.wikipedia.org/wiki/Word2vec){:target="_blank"}
and [GloVe](https://en.wikipedia.org/wiki/GloVe){:target="_blank"} 
introduced new concept: [Word Embeddings](https://en.wikipedia.org/wiki/Word_embedding){:target="_blank"}.

This is a representation of words as dense vectors in a continuous vector space,
capturing semantic relationships.
This allowed for more nuanced text comparisons.

{% include figure image_path="/assets/img/text-embed-space.jpg" alt="words embeddings space" caption="Words embeddings space capture semantic relations between words" %}

The simplest solution to compute text embedding is to take the mean value over all of its words:

{% include figure image_path="/assets/img/text-embed-words.jpg" alt="text embedding from words embeddings" caption="Take text embedding as the mean value over words embeddings" %}

#### Computation

#### Pros and Cons

This is the easiest and fastest solution.
You only need to have a dictionary of pre-trained words embeddings.
Such dictionaries are freely available.

Nevertheless, this method does not take into account the contextual relationships between words in a sentence.

<hr/>

### 2. Zero-Shot Classification

#### Description

There is a field in machine learning called
[**Natural Language Inference (NLI)**](https://en.wikipedia.org/wiki/Textual_entailment){:target="_blank"}.
This field is focused on models, which can compare two texts: a **hypothesis** and **premise** - and answer
whether a hypothesis is **True** (entailment), **False** (contradiction), or **Undetermined** (neutral) for a given premise.

We can take out input text as premise and each of the categories as hypothesis.
Then we can compute the probabilities of a pair and take the **entailnment** probability as
the measurement of a text across a category.

{% include figure image_path="/assets/img/text-embed-zeroshot.jpg" alt="zero-shot classification" caption="Text embedding computed from zero-shot classification" %}


#### Computation

TODO

#### Pros and Cons

Experiments show that embeddings produced this way are correct and suitable for the task of text comparison.

This approach has the benefit as the dimensions of an embedding vector are interpretable.
I.e. each dimension corresponds to some category.
Also, we can easily adjust the list of categories (by recomputing, of course). 

The only drawback here is that it takes too much time to compute embedding of a text this way.
It takes up to minutes to compute embedding for a text on a server with GPU!
This method is not practical.

<hr/>

### 3. Text Classification

#### Description

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

| Classes        | Classes        | Classes        | Classes      | Classes        | Classes    |
|----------------|----------------|----------------|--------------|----------------|------------|
| Arts           | Culture & Arts | Green          | Parenting    | Style          | Weddings   |
| Arts & Culture | Education      | Healthy Living | Parents      | Style & Beauty | Weird News |
| Black Voices   | Entertainment  | Home & Living  | Politics     | Taste          | Wellness   |
| Business       | Environment    | Impact         | Queer Voices | Tech           | Women      |
| College        | Fifty          | Latino Voices  | Religion     | The Worldpost  | World News |
| Comedy         | Food & Drink   | Media          | Science      | Travel         | Worldpost  |
| Crime          | Good News      | Money          | Sports       | U.S. News      |            |


This particular model is a fine-tuned version of [bert-base-uncased](https://huggingface.co/bert-base-uncased){:target=_blank}
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

{% include figure image_path="/assets/img/text-embed-classifier.jpg" alt="BERT-based classifier" caption="Text embeddings as the output of a BERT-based classifier model" %}

The model outputs 41 numbers - these are the probabilities that a text belongs to a certain category.
Typically, the category with the highest probability is taken as the final outcome.
But in our task we would instead keep all **41 numbers as the text embedding**.

#### Computation

Here is the source code of how to compute such text embeddings:

```python
from transformers import AutoTokenizer, AutoModelForSequenceClassification
from typing import Union, Sequence, List
import pandas as pd
import numpy as np
import torch

device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')

model_name = 'cssupport/bert-news-class'
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForSequenceClassification.from_pretrained(model_name).to(device)

classes = "Arts,Arts & Culture,Black Voices,Business,College,Comedy,Crime,Culture & Arts,Education,Entertainment,Environment,Fifty,Food & Drink,Good News,Green,Healthy Living,Home & Living,Impact,Latino Voices,Media,Money,Parenting,Parents,Politics,Queer Voices,Religion,Science,Sports,Style,Style & Beauty,Taste,Tech,The Worldpost,Travel,U.S. News,Weddings,Weird News,Wellness,Women,World News,Worldpost".split(',')
print(f'Have: {len(classes)} classes in total')

texts = {
    'Thermos Ads': 'Introducing the Adventure Thermos – your ideal companion for outdoor excursions! Engineered for durability and optimum insulation, this thermos keeps your beverages hot or cold in any terrain. Whether you’re hiking, camping, or simply enjoying the great outdoors, trust PeakPro to keep your drinks at the perfect temperature throughout your adventure. Upgrade your outdoor experience with the Adventure Thermos – where every sip is an exploration in refreshment.',
    'How to become an Uber driver': 'Embark on a flexible and rewarding journey by becoming an Uber driver today! Getting started is easy – simply visit the Uber website or download the app to begin your driver application. Provide the required documents, including a valid driver’s license, insurance, and vehicle registration, and undergo a straightforward background check. Once approved, you’re ready to hit the road, set your own schedule, and earn money on your terms. Join the community of Uber drivers and turn your car into a source of income and independence.',
    'Crypto vs S&P500': 'Amidst a correction in the S&P index, the cryptocurrency market remains remarkably stable, showcasing its resilience in the face of traditional market fluctuations. Investors find solace in the consistent performance of cryptocurrencies, highlighting their potential as a diversification strategy. As the S&P undergoes correction, the crypto market’s steadiness prompts a reevaluation of investment portfolios in the ever-evolving financial landscape.',
    'Used boots for sale': 'For sale: Gently-used rubber boots in excellent condition! These reliable boots are ready for their next adventure, offering comfort and durability. Don’t miss the chance to snag a great pair at a fantastic price!',
    'EU central bank fights inflation': 'In a bold move to tackle inflationary pressures, the European Union’s central bank has announced an increase in its key interest rate. This strategic measure aims to curb rising inflation and maintain economic stability within the EU. Investors and economists will closely monitor the impacts of this decision on financial markets and the broader economic landscape.',
    'VW tries to resurrect the Bus': 'Volkswagen is making waves with the revival of the iconic VW Bus, now featuring a state-of-the-art electric engine. Combining nostalgia with environmental consciousness, the electric VW Bus aims to redefine road-tripping for the modern era. Get ready to experience the classic charm of the VW Bus with a sustainable twist, as Volkswagen pioneers a new chapter in electric mobility.',
}

def compute_embeddings(text: Union[str, Sequence[str]]) -> np.ndarray:
    input_is_string = isinstance(text, str)
    # Tokenize the input text
    inputs = tokenizer(text, return_tensors='pt', truncation=True, max_length=512, padding='max_length').to(device)
    # Compute class probabilities
    with torch.no_grad():
        logits = model(**inputs)[0]
        class_probabilities = torch.softmax(logits, dim=-1).cpu().numpy()
    if input_is_string:
        return class_probabilities[0]
    return class_probabilities

class_probabilities = compute_embeddings(list(texts.values()))

df = pd.DataFrame(class_probabilities, columns=classes, index=list(texts.keys()))
print(df.idxmax(axis=1))
print(df.to_markdown())
```

The most probable category for each text:

```text
Thermos Ads                           Travel
How to become an Uber driver        Business
Crypto vs S&P500                    Business
Used boots for sale                    Style
EU central bank fights inflation    Business
VW tries to resurrect the Bus       Business
```

The text embeddings for each text:

|                                  |   Arts | Arts & Culture | Black Voices |   Business | College | Comedy |  Crime | Culture & Arts | Education | Entertainment | Environment |  Fifty | Food & Drink | Good News |  Green | Healthy Living | Home & Living | Impact | Latino Voices |   Media |   Money | Parenting | Parents | Politics |   Queer Voices |   Religion |   Science | Sports |      Style | Style & Beauty |  Taste |   Tech | The Worldpost |     Travel | U.S. News | Weddings |   Weird News | Wellness |  Women | World News | Worldpost |
|:---------------------------------|-------:|---------------:|-------------:|-----------:|--------:|-------:|-------:|---------------:|----------:|--------------:|------------:|-------:|-------------:|----------:|-------:|---------------:|--------------:|-------:|--------------:|--------:|--------:|----------:|--------:|---------:|---------------:|-----------:|----------:|-------:|-----------:|---------------:|-------:|-------:|--------------:|-----------:|----------:|---------:|-------------:|---------:|-------:|-----------:|----------:|
| Thermos Ads                      | 0.0040 |         0.0020 |       0.0001 |     0.0104 |  0.0010 | 0.0019 | 0.0006 |         0.0038 |    0.0017 |        0.0003 |      0.0037 | 0.0259 |       0.0094 |    0.0035 | 0.0079 |         0.0116 |        0.0046 | 0.0024 |        0.0008 |  0.0006 |  0.0055 |    0.0027 |  0.0024 |   0.0002 |         0.0011 |     0.0018 |    0.0054 | 0.0007 |     0.0052 |         0.0051 | 0.0230 | 0.0035 |        0.0010 | **0.8289** |    0.0006 |   0.0024 |       0.0043 |   0.0065 | 0.0010 |     0.0008 |    0.0017 |
| How to become an Uber driver     | 0.0019 |         0.0014 |       0.0015 | **0.7740** |  0.0070 | 0.0019 | 0.0016 |         0.0013 |    0.0155 |        0.0009 |      0.0012 | 0.0160 |       0.0030 |    0.0025 | 0.0017 |         0.0123 |        0.0034 | 0.0252 |        0.0015 |  0.0021 |  0.0034 |    0.0022 |  0.0070 |   0.0045 |         0.0032 |     0.0017 |    0.0009 | 0.0008 |     0.0019 |         0.0020 | 0.0028 | 0.0647 |        0.0008 |     0.0107 |    0.0024 |   0.0010 |       0.0009 |   0.0019 | 0.0096 |     0.0006 |    0.0011 |
| Crypto vs S&P500                 | 0.0006 |         0.0003 |       0.0004 | **0.9250** |  0.0025 | 0.0003 | 0.0011 |         0.0004 |    0.0031 |        0.0008 |      0.0010 | 0.0008 |       0.0013 |    0.0006 | 0.0039 |         0.0020 |        0.0011 | 0.0046 |        0.0004 |  0.0017 |  0.0014 |    0.0004 |  0.0004 |   0.0109 |         0.0003 |     0.0004 |    0.0016 | 0.0006 |     0.0005 |         0.0007 | 0.0011 | 0.0163 |        0.0007 |     0.0016 |    0.0062 |   0.0003 |       0.0006 |   0.0005 | 0.0007 |     0.0008 |    0.0019 |
| Used boots for sale              | 0.0100 |         0.0062 |       0.0018 |     0.0081 |  0.0048 | 0.0027 | 0.0018 |         0.0185 |    0.0060 |        0.0020 |      0.0067 | 0.0243 |       0.0300 |    0.0173 | 0.0050 |         0.0074 |        0.0232 | 0.0101 |        0.0015 |  0.0013 |  0.0198 |    0.0109 |  0.0104 |   0.0003 |         0.0052 |     0.0043 |    0.0032 | 0.0099 | **0.4820** |         0.1574 | 0.0197 | 0.0031 |        0.0025 |     0.0189 |    0.0010 |   0.0184 |       0.0161 |   0.0095 | 0.0105 |     0.0025 |    0.0059 |
| EU central bank fights inflation | 0.0074 |         0.0013 |       0.0007 | **0.3497** |  0.0074 | 0.0007 | 0.0025 |         0.0035 |    0.0107 |        0.0042 |      0.0080 | 0.0026 |       0.0089 |    0.0033 | 0.0470 |         0.0082 |        0.0050 | 0.0765 |        0.0036 |  0.0035 |  0.0077 |    0.0025 |  0.0010 |   0.0361 |         0.0007 |     0.0027 |    0.0095 | 0.0022 |     0.0023 |         0.0066 | 0.0067 | 0.0071 |        0.0521 |     0.0085 |    0.0170 |   0.0028 |       0.0016 |   0.0040 | 0.0014 |     0.0825 |    0.1907 |
| VW tries to resurrect the Bus    | 0.0030 |         0.0014 |       0.0006 | **0.8037** |  0.0044 | 0.0005 | 0.0012 |         0.0014 |    0.0062 |        0.0008 |      0.0027 | 0.0045 |       0.0036 |    0.0036 | 0.0228 |         0.0041 |        0.0035 | 0.0406 |        0.0010 |  0.0015 |  0.0033 |    0.0010 |  0.0012 |   0.0066 |         0.0005 |     0.0013 |    0.0036 | 0.0010 |     0.0015 |         0.0018 | 0.0027 | 0.0214 |        0.0012 |     0.0254 |    0.0061 |   0.0007 |       0.0018 |   0.0018 | 0.0013 |     0.0012 |    0.0033 |



#### Pros and Cons

This approach has a great benefit as the text embedding is computed at one run, which is very fast.

But it is almost impossible to find a pre-trained model which covers a wide range of categories.
The 41 classes in the presented example, of course, are not enough to describe all variety of texts.

This implies you would need to train your own classifier.
The only drawback of such approach is that in order to train such classifier,
you need to construct a large enough dataset of texts with assigned categories labels.


### 4. Sentence Transformers

#### Description

As it has been mentioned above, **Word Embeddings** method does not take into account
the contextual relationships between words in a sentence.
While in **Text Classification** method it is hard to define a comprehensive list of categories and train a model on it.
If we take the best of both methods we end up with a **Sentence Transformer** method.

Here we use a BERT-based model, which is specially trained to produce text embeddings most suitable for comparison.
The idea of how to train BERT-based networks for the task of text comparison was first described in the paper:
[Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks](https://arxiv.org/pdf/1908.10084.pdf){:target=_blank}.

To achieve the best results for the task of semantic text similarity authors used the **Triplet Objective Function**.

> Triplet Objective Function:
> Given an anchor sentence `a`, a positive sentence `p`, and a negative sentence `n`,
> triplet loss tunes the model such that the distance between `a` embedding and `p` embedding
> is smaller  than the distance between `a` embedding and `n` embedding.

This technique helped to gain the top scores in the task of comparison of texts.

Note, that we do not specify the list of categories manually, but let the training process to choose them automatically.
Typically, existing pre-trained models produce embeddings of the size either 384 or 768 numbers.

A text in such model is processed in multiple stages, similar to the **Text Classification** method:

1. First text is tokenized (split into words or parts or words).
2. Special tokens `[CLS]` and `[SEP]` are added to the text.
3. Each token is substituted by corresponding token embedding using a pre-trained table.
4. Those token embeddings are passed into the model.
5. The information passes through multiple **Transformer Encoder layers**, and is transformed in each layer.
6. As the output of a final layer we get transformed embeddings for each input word.
7. Typically, we compute text embedding as the mean value of all output embeddings.

{% include figure image_path="/assets/img/text-embed-sbert.jpg" alt="SBERT" caption="Sentence Transformers take into account the contextual relationships between words in a sentence" %}

#### Computation

TODO

#### Pros and Cons

This approach has the advantage that the embedding vector is computed very fast,
even without GPU (using CPU only).

The only disadvantage here is that these dimensions are hardly interpretable.
I.e. we cannot know what is the meaning of the n-th dimension, what this number means for a particular text.

Nevertheless, we often do not need interpretability for the task of text comparison.
All we need is the ability to compare different texts and measure their similarity.

## Dealing With Long Texts

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


<hr/>

**Navigate to other articles of the series**

1. [Text Embeddings (1/3) - Explanation]({% post_url 2022-06-20-text-embeddings-explanation %}){:target=_blank}
2. **Text Embeddings (2/3) - Computation** (you are here)
3. [Text Embeddings (3/3) - Conclusion]({% post_url 2022-06-24-text-embeddings-conclusion %}){:target=_blank}
