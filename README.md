# A note on NLP interpretability.
*by [Shan Jiang](https://shanjiang.me) on 01/31/2020*

This note briefly goes through some recent papers on NLP interpretability.

## 0. Normative questions.

What is interpretability?

[The Mythos of Model Interpretability](http://www.zacklipton.com/media/papers/mythos_model_interpretability_lipton2016.pdf) (Zachary C. Lipton, 2016) divided the properties of interpretable models into two categories.

***Transparency***, or *how does the model work*, the opposite of *opacity* or *black-box-ness*, is the 1st category. It can be considered at three levels:
- At the level of the entire model, *simulatability* asks the model as a whole to be understandable by a person at once, e.g., very simple linear models or decision trees. 
- At the level of individual components, *decomposability* or *intelligibility* asks each part of the model admits an intuitive explanation, e.g., parameters of a linear model represent associations between each feature and the label.
- At the level of the training algorithm, *algorithmic transparency* asks for understanding the learning process itself, e.g., provable convergence of linear models.

***Explainability** (post-hoc)*, or *what else can the model tell me*, is the 2nd category. It asks for useful information without peeking under the interworking of the model. Some common approaches include:
- *Text explanation*. Just as humans often justify decisions verbally, a model can output text descriptions along with its predictions. These explanations are sometimes called ***rationales*** in NLP research.
- *Visualization* can be rendered to qualititvely demonstrate what a model has learned.
- *Local explanation* is focus on what a model depends on locally, e.g., a saliency map shows what a model is *focusing on*. 
- *Explanation by example*. Humans can also justify decisions by analogy, therefore a model can list several examples that are considered similar to the input, e.g., neighbors of word2vec representations.

Under these properties, the authors note that *linear models are not strictly more interpretable than neural networks*, e.g., linear models with high dimensional features lose simulatability, with ill-curated features lose decomposability. In addition, *humans are not strictly more interpretable than neural networks*, either, as human exhibit none of the transparency properties.

[Towards a Rigorous Science of Interpretable Machine Learning](https://arxiv.org/pdf/1702.08608.pdf)

## 1. Models with (some) built-in explainability.

### 1.1. Attention mechanism.

[Attention is not Explanation](https://arxiv.org/pdf/1902.10186.pdf)

[Attention is not not Explanation](https://arxiv.org/pdf/1908.04626.pdf)

[Is Attention Interpretable?](https://arxiv.org/pdf/1906.03731.pdf)

[Attention Interpretability across NLP Tasks](https://arxiv.org/pdf/1909.11218.pdf)

### 1.2. Hard attention mechanism.

[Rationalizing Neural Predictions](https://arxiv.org/pdf/1606.04155.pdf)

## 2. Models surpervised by rationales for explainability.

[ERASER: A Benchmark to Evaluate Rationalized NLP Models](https://arxiv.org/abs/1911.03429)
