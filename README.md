# A note on NLP interpretability.
*Last update: 01/31/2020*

This note briefly goes through some recent papers on NLP interpretability.

## 0. Normative questions.

What is interpretability?

[The Mythos of Model Interpretability](http://www.zacklipton.com/media/papers/mythos_model_interpretability_lipton2016.pdf) (Zachary C. Lipton, 2016) offered a taxonomy for this question. It started by introducing some potential benefits of interpretability, e.g., increasing trust, revealing causality, strengthing transferability, enabling fair and ethical decision-making, etc. Then, it discussed that the properties of interpretable models broadly fall into two categories.

*Transparency*, or *how does the model work*, is the opposite of *opacity* or *black-box-ness*. It can be considered at three levels:
- *Simulatability*
- *Decomposability*
- *Algorithmic transparency*

*(post-hoc) Explanation*, or *what else can the model tell me*, is another category of interpretability properties. It asks for useful information without elucidating the interworking of the model. Some common approaches to post-hoc explanation include:
- *Text explanation* These explanations sometimes called *rationales* in NLP research.
- *Visualization*
- *Local explanation*
- *Explanation by example*

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
