## Hi!

I'm Juri Opitz, a final year PhD student at Heidelberg University. I'm interested in machine learning, with a focus on NLP (Natural Language Processing).

### Some of my interests 🔍

#### Meaning representations and Explainability 🧐🎓

How can we capture *who does what to whom* in a text? A meaning representation tries to express the answer to this questions in a structured and explicit format, such as a graph.

One of my interests is the design and application of **metrics between such representations**. While such metrics are important to check the quality of systems that generate meaning representations, an interesting potential of such metrics is that they can *explain* to us why (and in which aspects) two texts are similar, or dissimilar.

There's also an issue that prevents a more wide-spread use of meaning representations for downstream tasks: they typically require slow and complex parsers, making downstream systems inefficient and not so easy to use. And thus they become kind of less useful. Therefore, another motivation of mine is to **make meaning representations more useful**. For instance, in [this paper](https://arxiv.org/abs/2206.07023) we generate sentence embeddings with meaning representations and make them more explainable -- without requiring a parser, keeping all efficiency of the neural sentence embeddings! Check out [this repository](https://github.com/flipz357/S3BERT) for the code.

#### Classification Evaluation 🤔💭

Even though classification is a task that seems straightforward, our choice of evaluation metric for testing the performance of a classifier can differ from case to case. Here's some classic questions:

- should we use this metric or that? what does that metric actually measure?
- why do researchers compare annotators with metric a, but systems with metric b?

I've written two notes on this topic. One is an analysis of false friends: *Macro F1 and macro F1* (no typo!), here's the [paper](https://arxiv.org/abs/1911.03347). Then there are [some refined teaching notes (pdf)](https://raw.githubusercontent.com/flipz357/flipz357.github.io/main/assets/pdf/metric_primer.pdf) that I wrote during my teaching, triggered by re-occuring discussions with students in reading groups.

#### Computational humanities 🤴

Finally, a passion of mine is the analysis of historic data. In particular, I find it interesting to test the large-scale statistical analysis of patterns in collections of historic texts, exploring the European medieval ages across time and spatial axes.

For instance, we have automatically reconstructed coordinates and movement patterns for thousands of medieval entities, starting from the time of the Carolingian dynasty (~750 CE) to Maximilian I. (~ 1500 CE). Of course, "automatic" also means that there's much space for future work to reduce the error of the resconstructions.

All code for the experiments and the data is available at [this repository](https://github.com/flipz357/regesta-imperii-to-semgis).

### Publications

See [Google Scholar](https://scholar.google.de/citations?user=DzxugZIAAAAJ&hl=de)

