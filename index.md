## Juri Opitz

Hi there! I'm Juri Opitz, a researcher interested in machine learning, NLP (Natural Language Processing), and computational linguistics. I obtained my Ph.D. from Heidelberg university, where I was advised by Anette Frank.

### Some of my interests 🔍

#### Meaning representations, Explainability, and Decomposability 🧐

How can we capture *who does what to whom* in a text? A meaning representation tries to express the answer to this questions in a structured and explicit format, such as a graph. One of my interests is investigating ways to build neural-symbolic methods from meaning representations and neural networks, leveraging the power of the latter and the explicitness and descriptiveness of the former. Indeed, while neural networks provide us with useful embeddings and generations, they tend to blend and intermingle everything in ways that we have great difficulties to understand. On the other hand, meaning representations describe the meaning with a crisp representation that is explicit and decomposable.

Aiming at the best of such worlds, in [this paper](https://arxiv.org/abs/2206.07023) we refine neural sentence embeddings with meaning representations to decompose them into different interpretable aspects. Indeed, we show that we can keep all efficiency and power of the neural sentence embeddings while getting some of that cool explainability of meaning representations! Check out [this repository](https://github.com/flipz357/S3BERT) for the code.

#### Other

- System Evaluation 😵‍💫: Even in the simplest of all evaluation tasks (classification evaluation) it's not so easy and there are false friends such as: [Macro F1 and macro F1]((https://arxiv.org/abs/1911.03347)) (no typo!). Finally, evaluation issues typically get compounded when looking at tasks where we don't generate class labels, but generate artificial text, or other structured predictions, such as semantic graphs. Here's some work on generation evaluation ([click](https://arxiv.org/abs/2305.16819)) and semantic parsing evaluation (introducing [standardiziation](https://arxiv.org/abs/2305.06993) and [discussing other issues](https://arxiv.org/abs/2210.06461).

- Computational humanities 🤴: I always liked to dig into historic data sets. How can computers help us make sense of tremendous amounts of such data? I have written some code for computing large-scale statistics in collections of historic texts, exploring the European medieval ages across time and spatial axes. For instance, we have automatically reconstructed coordinates and movement patterns for thousands of medieval entities, starting from the time of the Carolingian dynasty (~750 CE) to Maximilian I. (~ 1500 CE). Of course, "automatic" also means that there's much space for future work to reduce the error of the resconstructions. All code for the experiments and the data is available at [this repository](https://github.com/flipz357/regesta-imperii-to-semgis).

### Publications 📜

See [Google Scholar](https://scholar.google.de/citations?user=DzxugZIAAAAJ&hl=de)

### Teaching

At Heidelberg University

- Seminar on different self-attention mechanisms in transformer models
- Seminar on compuational argumentation
- Seminar on advances in semantic parsing and generation
- Lecture on advanced programming with python

### Invited talks

- Metrics of meaning representations and their interesting applications @DMR workshop at IWCS 2023


