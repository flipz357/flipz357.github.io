---
layout: default
title: "How to hack an AMR Parsing evaluation"
subtitle: "And what to do about it"
---

# {{ page.title }}

**...*and what to do about it*.**

TLDR:

- 🤯 By exploting vulnerabilities in the [Smatch](https://github.com/snowblink14/smatch) metric we get *the best possible score on the benchmark* 🚀. 

- ✅ For safe evaluation, use the [Smatch++](https://github.com/flipz357/smatchpp) metric.

## Introduction

AMR parsing is a fun task, where we map texts onto little graphs that explicate their meaning, so called Abstract Meaning Representations (AMRs). Even though this post is written for folks who have a bit of prior understanding in AMR, I’ll start with an analogy to better picture the issue. If you’ve got prior AMR knowledge, feel free to jump to the [next section](#hacking-the-amr-eval).

Imagine a cooking contest that takes place regularly, say, once a year. In all events, we have the same judge, participants are amateurs, meals are scored on 0 to 100, with 100 meaning “it can’t possibly get better”. Over the years, the participants got objectively better, and also their average score issued by the judge now almost touches 85.

Suddenly, an onlooker finds that the judge seems to like meals that are a bit more on the salty side. They decide to participate, cook a basic meal, and add a significant bit more salt than would be appropriate. They receive a very high grade, say 87, winning this year’s contest. Next time, they win again, scoring 90 (how? yes, you guessed it, by adding even more salt). Finally, in the round after that, they just submit a bowl of pure salt… and score 100 points.

When seeing this, can we trust this particular judge again to oversee a competition? Probably not. Should we declare all past competitions as invalid? No, we shouldn’t do this either, since probably the participants were not aware of the salt trick and so their meals only differed very little in their saltiness, leading, on average, to mostly objective ratings of their meals.

In our scenario, participants are AMR parsers, meals are parser predictions (parses), and the judge is a metric (Smatch) based on a gold standard of how the predictions should look (reference). The salt are so-called *duplicate-edges*, which are graph edges that occur more than once. While they do not make much sense (they do not add information), the metric that’s been used for scoring parsers does accept predictions that have duplicate edges. And that’s where most of the trouble starts.

## Hacking the AMR evaluation 🕵️‍♀️ <a id="hacking-the-amr-eval"></a>

Let's get down to business. Say a reference graph (what we want to have) was “the boy wants that the girl believes him”

```
(w / want-01
      :ARG0 (b / boy)
      :ARG1 (b2 / believe-01
            :ARG0 (g / girl)
            :ARG1 b))
```

While a prediction here expresses “The duck wants (something)”.

```
(w / want-01
  	:ARG0 (d / duck))
```
 
We're gonna score this graph with the *Smatch metric*, crawling the latest version of [from github](https://github.com/snowblink14/smatch) (commit 41, but we verified the same outcome with earlier versions, too). Simply put, Smatch counts edge matches and normalizes the count with an F-score, returning a number between 0 and 1, which for convenience we put between 0 and 100. Anyway, for our example, the metric should be low, since the graphs are quite different. And it kind of is:

```
>>> F-score: 46
```

Now we add a bit of “salt” to our prediction, we're gonna twice repeat that the duck is the “ARG0” of “w / want-01”:

```
(w / want-01
      :ARG0 (d / duck)
      :ARG0 d
      :ARG0 d)
```

We score this again with the Smatch metric. It should also be low, since the graphs are totally different.

```
>>> F-score: 67
```

Okay, well, let’s see how far we can push it, we'll add the edge (w, ARG0, d) ten further times. That's the result:

```
>>> F-score: 120.
```

💥💥💥, folks, we just broke the scale... 100 was supposed to be the upper limit! On a funny side note, when adding more duplicates, the score will converge to 200. Here's a little question for the readers: 
<details> 
  <summary>Why does the evaluation score converge to 200? </summary>
   It’s because of the harmonic mean in the F-score formula. By increasing the matching edges with our duplicate trick, the precision will converge to 100, while the recall will continuosly grow (due to it being normalized by the size of the reference graph which doesn’t change in size). In the harmonic mean of the F-measure we then have: x -> inf, 2 * x * 100 / (100 + x) = 200.
</details>
<br>
⇨ So let’s conclude that duplicate edges, much like a little devil 😈, can confuse the Smatch score for a graph pair. Next we see what happens when we evaluate a parser on a *set of graph pairs* (that is, a basic parser evaluation setup).

#### There’s actually two little devils 😈😈, and they work together: hacking a full parser evaluation by manipulating only a single graph

For scoring not a graph pair, but a set of graph pairs, we usually use “Micro averaging” to get a final score. Specifically, micro averaging means that we count the matching edges over all graph pairs before applying the normalization (as opposed to, e.g., getting a score for every prediction-gold pair and averaging). 

Actually, micro averaging for getting a final parser evaluation score is perfectly fine -- were it not be for the duplicate edge issue. In that case, micro averaging becomes another little 😈 and lets us change at will the overall score, just by manipulating a single graph pair. Remember that we count edges over all graph pairs, and so a super-large graph can easily dominate the result. If we make this single graph veeeery large, the two little 😈😈 are gonna make big trouble and the overall parser evaluation score converges to the result of the large graph.

#### There’s actually yet another little 😈: Using a heuristic 

While this devil cannot hack the evaluation as much, it’s still a funny one. Before counting matching edges, we need to align the nodes between the two graphs, and that's an optimization problem. For practicality (I guess), researchers have used a hill-climber in Smatch to determine the best matching. However, there are lots of local optima, where the heuristic can get stuck in, and so we can never be sure about the quality of the solution. This leads to some funny examples, as shown by BramVan Roy in [this issue](https://github.com/snowblink14/smatch/issues/43). Suppose you have one(!) large(!) graph and compare it against itself:

```
metric(G, G)
```

What should the metric do? Well, yes, it should return a score of 100, since the graphs are the same. However, as Bram shows, hill-climbing can return a different score, which can also differ significantly over repeated calculations 🥴:

```
# First run:
>>> F-score: 92

# Second run:
>>> F-score: 87
```

Seeing this, our trust in the evaluation doesn't exactly gets raised, right?

#### Can we trust previous AMR evaluation results? 🤔

Mostly, I'd say yes. Even though we're now aware of crucial vulnerabilities in the evaluation, there probably hasn’t been an AMR parser that has exploited them to a significant degree. Looking at parsing papers, some of them also seem to use [another Smatch implementation](https://github.com/ChunchuanLv/amr-evaluation-tool-enhanced) that removes duplicate edges and drives away the first two 😈😈. Also, I guess that everyone that's played around with parsers knows that AMR parsers have gotten much better since their introduction in 2014. So the overall progress that the metric showed us over the recent years doesn't seem wrong at all. However, for the sake of fairness, reproducible research, and overall trust in evaluation scores, steps should be taken to ensure improved and safe evaluations. So:

## Can we do better?

Yes 😊! And only a little step needs to be taken for starters:

- Use [Smatch++](https://github.com/flipz357/smatchpp) instead of Smatch to protect against hacks and randomness. Smatch++ has **an optimal solver** (it is not a heuristic), and **standardizes AMRs**. With this it fixes all problems that are described above ✅. It also provides macro scoring on top of micro scoring to inform us with another score that is less biased by graph size.

Beyond that, I think it'd be also interesting to consider more evaluation methods. E.g., we might use other metrics (there are other metrics), perform some human analysis of system outputs, or be creative and think of some downstream task evaluations. Clearly, structural matching of graphs in many situations isn’t enough, especially when parsers powered by LLMs have gotten really good. To see a simple failure case of structural matching, just consider AMRs of (near)paraphrase sentences. The graphs can differ much structurally but express the same meaning. Then structural metrics would assign a low score which goes to show that they're pretty coarse. Here's some of our research on that: 1. [comparing strong AMR parsers](https://aclanthology.org/2022.eval4nlp-1.4/), 2. [Other ways of measuring AMR similarity](https://aclanthology.org/2021.tacl-1.85/). There's recently also been interesting papers such as this one on [neural AMR matching](https://aclanthology.org/2023.acl-long.892/) and two works on AMR parsing with interesting parts on evaluation. [1.](https://aclanthology.org/2023.acl-short.137) and [2.](https://aclanthology.org/2023.findings-acl.125).

#### Cite this blog post

Smatch++ is introduced in an EACL findings paper that discussed some of the issues raised above. [Here's a bib file](https://github.com/flipz357/smatchpp#citation).

#### References

<details markdown="1"> 
<summary> Click to extend </summary>

[Abstract Meaning Representation for Sembanking](https://aclanthology.org/W13-2322) (Banarescu et al., LAW 2013)

[Smatch: an Evaluation Metric for Semantic Feature Structures](https://aclanthology.org/P13-2131) (Cai & Knight, ACL 2013)

[SMATCH++: Standardized and Extended Evaluation of Semantic Graphs](https://aclanthology.org/2023.findings-eacl.118) (Opitz, Findings 2023)

[Better Smatch = Better Parser? AMR evaluation is not so simple anymore](https://aclanthology.org/2022.eval4nlp-1.4) (Opitz & Frank, Eval4NLP 2022)

[AMRs Assemble! Learning to Ensemble with Autoregressive Models for AMR Parsing](https://aclanthology.org/2023.acl-short.137) (Martínez Lorenzo et al., ACL 2023)

[Incorporating Graph Information in Transformer-based AMR Parsing](https://aclanthology.org/2023.findings-acl.125) (Vasylenko et al., Findings 2023)

[Weisfeiler-Leman in the Bamboo: Novel AMR Graph Metrics and a Benchmark for AMR Graph Similarity](https://aclanthology.org/2021.tacl-1.85) (Opitz et al., TACL 2021)

[Evaluate AMR Graph Similarity via Self-supervised Learning](https://aclanthology.org/2023.acl-long.892) (Shou & Lin, ACL 2023)

</details>






