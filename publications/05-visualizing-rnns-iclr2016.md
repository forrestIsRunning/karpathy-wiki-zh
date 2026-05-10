# Visualizing and Understanding Recurrent Networks

## Metadata
- **Title:** Visualizing and Understanding Recurrent Networks
- **Authors:** Andrej Karpathy, Justin Johnson, Li Fei-Fei
- **Venue:** ICLR 2016 Workshop
- **Year:** 2015 (submitted June 5, 2015; revised November 17, 2015)
- **arXiv:** http://arxiv.org/abs/1506.02078
- **Subjects:** Machine Learning (cs.LG); Computation and Language (cs.CL); Neural and Evolutionary Computing (cs.NE)

## 摘要

循环神经网络（RNN），特别是带有长短期记忆（LSTM）的变体，由于在涉及序列数据的广泛机器学习问题中取得了成功应用，正在重新获得研究界的关注。然而，尽管 LSTM 在实践中提供了卓越的结果，其性能的来源及其局限性仍然没有得到很好的理解。本文以字符级语言模型作为可解释的测试平台，通过对其表示、预测和错误类型的分析来弥合这一差距。

关键发现：
- 实验揭示了可解释单元的存在，这些单元负责跟踪长距离依赖关系，如行长度、引号和括号匹配。
- 与有限视域 n-gram 模型的对比分析，将 LSTM 改进的来源追溯到长距离结构依赖。
- 本文还分析了剩余错误，并提出了进一步研究的方向。

## 笔记
- 最早提供 LSTM 内部机制详细可视化和分析的论文之一。
- 使用字符级语言模型作为可解释性测试平台。
- 揭示了 LSTM 单元学习可解释的模式（行长度跟踪、引号/括号匹配）。

## DOI
https://doi.org/10.48550/arXiv.1506.02078

## 解读
这项研究"打开"了电脑的"大脑"，看看它到底是怎么思考的。他们发现电脑里有一些"小开关"专门负责记住很长的句子中的结构信息——比如能记住这句话前面有没有出现过"（"，后面是不是该出现"）"了。就像观察一个人是如何记住别人说的一长段话的。