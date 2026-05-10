# Grounded Compositional Semantics for Finding and Describing Images with Sentences

## Metadata
- **Title:** Grounded Compositional Semantics for Finding and Describing Images with Sentences
- **Authors:** Richard Socher, Andrej Karpathy, Quoc V. Le, Christopher D. Manning, Andrew Y. Ng
- **Venue:** Transactions of the Association for Computational Linguistics (TACL), Volume 2
- **Year:** 2014 (Pages 207-218)
- **ACL Anthology:** https://aclanthology.org/Q14-1017/
- **DOI:** 10.1162/tacl_a_00177

## Abstract
Previous work on Recursive Neural Networks (RNNs) shows that these models can produce compositional feature vectors for accurately representing and classifying sentences or images. However, the sentence vectors of previous models cannot accurately represent visually grounded meaning. We introduce the DT-RNN model which uses dependency trees to embed sentences into a vector space in order to retrieve images that are described by those sentences.

Unlike previous RNN-based models which use constituency trees, DT-RNNs naturally focus on the action and agents in a sentence. They are better able to abstract from the details of word order and syntactic expression. DT-RNNs outperform other recursive and recurrent neural networks, kernelized CCA and a bag-of-words baseline on the tasks of finding an image that fits a sentence description and vice versa. They also give more similar representations to sentences that describe the same image.

## Model: DT-RNN (Dependency Tree Recursive Neural Network)
- Uses dependency trees instead of constituency trees for sentence representation.
- Naturally focuses on actions and agents in a sentence.
- Better at abstracting from word order and syntactic expression.

## Results
- Outperforms other recursive and recurrent neural networks.
- Outperforms kernelized CCA and bag-of-words baselines.
- Tasks: finding an image that fits a sentence description and vice versa.
- More similar representations for sentences describing the same image.

## Notes
- One of the early influential works in visual-semantic embeddings and grounded language understanding.
- 1500+ citations.
- Richard Socher and Andrej Karpathy collaboration bridging NLP and Computer Vision.

## BibTeX
```
@article{socher-etal-2014-grounded,
  title = {Grounded Compositional Semantics for Finding and Describing Images with Sentences},
  author = {Socher, Richard and Karpathy, Andrej and Le, Quoc V. and Manning, Christopher D. and Ng, Andrew Y.},
  journal = {Transactions of the Association for Computational Linguistics},
  volume = {2},
  year = {2014},
  pages = {207--218},
  publisher = {MIT Press},
  doi = {10.1162/tacl_a_00177}
}
```

## 三岁版
这个研究继续教电脑"看图说话"的本领。特别的是，电脑不再死记硬背整个句子，而是先分析句子的"骨架"——谁（主语）做了什么（动词）——然后把动作和图片里正在发生的事情对应起来。就像小朋友说"小狗追球"时，先搞明白"谁在追什么"，再去找图片里的小狗和球。