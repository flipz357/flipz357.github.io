---
title: Chomsky is Wrong, or Is He?  
subtitle: My Two Cents on a Best Paper
layout: default
published: false
---

# {{ page.title }}

LLMs are mysterious creatures, and science is all over them. Noam Chomsky goes against the tide and finds them rather unimpressive. 
He argues that they cannot distinguish the possible from the impossible, and that they can learn natural and impossible languages with [‘equal facility’](https://www.nytimes.com/2023/03/08/opinion/noam-chomsky-chatgpt-ai.html). 
Interestingly, an [ACL 2024 best paper](https://arxiv.org/abs/2401.06416) just appeared that claims to refute this claim. 

How cool is it to refute the opinion of a famous (and infamous) linguist, with *empirical evidence*? 
Intrigued by this “battle of the giants” (ACL best paper vs linguistic eminence), 
I looked more closely at the paper. In the end, however, I found myself siding with Chomsky.

But first, let’s examine the paper’s key evidence, which seems to be this:

> We find that models trained on possible languages learn more efficiently, evident from lower perplexities achieved in fewer training steps.*

If you’re not sure what is meant by impossible/impossible languages, simply take English as a possible language, and English with random word order as an impossible one. 
Informally, perplexity measures the ability to predict the next word in a sequence. It expresses uncertainty, so the lower the better.

And also let's assume, for the sake of the paper's argument, that learning efficiency is equivalent to Chomsky’s notion of "facility to learn." 

In the nice graphs that are shown in the paper, we clearly see faster convergence and better perplexity on the possible languages. 
So there is the appearance that learning such impossible languages is "natively" harder for LLMs. 

So can we call it a day, Chomsky is disproven, right? Well, it appears that there is a bug with this way of reasoning.

## Different data, different perplexity levels are expected

Let's first note that their training and testing data varies across setups (e.g., standard/shuffled word order). 
Therefore, having achieved lower perplexity doesn’t necessarily equate to having learnt more efficiently, even if it would also be achieved in fewer steps. 
Conversely, the ability to learn efficiently doesn’t guarantee equally lower perplexity on any kind of data. 

As a more concrete example, take one of the paper’s impossible languages: Shuffled word order. For text with random word order we would expect that the best possible perplexity is naturally worse than for standard text.
Consider that the next word in a random word sequence is harder to predict than the next word in a non-shuffled English sentence. 
English also contains well known regularities like SVO (Subject-Verb-Object), which are broken when shuffling. Thus, the uncertainty of the model can only be higher. 

In other words, the best perplexity level that a model can be expected to achieve is different across setups, even if the vocabulary of tokens is the same. 
In fact, it could even be that the opposite is true: The model could learn impossible languages better. However, the evidence for this seems to be as scant as for the original claim. So let's stop with this speculation.

So to draw safer conclusions about whether possible langauges are harder to learn for an LLM than impossible ones, we'd need to establish which perplexities could be reached across the different data setups. 

## Conclusion: Chomsky's argument is not refuted

In sum, I'd say that what Chomsky's view on this matter has not been disproven. 
Maybe, if you view LLMs as universal computers, this view even seems more natural:
LLMs can learn all kinds of patterns with about the same facility, be they "possible" or "impossible". 
Whether you want to take it one step further and also agree with him that *therefore* LLMs can’t tell us much about human language – that's up to you.
