---
title: 'TRUNAJOD: A text complexity library to enhance natural language processing'
tags:
  - Python
  - natural language processing
  - machine learning
  - text complexity
  - text coherence
authors:
  - name: Diego A. Palma
    orcid: 0000-0003-1540-7164
    affiliation: 1
  - name: Christian Soto
    affiliation: 1
  - name: Mónica Veliz
    affiliation: 1
  - name: Bruno Karelovic
    affiliation: 1
  - name: Bernardo Riffo
    affiliation: 1
affiliations:
 - name: Universidad de Concepción
   index: 1
date: 3 March 2020
bibliography: paper.bib
---

# Summary

We present `TRUNAJOD`, a text complexity analysis tool that includes a wide variety of linguistics 
measurements that can be extracted for texts as an approximate of readability, coherence and 
cohesion. The features that `TRUNAJOD` can extract from text are based on the literature and 
can be separated into the following categories: Discourse markers, emotions, entity grid based 
measurements, givenness, lexical semantic norms, semantic measures, surface proxies, etc. In 
this first version of `TRUNAJOD`, we support mainly Spanish language, but several features support 
any language that have a proper natural language processing POS tagging and dependency parsing 
capabilities. Finally, we show how TRUNAJOD could be used in applied research.

# Statement of need

`TRUNAJOD` is aiming to solve three problems:

1. Having a standardized API for text complexity measurements
2. Having an open source code, so any researcher in the linguistics field could contribute to it
3. Making easy to build applications and tools that rely in text complexity assessment

Moreover, `TRUNAJOD` is not only taking state of the art measurements for text complexity assessment, it also comes bundled with new sets of predictors for this task, and thus `TRUNAJOD` ́s contributions are:

* Fixes periphrasis of texts, because many NLP tools have issues dealing with periphrasis. In this release, 
this only applies for Spanish.
* Adds heuristics for measurements based on clause count. TRUNAJOD provides a new algorithm for 
clause segmentation.
* TRUNAJOD provides several approximations to narrativity in these new clause segmentation dependent indices.

Text complexity assessment is a natural language processing task that can be applied for multiple problems, 
such as automatic summarization, automatic essay scoring, automatic summary evaluation, intelligent tutoring systems 
and so on. Text complexity is usually related with the readability of a text, which is dependent on several intrinsic 
properties of it, mainly cohesion and coherence.

Automatic coherence evaluation is an open problem, and there have been several studies addressing it. On one side, 
text coherence assessment has been related to how sentences connect to each other either semantically, 
or by co-referencing noun phrases. In the semantic view of coherence, Latent Semantic Analysis (LSA) [@foltz1998measurement] 
has been widely used because of its simplicity. In essence, sentences are represented as vectors, 
and coherence of the text is computed by combination of averages between sentence similarity, 
using similarity vector measurements (such as cosine distance). This approach has drawbacks, 
such as that sentence ordering does not matter. For solving this issue, other methodologies have been 
proposed, based on discourse theory, in particular the centering theory. One such approach are entity 
grids [@barzilay2008modeling] and entity graphs [@guinaudeau2013graph] that treat coherence as 
how are entities taking different roles between  sentences and how are they connected in the text. `TRUNAJOD` 
comes with all these models implemented, and thus `TRUNAJOD` is able to compute coherence based on 
sentence similarities using word vectors, and also `TRUNAJOD` as an API for dealing with entity grids an entity 
graphs, to extract such measurements.

A downside of the previous approaches for text complexity is that they only capture either CORPUS based semantics, 
or relationships between entities, and entity grids rely heavily on the dependency parser at hand and 
the co-reference resolution used, because an entity might be mentioned in several ways across a text. The problem 
with this is that, these measurements might be noisy depending on the use case, and simpler measurements would 
fit better in such cases. In `TRUNAJOD` we compute several surface proxies that has been used by several state of 
the art text assessment tools [@mcnamara2014automated] [@page1994computer]. Such surface proxies try to 
approximate intrinsic properties of the text such as narrativity, connectiveness, givenness, cohesion and coherence. 
`TRUNAJOD` includes classical measurements such as: word count, sentence count, pronoun-noun ratio, type token ratios, 
frequency index, etc. Moreover `TRUNAJOD` comes bundled with heuristics to compute clause count based metrics, such as 
ubordination, clause length, among others. To achieve this, `TRUNAJOD` adds periphrasis tags to the text in order to 
heuristically segment clauses.

One drawback of using surface proxies (shallow measurements) is that they do not capture all properties of the text, 
and just rely on approximations that are captured from the raw text. In some use cases this is not desirable 
(e.g. automatic essay scoring, intelligent tutoring systems), and these measurements should be complemented with 
others measurements that are desirable in those use cases such as lexical-semantic norms and word emotions. Lexical 
semantic norms are norms for words that are related to how words have a psychological degree of activation in 
the reader [@guasch2016spanish], and some examples of such variables are: concreteness, imageability, familiarity, arousal, valence. 
These variables might be used for reading comprehension tools (e.g. it is desirable that for reading comprehension 
assessments, feedback is concrete). Moreover, emotions could be used in such cases, and even in 
opinion mining [@sidorov2012empirical]. `TRUNAJOD` comes bundled with both types of features, and thus, average lexical- semantic norms and 
emotions could be extracted from the text. 

`TRUNAJOD` architectural design is shown in figure 1.

![Fig 1. `TRUNAJOD` architectural design.](figure1.png){ width=50% }

Basically, `TRUNAJOD` API takes as input a spaCy Doc and TRUNAJOD models (lemmatizer, synonym map, lexical-semantic norm map, etc.) and 
then it is able to compute supported text complexity metrics. It is worth noting that TRUNAJOD has available downloadable models from 
its Github repository, but currently only Spanish models are available. Nevertheless, it should be straightforward adding 
models for different languages.


# Acknowledgements

This research was supported by FONDEF (Chile) under Grant IT17I0051 "Desarrollo de una herramienta computacional para 
evaluación automática de textos del Sistema escolar chileno" ("Development of a computational tool for automatic 
assessment of Chilean school texts")

# References