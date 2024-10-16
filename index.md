## Juri Opitz

Hi there! I'm a researcher interested in machine learning, statistics, NLP (Natural Language Processing), and computational linguistics.  

My Ph.D. was obtained from Heidelberg University, where I was advised by [Anette Frank](https://www.cl.uni-heidelberg.de/nlpgroup/person/frank). I am now based in Switzerland, working for the [University of Zurich's CL department](https://www.cl.uzh.ch/en.html), affiliated with the [Impresso project](https://impresso-project.ch/).

### Overview of some work and interests 🔍

#### Meaning representations, Explainability, and Decomposability 🧐

I like to study representations and their ability to meaningfully capture data (e.g., text, images, etc.), find ways to improve their representation power or efficiency and possibly find some structural interlinks between the diverse representations. 

*Example*: *Who does what to whom*? A meaning representation (MR) tries to express this in a structured and explicit format, such as a graph. In [this paper](https://arxiv.org/abs/2206.07023) we refine neural sentence embeddings with MRs to decompose them into different interpretable aspects. It keeps the efficiency and power of the neural sentence embeddings while getting some of that cool explainability from meaning representations! Check out [this repository](https://github.com/flipz357/S3BERT) for the code.

#### System evaluation 😵‍💫

Even one of the simplest of all evaluation tasks (classification evaluation) is far from trivial. For an intuitive analytical overview and comparison of classification metrics such as Macro F1, Weighted F1, Kappa, Matthews Correlation Coefficient (MCC), check out this paper at [MIT press](https://doi.org/10.1162/tacl_a_00675) or [arxiv](https://arxiv.org/abs/2404.16958). Funnily, there's even overloaded names such as [Macro F1 and macro F1](https://arxiv.org/abs/1911.03347) (no typo!). Also, evaluation issues typically get compounded when looking at tasks where we don't generate class labels, but generate artificial text, or other structured predictions, such as semantic graphs. Here's some work on generation evaluation ([click](https://arxiv.org/abs/2305.16819)) and semantic parsing evaluation, introducing [standardiziation](https://arxiv.org/abs/2305.06993) and [discussing other issues](https://arxiv.org/abs/2210.06461).

#### Other interests ✨:

NLP for history / humanities: Nowadays we got huge digitized historic data sets at our fingertips. How can computers help us make sense of tremendous amounts of such data? In a project, we've tried automatically reconstructing coordinates and movement patterns for thousands of medieval entities (🤴👸🧑‍🌾...), starting from the time of the Carolingian dynasty (ca. 750 CE) to Maximilian I. (ca. 1500 CE). Of course, "automatic" also means that there's much room for reducing the error of the resconstructions -- If you've got a nice idea for reducing the error in such approximations, [here's](https://github.com/flipz357/regesta-imperii-to-semgis) has code and data.

### Selected works 📜

🍄 *A Closer Look at Classification Evaluation Metrics and a Critical Reflection of Common Evaluation Practice*. Available at: [MIT press](https://doi.org/10.1162/tacl_a_00675), [arxiv](https://arxiv.org/abs/2404.16958)

🍄 *SBERT studies Meaning Representations: Decomposing Sentence Embeddings into Explainable Semantic Features*. Available at: [ACL anthology](https://aclanthology.org/2022.aacl-main.48/), [arxiv](https://arxiv.org/abs/2206.07023)

🍄 *SMATCH++: Standardized and Extended Evaluation of Semantic Graphs*. Available at: [ACL anthology](https://aclanthology.org/2023.findings-eacl.118/), [arxiv](https://arxiv.org/abs/2305.06993)

For other publications, see [Google Scholar](https://scholar.google.de/citations?user=DzxugZIAAAAJ&hl=de).

### Teaching

At Heidelberg University

- Lecture on advanced programming with python
- Seminar on self-attention variants in transformer models
- Seminar on computational argumentation
- Seminar on semantic parsing and generation (two term projects of excellent students resulted in publications: [one](https://arxiv.org/abs/2106.04565) and [two](https://arxiv.org/abs/2203.13226))

At TU Darmstadt

- Co-supervised a graduate student project on summary evaluation, resulting in [this publication](https://arxiv.org/abs/2404.01701).

### Invited talks

- *Metrics of meaning representations and their interesting applications* @DMR workshop at International Conference for Comp. Semantics, 2023, Nancy, France.
- *NLP for scholars -- and the role of linguistics* @NLP retreat of *Data and Web Science Group*, 2024, Annweiler-Trifels, Germany.


