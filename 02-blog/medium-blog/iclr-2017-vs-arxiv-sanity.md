# ICLR 2017 vs arxiv-sanity

- **Author:** Andrej Karpathy
- **Published:** March 14, 2017
- **URL:** https://karpathy.medium.com/iclr-2017-vs-arxiv-sanity-d1488ac5c131
- **Claps:** 736
- **Read time:** 11 min

---

I thought it would be fun to cross-reference the [ICLR 2017](http://www.iclr.cc/doku.php?id=ICLR2017%3Amain&redirect=1) (a popular Deep Learning conference) [decisions](https://openreview.net/group?id=ICLR.cc%2F2017%2Fconference) (which fall into 4 categories: **oral**, **poster**, **workshop**, **reject**) with the number of times each paper was added to someone's library on [arxiv-sanity](http://arxiv-sanity.com/). ICLR 2017 decision making involves a number of area chairs and reviewers that decide the fate of each paper over a period of few months, while arxiv-sanity involves one person working 2 hours once a month (me), and a number of people who use it to tame the flood of papers out there. It is a battle between top down and bottom up. Lets see what happens.

[Here](https://openreview.net/group?id=ICLR.cc%2F2017%2Fconference) are the decisions for ICLR 2017. A total of 491 papers were submitted, of which 15 (3%) will be an oral, 183 (37.3%) a poster, 48 (9.8%) were suggested for workshop and 245 (49.9%) were rejected.

On the other hand we have arxiv-sanity, which has a **library** feature. In short, any registered user can add a paper to their library, and arxiv-sanity will train a personalized SVM on bigram tfidf features of the full text of all papers to make content-based recommendations to the user. The **review pool** of arxiv-sanity is as of now a total of 3195 users — this is the number of people with an account that have at least one paper in the library. Together, these users have so far included 55,671 papers into their libraries, i.e. an average of 17.4 papers.

## The experiment

Long story short, I loop over all papers in ICLR and try to find them on arxiv using an exact match on the title. Some ICLR papers are not on arxiv, and some won't get matched because the authors renamed them, or they contain weird characters, etc.

For example, lets look at the papers that got an oral at ICLR 2017. We get:

```
for oral, found 10/15 papers on arxiv with library counts:

 64 Reinforcement Learning with Unsupervised Auxiliary Tasks
 44 Neural Architecture Search with Reinforcement Learning
 38 Understanding deep learning requires rethinking generalizatio...
 28 Towards Principled Methods for Training Generative Adversaria...
 22 Learning End-to-End Goal-Oriented Dialog
 19 Q-Prop: Sample-Efficient Policy Gradient with An Off-Policy C...
 13 Learning to Act by Predicting the Future
 12 Amortised MAP Inference for Image Super-resolution
  8 Multi-Agent Cooperation and the Emergence of (Natural) Langua...
  8 End-to-end Optimized Image Compression
```

Now lets look at the **posters**:

```
for poster, found 113/183 papers on arxiv with library counts:

149 Adversarial Feature Learning
147 Hierarchical Multiscale Recurrent Neural Networks
140 Recurrent Batch Normalization
 80 HyperNetworks
 79 FractalNet: Ultra-Deep Neural Networks without Residuals
 73 Zoneout: Regularizing RNNs by Randomly Preserving Hidden Acti...
 62 Unrolled Generative Adversarial Networks
 52 Adversarially Learned Inference
 49 Quasi-Recurrent Neural Networks
 48 Do Deep Convolutional Nets Really Need to be Deep and Convolu...
```

For **workshop** suggestions we get:

```
for workshop, found 23/48 papers on arxiv with library counts:

 60 Adversarial examples in the physical world
 31 Learning in Implicit Generative Models
 16 Surprise-Based Intrinsic Motivation for Deep Reinforcement Le...
 14 Multiplicative LSTM for sequence modelling
 13 Efficient Softmax Approximation for GPUs
 12 RenderGAN: Generating Realistic Labeled Data
 12 Generalizable Features From Unsupervised Learning
 10 Programming With a Differentiable Forth Interpreter
  8 Gated Multimodal Units for Information Fusion
  8 Deep Learning with Sets and Point Clouds
```

and for **reject**, lets look at the few that arxiv-sanity users really liked, but the ICLR ACs and reviewers did not:

```
for reject, found 58/245 papers on arxiv with library counts:

 46 The Predictron: End-To-End Learning and Planning
 39 RL^2: Fast Reinforcement Learning via Slow Reinforcement Lear...
 35 Understanding intermediate layers using linear classifier pro...
 33 Hierarchical Memory Networks
 31 An Analysis of Deep Neural Network Models for Practical Appli...
 20 Low-rank passthrough neural networks
 19 Higher Order Recurrent Neural Networks
 18 Adding Gradient Noise Improves Learning for Very Deep Network...
```

Full version: https://cs.stanford.edu/people/karpathy/iclr2017.txt

There are a few papers on the top of this list that were possibly unfairly rejected.

Here's another question — what would ICLR 2017 look like if it were simply voted on by the crowd of arxiv-sanity users (of the papers we can find on arxiv)? Here is an excerpt:

```
oral:

149 Adversarial Feature Learning
147 Hierarchical Multiscale Recurrent Neural Networks
140 Recurrent Batch Normalization
 80 HyperNetworks
 79 FractalNet: Ultra-Deep Neural Networks without Residuals
 73 Zoneout: Regularizing RNNs by Randomly Preserving Hidden Acti...
 64 Reinforcement Learning with Unsupervised Auxiliary Tasks
 62 Unrolled Generative Adversarial Networks
 60 Adversarial examples in the physical world
 52 Adversarially Learned Inference
```

Note that in particular, some ICLR2017 papers that were rejected would have been almost an oral based on arxiv-sanity users alone, especially the Predictron, RL^2, "Understanding intermediate layers", and "Hierarchical Memory Networks". Conversely, some accepted papers had very little love from arxiv-sanity users.

Also, congratulations to Max et al. for "[Reinforcement Learning with Unsupervised Auxiliary Tasks](https://arxiv.org/abs/1611.05397)", which is the only paper that both groups agree should be an oral :)

## Discussion

There are several factors that skew these results. For example, the size of arxiv-sanity user base grows over time, so these results likely slightly favor papers that were published on arxiv later than earlier, as these would have come to more user's attention as new papers on the site. Also, papers are not seen with equal frequencies — for instance if some paper gets tweeted out by someone popular, more people will see it, and more people might add it to their library. And finally, a good argument could be made that on arxiv-sanity "rich get richer", because arxiv papers are not anonymous and celebrities could get more attention. In this particular case, ICLR 2017 is single-blind so this is not a differentiating factor.

Overall, my own conclusion from this experiment is that there is quite a bit of signal here. And we're getting it "for free" from a bottom up process on the internet, instead of something that takes a few hundred people several months. And as someone who has had a good amount of long, painful, stressful, rebuttals back and forth on both submitting/reviewing sides that dragged on for multiple weeks/months, I say: Maybe we don't need it. Or at the very least maybe there is a lot of room for improvement.