---
title: What’s in a %&!$# vector? Explaining text embeddings and text similarity
subtitle: Explaining text embeddings and text similarity
layout: default
published: false
---

# {{ page.title }}

# Intro: What’s in a $&!#\*[^1] vector?

Capturing the meaning of a text as a vector (aka representation, or embedding, if you will) has been a long standing goal of NLP research. With good vectors, we can use some simple algebra for performing important NLÜ tasks efficiently: search/information retrieval, clustering, evaluating generated text, retrieval-augmented generation with LLMs (RAG), and so on. 

Obviously, in the age of BERT and LLMs, we do have methods that can map text to such a useful vector. While that pretty cool and also useful, at one point, we may have to **explain why our model considers two documents to be similar**, or not. As an hypothetical edge case, think of a court where we’d have to argue why our model returned a “wrong” text that somehow led to some sort of legal mess further downstream.

So let’s dive into two cool methods for interpretation of embeddings. 

We’ll learn how to use them and that they’re actually complementary: the first method aims at understanding the text embedding vector space itself, and the second aims at understanding how tokens contribute to overall similarity. 
We’ll call those two:

1. Decision space explanation with multi feature embeddings and metric distillation. [Code](https://github.com/flipz357/S3BERT), [Paper](https://aclanthology.org/2022.aacl-main.48)

2. Input space explanation to find salient phrase pairs. [Code](https://github.com/lucasmllr/xsbert), [Paper](https://aclanthology.org/2023.emnlp-main.980)

Don’t worry, **we’ll keep this post light-hearted**, so that you won’t need to digest much math for understanding.

## Method 1): Decision space explanation via metric distillation

This is based on a work written by me and Anette Frank. A motivation was to get some high-level explanation on similarity decisions and compose the overall similarity in a faithful way from aspectual sub-similarities.  
Us humans want to have higher-level explanations: *“These documents are similar because they’re about the same topics”*. *“These documents are dissimilar because they’re contradicting each other”*. And so on.

The basic idea is outlined in this figure:

[Vector partitioning](/assets/img/blog/partition-crop.png)

We divide the text embeddings into different sub-vectors that capture different attributes that we’re interested in! In the end, we can trace the whole similarity computation back to our high-level features. In the example, the overall similarity is 0.8. The sentences have the same topic (1.0), but opposing polarity (0.0). So we can perform all standard tasks with the full embedding, but also can do finer tasks such as searching or clustering embeddings for specific aspects we’re interested in. Indeed, these sub-embeddings or features compose the full text representation, so we can exactly trace how they’re used and weighted!

A strength of this approach may be also a downside: There's lots of freedom in how you design your interpretable metrics, which can require some time for exploration as to what works and what not.

## Method 2): Input space explanation via integrated gradients

This is a cool work by Lukas Moeller et al. For input space explanation, we’d like to know the input features that have the most impact on a decision. It’s sort of the most popular interpretability goal, where people have used attention weights, gradient analysis, Shapley values, and so on, to highlight the important input features that a model thinks are important. This is about how it’s done:

[Token attribution](/assets/img/blog/attribution-crop.png)

The sprinkling stars stand for some magic (that is math) that’s happening in the process that hands us a so-called attribution matrix. This matrix approximates the full similarity function of two documents, in a decomposed way! That means, we can check out how every pair of words contributes to the decision of our overall similarity. How is this matrix found, what’s the magic? On a high level, it’s found with the method of “integrated gradients”: Starting from a neutral input, we view how the gradients change when gradually going to our real input, integrating the curve with respect to each input feature. Since by integrating a gradient we kind of end up at our actual model function kind of, we can call this approach faithful. 

Like in every method, there's may be also some downsides to this approach: we’d need i) to run some iterative approximations which makes the method not efficient and ii) we’d have to stick using dot-product as a similarity measure. All this can lower the results on benchmarks by a tiny bit, and can reduce the practical usage in case we want to run the method for a lot of pairs. A [later paper](https://arxiv.org/abs/2402.02883) by the same authors seems to mitigate some of these concerns.

### Other approaches:

There's also interesting other papers about vectors and interpretability: Vivi Nastase shows that [matrix structures](https://arxiv.org/abs/2312.09890) can potentially capture some phenomena better than vectors. Jannis Vasmas and Rico Sennrich show that to detect meaningful differences between tokens of documents, it’s quite effective to simply use a greedy [token matching](https://arxiv.org/abs/2305.13303) similar to what’s done by BERTScore.

<details markdown="1"> 
<summary> Click to extend </summary>

[SBERT studies Meaning Representations: Decomposing Sentence Embeddings into Explainable Semantic Features](https://aclanthology.org/2022.aacl-main.48) (Opitz & Frank, AACL-IJCNLP 2022)

[An Attribution Method for Siamese Encoders](https://aclanthology.org/2023.emnlp-main.980) (Moeller et al., EMNLP 2023)


</details>


[^1] The "$&!#* vector" is derived from a quote ascribed to R. Mooney, see also [this presentation](https://aclanthology.org/attachments/P18-1198.Presentation.pdf)



