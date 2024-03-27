---
title: What’s in a vector? Explaining text embeddings and text similarity
subtitle: Two approaches: Metric distillation and integradeted gradients
layout: post
published: false
---

# {{ page.title }}

What’s in a %&!$# vector? Modeling the meaning of a sentence or text as a vector has been a long standing goal of NLP research. 
With good vector representations, we can use some simple vector algebra for performing search/information retrieval, clustering, evaluating generated text, retrieval-augmented generation with LLMs (RAG), and so on. 
So far, so good.

However, at one point, we may have to explain why our model considers two documents to be similar, or not. 
As an edge case, think of a hypothetical court where we’d have to explain why our model returned a “wrong” text that somehow led to some sort of mess further downstream.

Let’s dive into two cool methods for interpretation of embeddings. 
We’ll learn how to use them and that they’re actually complementary: the first method aims at understanding the text embedding vector space itself, and the second aims at understanding how tokens contribute to overall similarity. 
We’ll call those two:

1. Decision space explanation with multi feature embeddings and metric distillation [code, paper]

2. Input space explanation to find salient phrase pairs [code, paper]

Don’t worry, we’ll keep this post light-hearted, so that you won’t need to digest much math for understanding.

## Method 1): Decision space explanation

This is based on a work written by me and Anette Frank. A motivation was get some high-level explanation on similarity decisions and compose the overall similarity in a faithful way from aspectual sub-similarities.  
Us humans want to have higher-level explanations: *“These documents are similar because they’re about the same topics”*. *“These documents are dissimilar because they’re contradicting each other”*. And so on.

The basic idea is outlined in this figure:

<figure>

We divide the text embeddins into different sub-vectors that capture different attributes that we’re interested in! In the end, we can trace the whole similarity computation back to our high-level features. In the example, the overall similarity is 0.8. The sentences have the same topic (1.0), but opposing polarity (0.0). So we can perform all standard tasks with the full embedding, but also can do finer tasks such as searching or clustering embeddings for specific aspects we’re interested in. Indeed, these sub-embeddings or features compose the full text representation, so we can exactly trace how they’re used and weighted!



