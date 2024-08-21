---
title: Chomsky is wrong, or is he?  
subtitle: My two cents on LLMs for impossible languages
layout: default
published: true
---

# {{ page.title }}
***{{ page.subtitle }}***

LLMs are mysterious creatures, and science is all over them. Noam Chomsky goes against the tide and finds them rather unimpressive. 
He argues that they cannot distinguish the possible from the impossible, and that they can learn natural and impossible languages with [‘equal facility’](https://www.nytimes.com/2023/03/08/opinion/noam-chomsky-chatgpt-ai.html). 
Interestingly, an [ACL 2024 best paper](https://arxiv.org/abs/2401.06416) argues that Chomsky is wrong on this matter, bringing forward empirical evidence. 

How cool is it to refute a world famous linguist with empirical evidence? 
Intrigued by this “battle of the giants” (ACL best paper vs linguistic eminence), 
I looked more closely at the paper. In the end, however, I found myself siding with Chomsky.

### Examining the main evidence

First, let’s examine the paper’s main evidence, which seems to be this:

> We find that models trained on possible languages learn more efficiently, evident from lower perplexities achieved in fewer training steps.

If you’re not sure what is meant by possible/impossible languages, simply take English as a possible language, and English with random word order as an impossible one. 
Informally, perplexity measures the ability to predict the next symbol in a sequence. It expresses uncertainty, so the lower the better.

And also let's assume, for the sake of the paper's argument, that learning efficiency is equivalent to Chomsky’s notion of "facility to learn." 

In the nice graphs that are shown in the paper, we clearly see faster convergence and better perplexity on the possible languages. 
So there is the appearance that learning impossible languages is "natively" harder for LLMs. 

So can we call it a day, Chomsky is disproven, right? Well, it appears that there may be a bug with this way of reasoning.

### Different data, different perplexity levels to be expected

Let's first note that the paper's training and testing data varies across setups. 
Therefore, having achieved lower perplexity doesn’t necessarily equate to having learnt more efficiently, even if it would also be achieved in fewer steps. 
Similarly, the ability to efficiently learn any kind of patters doesn’t guarantee equally lower perplexity on any kind of data. 

For more conreteness, just consider the example of shuffled word order. For text with random word order we would expect that the best possible perplexity is naturally worse:
A next word in a random word sequence is harder to predict than a next word in a non-shuffled English sentence. 
English also contains regularities like SVO (Subject-Verb-Object), which are broken when shuffling. 
Thus, the uncertainty of the model on shuffled words can only be higher. 

So the best perplexity level that a model can be expected to achieve is different across setups, even if the vocabulary of tokens is the same. Without knowing these expected levels it's hard to judge whether Chomsky is wrong.

### Conclusion: Chomsky's argument is yet to be refuted

In sum, I'd say that Chomsky's view on this matter has not been disproven. 
Maybe, if we view LLMs as universal computers, it even seems natural to think that
LLMs can learn all kinds of patterns with about the same facility, be they "possible" or "impossible". 
Whether you want to take it one step further and also agree with him that *therefore* LLMs can’t tell us much about human language – that's very much up to you.
