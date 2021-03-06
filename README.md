# A note on NLP interpretability.
*by [Shan Jiang](https://shanjiang.me), on 02/03/2020, available on [GitHub](https://github.com/printfoo/nlp-interpretability)* 

This note briefly goes through some recent papers on NLP interpretability.

## 0. Normative questions.

What is interpretability?

[The Mythos of Model Interpretability](https://arxiv.org/pdf/1606.03490.pdf) (Lipton, 2016) divided the properties of interpretable models into two categories.

***Transparency***, or *how does the model work*, the opposite of *opacity* or *blackboxness*, is the 1st category. It can be considered at three levels:
- At the level of the entire model, *simulatability* asks the model as a whole to be understandable by a person at once, e.g., very simple linear models or decision trees. 
- At the level of individual components, *decomposability* or *intelligibility* asks each part of the model admits an intuitive explanation, e.g., parameters of a linear model represent associations between each feature and the label.
- At the level of the training algorithm, *algorithmic transparency* asks for understanding the learning process itself, e.g., provable convergence of linear models.

***Explainability** (built-in or post-hoc)*\*, or *what else can the model tell me*, is the 2nd category. It asks for useful information without peeking under the interworking of the model. Some common approaches include:
- *Text explanation*. Just as humans often justify decisions verbally, a model can output text descriptions along with its predictions. These explanations are sometimes called ***rationales*** in NLP research.
- *Visualization* can be rendered to qualitatively demonstrate what a model has learned.
- *Local explanation* is focused on what a model depends on locally, e.g., a saliency map shows what a model is *focusing on*. 
- *Explanation by example*. Humans can also justify decisions by analogy, therefore a model can list several examples that are considered similar to the input, e.g., neighbors of word2vec representations.

(\* Called *post-hoc interpretability* in the original paper, but recent work roughly uses the term *explainability* for this category.)

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

*Generator* is a neural module designed to extract phrases from input sequences as rationales. It is called *hard* because the downstream neural module will *only* use the rationales selected by the generator.

[Rationalizing Neural Predictions](https://arxiv.org/pdf/1606.04155.pdf) (Lei et al., 2016) proposed the *generator*-*predictor*\* framework. The generator specifies a distribution over the text fragments as candidates rationals and these are passed through the predictor for prediction. Rationales are not provided during training, but are learned by including desiderata for rationales (i.e., short phrases with consecutive words) to the loss function.

Given a sequence input ***x*** and its label *y*, the generator's job is to learn a mask ***z***=gen(***x***) where each element in ***z*** is a binary mask denoting if the corresponding feature of ***x*** is selected. The predictor's job is then to take the selected rationales and make a prediction *y*=pred(gen(***x***)⊙***x***). The generator and predictor have a joint objective so that they can be trained in an end-to-end fashion. The loss function contains three parts:

- Selected rationales should be *sufficient* to make a prediction, i.e., some distance measure between conpred(·) and ground-truth *y*.
- Selected rationales should be *short*, i.e., some penalty on the norm of ***z***.
- Selected rationales should be *consecutive*, i.e., some penalty on the number of neighbors in ***z*** with opposite masks.

The *generator*-*predictor*\* framework is evaluated with the soft attention mechanism and showed improved performance.

\* Called *encoder* in the original paper, but recent work uses the term *predictor* to not confuse with the *encoder*-*decoder* framework.

[Rethinking Cooperative Rationalization: Introspective Extraction and Complement Control](https://arxiv.org/pdf/1910.13294.pdf) (Yu et al., 2019) extended (Lei et al., 2016) by introducing an *adversarial* player, the *anti-predictor*\*, whose job is to take the *unselected* rationales and make a prediction *y*=antipred((1-gen(***x***))⊙***x***), which should be insufficient if all rationales are selected. This is realized by introducing another item in the loss function:

- Unselected rationales should be *insufficient* to make a prediction, i.e., some distance measure between antipred(·) and ground-truth *y*.

There are some additional mechanisms introduced in the paper, such as an *introspective* generator.

Interestingly, this paper introduced a human evaluation method for selected rationales: human annotators are asked to give a label for the input with the rationales masked out, and intuitively, a good model should decrease the accuracy of human annotators.

\* Called *complement predictor* in the original paper.

[A Game Theoretic Approach to Class-wise Selective Rationalization](https://arxiv.org/pdf/1910.12853.pdf) (Chang et al., 2019) future extended (Yu et al., 2019) to output both justifying and countering rationales for the prediction.

[Extractive Adversarial Networks: High-Recall Explanations for Identifying Personal Attacks in Social Media Posts](https://www.aclweb.org/anthology/D18-1386.pdf) (Carton et al., 2018) used a similar approach compared to (Yu et al., 2019), but for an application of detecting personal attacks.

[Learning to Explain: An Information-Theoretic Perspective on Model Interpretation](https://arxiv.org/pdf/1802.07814.pdf) (Chen et al., 2018a) designed the generator\* to maximize the mutual information between selected features and the label.

\* Called *feature selector* in the original paper.

[L-Shapley and C-Shapley: Efficient Model Interpretation for Structured Data](https://arxiv.org/pdf/1808.02610.pdf) (Chen et al., 2018b) adopted Shapley value e from cooperative game theory as a fair scorer.

### 1.1. *Soft* rationale selection with *attention*.

*Attention* is a neural mechanism designed to weigh input sequences for downstream modules, and attention weights can be viewed as rationales. It is called *soft* because the downstream neural module will *both* use the attention and the representation of the whole input.

[Attention is not Explanation](https://arxiv.org/pdf/1902.10186.pdf) (Jain and Wallace, 2019) showed that attention does not provide *faithful* explanations, the following two senses:

- Attention weights are only weakly correlated with measures of feature importance.
- Alternative (adversarially generated) attention weights can yield the same prediction.

[Attention is not not Explanation](https://arxiv.org/pdf/1908.04626.pdf) (Wiegreffe and Pinter, 2019) continues (Jain and Wallace, 2019), and show that although attention explanation may not be *faithful*, they are *plausible*.

[Attention Interpretability across NLP Tasks](https://arxiv.org/pdf/1909.11218.pdf) (Vashishth et al., 2019) evaluated attention as explanations on diverse NLP tasks, and shows that attention weights correlate with measures of feature importance for pair sequence tasks (e.g., question answering), but not for single sequence tasks (e.g., sequence classification).

## 2. Models supervised by rationales for explainability.

NLP models that output rationales while incorporating rationales in the learning process.

[ERASER: A Benchmark to Evaluate Rationalized NLP Models](https://arxiv.org/abs/1911.03429) (DeYoung et al., 2019) unified some existing datasets containing rationales and experimented with benchmark models, which used rationales to supervise the generator.
