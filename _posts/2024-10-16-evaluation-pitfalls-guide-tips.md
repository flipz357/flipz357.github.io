---
title: Evaluation Quirks, Pitfalls and Some General Recommendations 
layout: default
published: true
---

# {{ page.title }}

I’ve been observing system evaluation practice for close to 10 years. Thought to share a few funny and intriguing things that I noted. 

Structure of this post:

- [Intriguing Evaluation Quirks](#six-intriguing-evaluation-quirks)
- [General Evaluation Recommendations](#evaluation-tips)
- [Detailed References](#detailed-references)

## Six Intriguing Evaluation Quirks

### Doppelganger metrics:

1) *Doppelganger metrics by name*: Folks have been using two metrics called “macro F1” for multi-class evaluation. They can differ up to 50 points!

2) *Doppelganger metrics by implementation*: For multi-class evaluation, “micro F1” is the same as “Accuracy”.

### Implementation bugs:

3) *Optimistic result because of double-counting*: By improperly evaluating retrieved instances in an IR setting, the F1 score can rise up to 200% points, kind of exploding the scale which is supposed to end at 100%. 

4) *Optimistic result because of tie-breaking*: Sometimes, evaluation scores can be optimistic. This can happen, e.g., when ties in an ensemble classifier are resolved using the gold label.

### Quirky metric properties:

5) *Wrong prediction, better score.* For MCC and Kappa, there can be a situation where a wrong prediction would increase the score.

### Ambiguous Metric Goals:

6) *“Balance”*: Researchers are often wishing for a “balance” when they’re evaluating a system. This “balance” is then said to be achieved by using metrics such as MCC or macro F1. But it’s actually not clear what this balance is, and how these metrics achieve this. If we define “balance” in the sense of a metric being invariant to class prevalence, then only macro Recall is actually “balanced”.

—

## Evaluation Tips

My basic *simple take-aways* from such evaluation quirks are:

Try to become aware of what an evaluation metric actually measures.
Become aware of the evaluation problem.
This knowledge helps you select a metric.
Make sure it’s correctly implemented.

For deeper reading, and to help practitioners and researchers with this, I’ve written a paper that explores how to select the right metrics and make more sense of their behavior:

> ***A Closer Look at Classification Evaluation Metrics and a Critical Reflection of Common Evaluation Practice***

Links: 
[journal](https://doi.org/10.1162/tacl_a_00675),
[arxiv](https://arxiv.org/abs/2404.16958)


To give a quick idea of the work: The paper analyzes how metrics behave depending on factors like how often a class appears (prevalence) and the model’s tendency to predict certain classes (classifier bias). Metrics analyzed: Accuracy, macro Recall and Precision, F1, weighted F1, macro F1, Kappa, MCC. A finding, for instance, is that in a strict sense, only macro Recall is “balanced”.


## Detailed references

Point 1) **“macro F1 doppelgangers”**

See 4.4 in [this metric overview](https://doi.org/10.1162/tacl_a_00675). For a deeper analysis of the relationships of the two F1 formulas that proves their difference see [“Macro F1 and Macro F1](https://doi.org/10.48550/arXiv.1911.03347).

Point 2) **“Micro F1 = Accuracy”**
I think that’s already known to some folks, but probably not to all. If you need to see the simple derivation, look at, e.g., [Appendix A](https://doi.org/10.1162/tacl_a_00675).

Point 3) **“200% F1 score”**

Essentially, what has happened is using a function like this for calculating recall:

```python
 def misleading_recall(cand, ref):
      for pred in cand:
             If pred in ref:
                   count += 1
      return count / len(ref)
```

Now if you feed a list into this function where the same element accidentally occurs multiple times (can happen in generative AI), go figure! With a recall that’s approaching infinity, the F1 score approaches 200. 

I observed this in evaluation of semantic parsing, a popular NLP task that has even been targeted by NeurIPS papers. Potentially, there are other applications who also suffer from this bug.

I prepared a [github repository](https://github.com/flipz357/FunnyMetrics) so you can simply reproduce this quirk!

Point 4) **“Optimistic evaluation”**

There’s been a very popular ACL paper for low-resource text classification with a super cool and simple method. GZIP distance and KNN! It provides promising results – but the results are not quite as strong as shown in the paper (it doesn’t outperform BERT), due to a quirk in the evaluation. See [my writeup here](https://arxiv.org/abs/2307.15002), and [Ken Schutte’s blogpost here](https://kenschutte.com/gzip-knn-paper2/).

Point 5) **“Wrong prediction can increase score”**

See Section 4.7 in the [metric overview](https://doi.org/10.1162/tacl_a_00675).

Point 6) **“Concept of “Balance””**

For example, one notion of such a “balance” could be understood as a wish for prevalence-invariance, that is, a metric yields the same score when label prevalences are different (e.g., say 95/5 positive/negative class vs.  5/95 positive/negative class). It is accomplished by a very simple metric: macro Recall. See property V and Section 4.2 in the [metric overview](https://doi.org/10.1162/tacl_a_00675).
