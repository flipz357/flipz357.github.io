---
title: Interests
layout: default
permalink: /interest
---

# Overview of research interests 🔍

#### System evaluation 😵‍💫

Even one of the simplest of all evaluation tasks (classification evaluation) is far from trivial. For an intuitive analytical overview and comparison of classification metrics such as Macro F1, Weighted F1, Kappa, Matthews Correlation Coefficient (MCC), check out this paper at [MIT press](https://doi.org/10.1162/tacl_a_00675) or [arxiv](https://arxiv.org/abs/2404.16958). Then evaluation issues typically get compounded when looking at tasks where we don't generate class labels, but generate artificial text, or other structured predictions, such as semantic graphs. Here's some work on generation evaluation ([click](https://arxiv.org/abs/2305.16819)) and semantic parsing evaluation, introducing [standardized and fine-grained matching](https://arxiv.org/abs/2305.06993).

#### Meaning representations, Explainability, and Decomposability 🧐

I like to study representations and their ability to meaningfully capture data (e.g., text, images, etc.), find ways to improve their representation power, efficiency, and interlinks. 

*Example*: *Who does what to whom*? A meaning representation (MR) tries to express this in a structured and explicit format, such as a graph. In [this paper](https://arxiv.org/abs/2206.07023) we refine neural sentence embeddings with MRs to decompose them into different interpretable aspects. It keeps the efficiency and power of the neural sentence embeddings while adding some valuable explainability! Check out [this repository](https://github.com/flipz357/S3BERT) for the code.

#### NLP for History / humanities ✨

NLP for history / humanities: Nowadays we got huge digitized historic data sets at our fingertips. How can computers help us make sense of tremendous amounts of such data? These days, I'm working within the [impresso project](https://impresso-project.ch/), a large, interdiscplinary collaboration of researchers from Switzerland (UZH and EPFL) and Luxembourg. A few years ago, I've took a stab at automatically reconstructing coordinates and movement patterns for thousands of medieval entities (🤴👸🧑‍🌾...), starting from the time of the Carolingian dynasty (ca. 750 CE) to Maximilian I. (ca. 1500 CE). Of course, "automatic" also means that there's much room for reducing the error of the resconstructions -- If you've got an idea for reducing the error in such approximations, [here's](https://github.com/flipz357/regesta-imperii-to-semgis) code and data.

#### Understanding AI usage and impact 🦙

"AI" ("KI" in German), "LLMs" (Large Language Models), or "ChatGPT", are terms that are by now familiar to millions, and oftentimes they're used as synonyms! Like it or not, the associated technology is here to stay. And it has an icreasing impact on various parts of society and social interaction. Since this technology is rather new, it seems specifically important to understand its impact on human society and economy, leveraging its strengths, but also mitigating false conceptions and learning about strategies for fair and safe usage. Some thoughts about the impact and emerging relations of this technology on/to (computational) linguistics are contained in [this piece](https://doi.org/10.1162/coli_a_00560).
