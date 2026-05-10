# Grounded Compositional Semantics for Finding and Describing Images with Sentences

## Metadata
- **Title:** Grounded Compositional Semantics for Finding and Describing Images with Sentences
- **Authors:** Richard Socher, Andrej Karpathy, Quoc V. Le, Christopher D. Manning, Andrew Y. Ng
- **Venue:** Transactions of the Association for Computational Linguistics (TACL), Volume 2
- **Year:** 2014 (Pages 207-218)
- **ACL Anthology:** https://aclanthology.org/Q14-1017/
- **DOI:** 10.1162/tacl_a_00177

## 摘要

以往关于递归神经网络（RNN）的研究表明，这类模型能够生成组合特征向量，用于准确表示和分类句子或图像。然而，以往模型的句子向量无法准确表示基于视觉的具体语义（visually grounded meaning）。我们引入了 DT-RNN 模型，该模型使用依存树将句子嵌入到向量空间中，从而检索出那些句子所描述的图像。

与以往使用短语结构树的基于 RNN 的模型不同，DT-RNN 天然地关注句子中的动作和施动者。它能够更好地从词序和句法表达的细节中抽象出来。在寻找匹配句子描述的图像以及反过来寻找匹配图像的句子描述这两项任务上，DT-RNN 均优于其他递归和循环神经网络、核化 CCA 以及词袋基线方法。同时，DT-RNN 对描述同一幅图像的句子能够给出更相似的表示。

## 模型：DT-RNN（依存树递归神经网络）
- 使用依存树而非短语结构树来表示句子。
- 天然关注句子中的动作和施动者。
- 能更好地从词序和句法表达中抽象出来。

## 结果
- 优于其他递归神经网络和循环神经网络。
- 优于核化 CCA 和词袋基线方法。
- 任务：寻找匹配句子描述的图像，以及反过来寻找匹配图像的句子描述。
- 对于描述同一幅图像的句子，能给出更相似的表示。

## 笔记
- 视觉-语义嵌入和基于视觉的语言理解领域的早期有影响力的工作之一。
- 1500+ 次引用。
- Richard Socher 与 Andrej Karpathy 的合作，连接了 NLP 与计算机视觉。

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

## 解读
这项研究继续强化电脑"看图说话"的本领。特别的是，电脑不再死记硬背整个句子，而是先分析句子的"骨架"——谁（主语）做了什么（动词）——然后把动作和图片里正在发生的事情对应起来。就像在说"小狗追球"时，先搞明白"谁在追什么"，再去找图片里的小狗和球。