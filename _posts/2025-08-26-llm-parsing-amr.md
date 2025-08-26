---
title: LLMs can’t parse (yet) 
layout: default
published: true
---

# {{ page.title }}

Parsing a text into a formal meaning representation like AMR requires high precision and strict observance of [guidelines](https://github.com/amrisi/amr-guidelines/blob/master/amr.md). Interestingly, recent research seems to indicate that LLMs are rather bad at creating AMRs!

- [1] and [2] both examine GPT models for parsing via prompting. The results are mediocre at best.
- [3] finetunes LLMs and while this works better, they do not seem to achieve the same accuracy compared with a much smaller and more efficient sequence-to-sequence model.

What does this mean? For me this shows that LLMs have difficulties in following strict plans, even when fine-tuned. I find this somewhat intuitive, since they excel in pragmatics and also seem reasonably creative. Constraining their "wild nature" into a formal corset might limit their capabilities in other important NLP tasks, like dialogue or summarization, where no strict human guidelines can be defined.

Still, this shows that in tasks where utmost strictness and rule-following are required, LLMs may not always be the best tools available.

But is this inability to parse AMR really a problem, or just evidence that LLMs aren’t the right tool for this particular job? Maybe it’s less a red flag and more a reminder that non-LLM systems and LLMs can complement one another. 

## References

[1] [“You Are An Expert Linguistic Annotator”: Limits of LLMs as Analyzers of Abstract Meaning Representation](https://aclanthology.org/2023.findings-emnlp.553/) (Ettinger et al., Findings 2023)

[2] [GPT makes a poor AMR parser](https://doi.org/10.21248/jlcl.38.2025.285) (Li & Fowlie, JLCL 2025)

[3] [Evaluation of Finetuned LLMs in AMR Parsing](https://arxiv.org/abs/2508.05028) (Ho Shu Han, arxiv 2025)
