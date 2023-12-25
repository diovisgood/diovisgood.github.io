---
date: 2022-06-24
title: "Text Embeddings (3/3) - Conclusion"
excerpt: "Did some research and experiments on how to compare texts. Sharing my knowledge here."
category: machine-learning
tags: nlp embedding transformers
---

## Introduction

This is the third of three articles on text embeddings for beginners:
1. [Text Embeddings (1/3) - Explanation]({% post_url 2022-06-20-text-embeddings-explanation %}){:target="_blank"}
2. [Text Embeddings (2/3): Computation]({% post_url 2022-06-22-text-embeddings-computation %}){:target="_blank"}
3. **Text Embeddings (3/3) - Conclusion** (you are here)

Here you may find my concluding thoughts on text embeddings.

## Pros and Cons of Text Embeddings

### Pros

1. Text embeddings capture the true semantic relationship between texts.
   This works much better than any of keywords search or words statistics comparison.
   This provides the possibility to search for similar texts and to compare texts.

2. Feature Extraction.
   Text embeddings serve as effective features for other traditional machine learning algorithms
   for text classification, clustering, etc.

### Cons

1. Text embedding methods I've studied so far all struggle to understand negation.
   For example: `I like coffee` and `I do not like coffee` can produce text embeddings,
   which are located very close to each other in the embeddings space,
   despite having an opposite meaning.
   
2. The number of dimensions of embeddings is fixed.
   We still do not know what is the optimal dimensionality to describe the world,
   nor how to add new dimensions to already pre-trained word embeddings, if it is not enough.
   A typical NLP system lacks any tools to change embeddings dimensionality.

3. Text embeddings are fixed.
   Because they are produced by a model with fixed weights on the base of word embeddings, which are also pre-trained.
   A typical NLP system lacks any tools to adjust model weights to new information.
   This is different from how human brain is changing when it grasps new ideas and concepts.

4. Thus text embeddings may not perform well on some specific tasks,
   as they are trained on diverse datasets and might not capture
   the nuances of certain domains.

5. Poor interpretability.
   Interpreting the meaning of individual dimensions in an embedding space can be challenging,
   making it difficult to understand why certain comparisons yield specific results.

<hr/>

## Conclusion

Text embeddings revolutionized text comparison and processing.
They represent entire documents as vectors in a continuous vector space.
Which makes it possible to compute similarity of texts,
find "mean value" of two texts and do other vector tricks.

Yet I believe this is not the end stop, as there are ways for improvement.
A better and adjustable solution is yet to be discovered.

From the practical point of view, embeddings computed with **Sentence Transformers** and **OpenAI API** methods
produce the best results.
Yet, as of today, the embeddings from **Sentence Transformers** are slightly better.

If you decide what method to choose to compute text embeddings,
I would recommend the **Sentence Transformers** method.
- its models, typically, run very fast;
- they can even be used without GPU (CPU only);
- they are free to use for commercial purpose;
- embeddings they produce are very good for text comparison.

You can choose a particular **Sentence Transformer** model
using this [benchmark](https://huggingface.co/spaces/mteb/leaderboard){:target="_blank"}.
 
<hr/>

#### Links and Resources

The source code for this article is freely available here:
[text-embeddings.ipynb ](https://gist.github.com/diovisgood/ed226fa670076fdba65c5ce556d289eb){:target="_blank"}

1. [Key Word in Context (KWIC)](https://en.wikipedia.org/wiki/Key_Word_in_Context){:target="_blank"}
2. [Vector Space Models (VSM)](http://mlwiki.org/index.php/Vector_Space_Models){:target="_blank"}
3. [Term Frequency-Inverse Document Frequency (TF-IDF)](http://mlwiki.org/index.php/TF-IDF){:target="_blank"}
4. [Latent Semantic Analysis (LSA)](http://mlwiki.org/index.php/Latent_Semantic_Analysis){:target="_blank"}
5. [Word2Vec Wiki](https://en.wikipedia.org/wiki/Word2vec){:target="_blank"}
6. [GloVe Wiki](https://en.wikipedia.org/wiki/GloVe){:target="_blank"}
7. [Transformer Wiki](https://en.wikipedia.org/wiki/Transformer_(machine_learning_model)){:target="_blank"}
8. [Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks](https://arxiv.org/pdf/1908.10084.pdf){:target="_blank"}
9. [Natural Language Inference (NLI) Wiki](https://en.wikipedia.org/wiki/Textual_entailment){:target="_blank"}
10. [HuggingFace - Text Classification](https://huggingface.co/docs/transformers/tasks/sequence_classification){:target="_blank"})
11. [Sentence Transformers Library](https://www.sbert.net/){:target="_blank"}
12. [Reddit: compare openai and Sentence Transformer](https://www.reddit.com/r/MachineLearning/comments/11okrni/discussion_compare_openai_and_sentencetransformer/){:target="_blank"}
13. [Some benchmark table of different models](https://huggingface.co/spaces/mteb/leaderboard){:target="_blank"}
14. [Private opinion on opeanai embeddings](https://iamnotarobot.substack.com/p/should-you-use-openais-embeddings){:target="_blank"}
15. [Embeddings - OpenAI API](https://platform.openai.com/docs/guides/embeddings/use-cases){:target="_blank"}
