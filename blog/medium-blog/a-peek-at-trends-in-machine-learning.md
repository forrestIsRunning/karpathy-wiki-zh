---

**中文翻译**

Karpathy 利用他的 arxiv-sanity 数据库（包含 28,303 篇 ML 论文）分析了机器学习研究在过去 5 年的演变趋势。

**arxiv 奇点**：2017 年 3 月相关领域提交了近 2000 篇论文。会议截止日期引起明显峰值。

**深度学习框架**：TensorFlow 领先（9.1% 论文提及），Caffe 第二（4.3%），Theano 第三（2.6%）。

**研究趋势变化**：
- 神经网络相关论文从 2012 年的 25% 增长到 2017 年的接近 100%
- 计算机视觉在 2013 年后起飞（受 AlexNet 推动）
- 样本/数据效率在 2014 年达到峰值后下降（大家都在用更大的模型和数据）
- 优化/训练相关论文日益增多
- "学习"在 2015 年后成为最常见的词（元学习、主动学习、课程学习等）
- 对抗样本在 2014 年后成为热门话题
- LSTM 在 2015 年达峰后开始被其他架构超越

**结论**：数据处理和可视化虽然无聊但很有用。arxviv-sanity 现在每天处理近 700 篇新论文。

---

# A Peek at Trends in Machine Learning

- **Author:** Andrej Karpathy
- **Published:** April 7, 2017
- **URL:** https://karpathy.medium.com/a-peek-at-trends-in-machine-learning-ab8a1085a106
- **Claps:** 3K
- **Read time:** 6 min

---

*(Edit: machine learning is a large area. A good chunk of this post is about deep learning specifically, which is the subarea I am most familiar with.)*

Have you looked at [Google Trends](https://trends.google.com/trends/?cat=)? It's pretty cool — you enter some keywords and see how Google Searches of that term vary through time. I thought — hey, I happen to have this [arxiv-sanity](http://arxiv-sanity.com/) database of 28,303 (arxiv) Machine Learning papers over the last 5 years, so why not do something similar and take a look at how Machine Learning research has evolved over the last 5 years? The results are fairly fun, so I thought I'd post.

### The arxiv singularity

Let's first look at the total number of submitted papers across the arxiv-sanity categories (**cs.AI, cs.LG, cs.CV, cs.CL, cs.NE, stat.ML**), over time. We get the following:

Yes, March of 2017 saw almost 2,000 submissions in these areas. The peaks are likely due to conference deadlines (e.g. NIPS/ICML). Note that this is not directly a statement about the size of the area itself, since not everyone submits their paper to arxiv, and the fraction of people who do likely changes over time. But the point remains — that's a lot of papers to be aware of, skim, or (gasp) read.

This total number of papers will serve as the denominator. We can now look at what fraction of papers contain certain keywords of interest.

### Deep Learning Frameworks

To warm up let's look at the Deep Learning frameworks that are in use. To compute this, we record the fraction of papers that mention the framework somewhere in the full text (anywhere — including bibliography etc). For papers uploaded on March 2017, we get the following:

```
% of papers    framework    has been around for (months)
------------------------------------------------------------
 9.1           tensorflow   16
 7.1           caffe        37
 4.6           theano       54
 3.3           torch        37
 2.5           keras        19
 1.7           matconvnet   26
 1.2           lasagne      23
 0.5           chainer      16
 0.3           mxnet        17
 0.3           cntk         13
 0.2           pytorch      1
 0.1           deeplearning4j 14
```

That is, 10% of all papers submitted in March 2017 mention TensorFlow. Of course, not every paper declares the framework used, but if we assume that papers declare the framework with some fixed random probability independent of the framework, then it looks like about 40% of the community is currently using TensorFlow (or a bit more, if you count Keras with the TF backend).

We can see that Theano has been around for a while but its growth has somewhat stalled. Caffe shot up quickly in 2014, but was overtaken by the TensorFlow singularity in the last few months. Torch (and the very recent PyTorch) are also climbing up, slow and steady. It will be fun to watch this develop in the next few months — my own guess is that Caffe/Theano will go on a slow decline and TF growth will become a bit slower due to PyTorch.

### ConvNet Models

For fun, how about if we look at common ConvNet models? Here, we can clearly see a huge spike up for ResNets, to the point that they occur in 9% of all papers last March.

Also, who was talking about "*inception*" before the InceptionNet? Curious.

### Optimization algorithms

In terms of optimization algorithms, it looks like [Adam](https://arxiv.org/abs/1412.6980) is on a roll, found in about 23% of papers!

### Researchers

I was also curious to plot the mentions of some of the most senior PIs in Deep Learning (this gives something similar to citation count, but 1) it is more robust across population of papers with a "0/1" count, and 2) it is normalized by the total size of the pie):

A few things to note: "bengio" is mentioned in 35% of all submissions, but there are two Bengios: Samy and Yoshua, who add up on this plot. In particular, Geoff Hinton is mentioned in more than 30% of all new papers! That seems like a lot.

## Hot or Not Keywords

Finally, instead of manually going by categories of keywords, let's actively look at the keywords that are "hot" (or not).

### Top hot keywords

There are many ways to define this, but for this experiment I look at each unigram or bigram in all the papers and record the ratio of its max use last year compared to its max use up to last year. The papers that excel at this metric are those that one year ago were niche, but this year appear with a much higher relative frequency. The top list (slightly edited out some duplicates) comes out as follows:

```
resnet                   8.17
tensorflow               6.77
gans                     5.22
residual networks        5.01
adam                     4.35
batch normalization      2.95
fcn                      2.62
vgg16                    2.48
style transfer           2.04
gated                    2.00
deep reinforcement       1.99
lstm                     1.98
nmt                      1.94
inception                1.91
siamese                  1.90
character level          1.89
region proposal          1.88
distillation             1.82
tree search              1.81
torch                    1.79
policy gradient          1.78
encoder decoder          1.77
gru                      1.75
word2vec                 1.72
relu activation          1.72
visual question          1.71
image generation         1.70
```

For example, ResNet's ratio of 8.17 is because until 1 year ago it appeared in up to only 1.044% of all submissions (in Mar 2016), but last last month (Mar 2017) it appeared in 8.53% of submissions, so 8.53 / 1.044 ~= 8.17. So there you have it — the core innovations that became all the rage over the last year are **1) ResNets, 2) GANs, 3) Adam, 4) BatchNorm**. Use more of these to fit in with your friends. In terms of research interests, we see 1) style transfer, 2) deep RL, 3) Neural Machine Translation ("nmt"), and perhaps 4) image generation. And architecturally, it is hot to use 1) Fully Convolutional Nets (FCN), 2) LSTMs/GRUs, 3) Siamese nets, and 4) Encoder decoder nets.

### Top not hot

How about the reverse? What has seen many fewer submissions over the last year than has historically had a higher "mind share"? Here are a few:

```
fractal               0.05
learning bayesian     0.11
ibp                   0.12
texture analysis      0.14
bayesian network      0.15
differential evolution 0.17
wavelet transform     0.23
dirichlet process     0.24
```

I'm not sure what "fractal" is referring to, but more generally it looks like bayesian nonparametrics are under attack.

## Conclusion

Now is the time to submit paper on Fully Convolutional Encoder Decoder BatchNorm ResNet GAN applied to Style Transfer, optimized with Adam. Hey, that doesn't even sound too far-fetched.

:)