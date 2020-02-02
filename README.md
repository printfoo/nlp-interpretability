# A note on NLP interpretability.
*by [Shan Jiang](https://shanjiang.me) on 02/01/2020*

This note briefly goes through some recent papers on NLP interpretability.

## 0. Normative questions.

What is interpretability?

[The Mythos of Model Interpretability](https://arxiv.org/pdf/1606.03490.pdf) (Lipton, 2016) divided the properties of interpretable models into two categories (some notes are my own based on more recent work).

***Transparency***, or *how does the model work*, the opposite of *opacity* or *blackboxness*, is the 1st category. It can be considered at three levels:
- At the level of the entire model, *simulatability* asks the model as a whole to be understandable by a person at once, e.g., very simple linear models or decision trees. 
- At the level of individual components, *decomposability* or *intelligibility* asks each part of the model admits an intuitive explanation, e.g., parameters of a linear model represent associations between each feature and the label.
- At the level of the training algorithm, *algorithmic transparency* asks for understanding the learning process itself, e.g., provable convergence of linear models.

***Explainability** (built-in or post-hoc)*, or *what else can the model tell me*, is the 2nd category. It asks for useful information without peeking under the interworking of the model. Some common approaches include:
- *Text explanation*. Just as humans often justify decisions verbally, a model can output text descriptions along with its predictions. These explanations are sometimes called ***rationales*** in NLP research.
- *Visualization* can be rendered to qualitatively demonstrate what a model has learned.
- *Local explanation* is focused on what a model depends on locally, e.g., a saliency map shows what a model is *focusing on*. 
- *Explanation by example*. Humans can also justify decisions by analogy, therefore a model can list several examples that are considered similar to the input, e.g., neighbors of word2vec representations.

Note that this division is not absolute, and some properties of interpretability fall in between a mixture of both.

Under these properties, the authors note that *linear models are not strictly more interpretable than neural networks*, e.g., linear models with high dimensional features lose simulatability, with ill-curated features lose decomposability. Also, *humans are not strictly more interpretable than neural networks*, either, as humans exhibit none of the transparency properties.

**The rest of the reading list contains technical papers focused on *explainability***. *Transparency* often requires a specialized architectural choice of neural networks, e.g., module networks, that do not yet reach accuracies comparable to blackbox approaches, while *explainability* can be achieved by imposing constraints on existing neural network architectures.

[Towards a Rigorous Science of Interpretable Machine Learning](https://arxiv.org/pdf/1702.08608.pdf) (Doshi-Velez and Kim, 2017) discussed a taxonomy to evaluate interpretability, which includes:

- Application-grounded evaluation, which involves domain experts to evaluate real applications.
- Human-grounded evaluation, which involves lay humans to evaluate simplified tasks.
- Functionally-grounded evaluation, which involves no humans and uses some proxy to measure interpretability.

## 1. Models with (some) intrinsic explainability.

NLP models that output rationales without learning rationales.

### 1.2. *Hard* rationale selection with *generator*.

[Rationalizing Neural Predictions](https://arxiv.org/pdf/1606.04155.pdf) (Lei et al., 2016)

[Rethinking Cooperative Rationalization: Introspective Extraction and Complement Control](https://arxiv.org/pdf/1910.13294.pdf) (Yu et al., 2019)

[A Game Theoretic Approach to Class-wise Selective Rationalization](https://arxiv.org/pdf/1910.12853.pdf) (Chang et al., 2019) future extended (Yu et al., 2019) to output both justifying and countering rationales for the prediction.

[Extractive Adversarial Networks: High-Recall Explanations for Identifying Personal Attacks in Social Media Posts](https://www.aclweb.org/anthology/D18-1386.pdf) (Carton et al., 2018) used a similar approach compared to (Yu et al., 2019), but for an application of detecting personal attacks.

### 1.1. *Soft* rationale selection with *attention*.

[Attention is not Explanation](https://arxiv.org/pdf/1902.10186.pdf) (Jain and Wallace, 2019)

[Attention is not not Explanation](https://arxiv.org/pdf/1908.04626.pdf) (Wiegreffe and Pinter, 2019)

[Is Attention Interpretable?](https://arxiv.org/pdf/1906.03731.pdf) (Serrano and Smith, 2019)

[Attention Interpretability across NLP Tasks](https://arxiv.org/pdf/1909.11218.pdf) (Vashishth et al., 2019)

## 2. Models surpervised by rationales for explainability.

NLP models that output rationales while incorporating rationales in the learning process.

[ERASER: A Benchmark to Evaluate Rationalized NLP Models](https://arxiv.org/abs/1911.03429) (DeYoung et al., 2019) unified some existing datasets containing rationales and experimented with benchmark models, which used rationales to supervise the generator.
