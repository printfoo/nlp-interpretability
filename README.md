# A note on NLP interpretability.
*by [Shan Jiang](https://shanjiang.me) on 01/31/2020*

This note briefly goes through some recent papers on NLP interpretability.

## 0. Normative questions.

What is interpretability?

[The Mythos of Model Interpretability](http://www.zacklipton.com/media/papers/mythos_model_interpretability_lipton2016.pdf) (Zachary C. Lipton, 2016) offered a taxonomy for this question. It started by introducing some potential benefits of interpretability such as increasing trust and enabling fair and ethical decision-making. Then, it divides the properties of interpretable models into two categories.

***Transparency***, or *how does the model work*, the opposite of *opacity* or *black-box-ness*, is the 1st category. It can be considered at three levels:
- At the level of the entire model, *simulatability*
- At the level of individual components, *decomposability*, or *intelligibility*
- At the level of the training algorithm, *algorithmic transparency*

*(post-hoc) **Explanation***, or *what else can the model tell me*, is the 2nd category. It asks for useful information without peeking beneath the interworking of the model. Some common approaches to post-hoc explanation include:
- *Text explanation* These explanations sometimes called ***rationales*** in NLP research.
- *Visualization*
- *Local explanation*
- *Explanation by example*

***Linear models* are not strictly more interpretable than neural networks**

***Humans* are not strictly more interpretable than neural networks**, either.


[Towards a Rigorous Science of Interpretable Machine Learning](https://arxiv.org/pdf/1702.08608.pdf)

## 1. Models with built-in interpretability.

### 1.1. Attention mechanism.

[Attention is not Explanation](https://arxiv.org/pdf/1902.10186.pdf)

[Attention is not not Explanation](https://arxiv.org/pdf/1908.04626.pdf)

[Is Attention Interpretable?](https://arxiv.org/pdf/1906.03731.pdf)

[Attention Interpretability across NLP Tasks](https://arxiv.org/pdf/1909.11218.pdf)

### 1.2. Hard attention mechanism.

[Rationalizing Neural Predictions](https://arxiv.org/pdf/1606.04155.pdf)

## 2. Rationale-supervised learning.

[ERASER: A Benchmark to Evaluate Rationalized NLP Models](https://arxiv.org/abs/1911.03429)
