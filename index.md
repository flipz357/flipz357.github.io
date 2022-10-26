## Welcome to my page!

I'm Juri Opitz, a researcher currently based in Heidelberg, Germany. I'm an interested in machine learning, with a focus on NLP (Natural Language Processing).

### Some of my interests

#### Meaning representations and Explainability

Given a text, how can we capture *who does what to whom?* Meaning representation try to express the answer to this questions in a structured format, such as a graph, which can be processed and understood by machines.

One of my interests is the analysis, design and application of *metrics* between such representations. While such metrics are important to check the quality of systems that generate meaning representations, an interesting potential of such metrics is that they can *explain* to us why (and in which aspects) two texts are similar, or dissimilar. 

Moreover, in my opinion, there's an important issue that prevents a more wide-spread use of meaning representations for downstream tasks: they typically require slow and complex parsers, making downstream systems inefficient and not so easy to use. And thus they become kind of less useful. Therefore, another motivation of mine is to **make meaning representations actually useful**. For instance, in [this paper](https://arxiv.org/abs/2206.07023) we generate sentence embeddings with meaning representations and make them more explainable -- without requiring a parser, keeping all efficiency of the nerual sentence embeddings! Check out [this repository](https://github.com/flipz357/S3BERT) for the code.

#### Classification Evaluation

Even though classification is a task that is straightforward, the suitability of a metric for testing the performance of a classifier can differ from case to case. In the courses that I taught and in my own research, questions that have popped up repeatedly are

- should we use this metric or that?
- why do researchers compare annotators with metric a, but systems with metric b?
- what does it mean, when a data set is "imbalanced", how should this affect the selection of an evaluation metric?

I've written two notes on this topic. One is an analysis of false friends: *Macro F1 and macro F1* (no typo!), here's the [paper](https://arxiv.org/abs/1911.03347). Then there are [some refined teaching notes (pdf)](https://raw.githubusercontent.com/flipz357/flipz357.github.io/main/pdf/metric_primer.pdf) that I wrote during my teaching, triggered by re-occuring questions with students about reasons for selecting particular evaluation metrics in papers.


#### Computational humanities

Finally, a passion of mine is the analysis of historic data. In particular, I find it interesting to test the large-scale statistical analysis of patterns in collections of historic texts, exploring the European medieval ages across time and spatial axes.

For instance, we have automatically reconstructed coordinates and movement patterns for thousands of medieval entities, starting from the time of the Carolingian dynasty (~750 CE) to Maximilian I. (~ 1500 CE). Of course, "automatic" also means that there's much space for future work to reduce the error of the resconstructions.

All code for the experiments and the data is available at [this repository](https://github.com/flipz357/regesta-imperii-to-semgis).

