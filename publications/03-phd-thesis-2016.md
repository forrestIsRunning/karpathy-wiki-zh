# Connecting Images and Natural Language

## Metadata
- **Title:** Connecting Images and Natural Language
- **Author:** Andrej Karpathy
- **Degree:** Doctor of Philosophy (Computer Science)
- **Institution:** Stanford University
- **Date:** August 2016
- **Adviser:** Fei-Fei Li
- **Reading Committee:** Fei-Fei Li, Percy Liang, Christopher Manning
- **URL:** https://cs.stanford.edu/people/karpathy/main.pdf
- **Online:** http://purl.stanford.edu/wf528qt3314

## 摘要

人工智能领域的一个长期目标是开发能够感知和理解我们周围丰富视觉世界的智能体，并且能够用自然语言与我们交流这些视觉信息。

近年来，由于计算基础设施、数据收集和算法的同步进步，我们在实现这一目标上取得了重大进展。视觉识别领域的进展尤其迅速，计算机现在能够以与人类相媲美甚至在某些方面（如识别狗的品种）超越人类的性能对图像进行分类。然而，尽管取得了令人鼓舞的进展，视觉识别的大多数进步仍然停留在为一幅图像分配一个或几个离散标签的层面（例如：人、船、键盘等）。

在本论文中，我们开发了连接视觉数据域和自然语言表述域的模型与技术，实现了两个域之间的跨域翻译。具体来说：

1. 首先，我们引入了一个将图像和句子共同嵌入到多模态嵌入空间的模型。该空间使我们能够识别出描述任意句子的图像；反之，我们也能找到描述任意图像的句子。
2. 其次，我们开发了一个图像描述模型，该模型能够接收图像并直接生成句子描述，而不受限于有限的预设句子集合。
3. 最后，我们描述了一个能够接收图像并对其所有显著部分进行定位和描述的模型。我们还证明了该模型可以反向使用——接收任意描述（例如"白色运动鞋"），并在大量图像集合中高效定位所描述的概念。

从建模角度来看，我们没有设计显式算法并在复杂的处理流水线中编排图像和句子的处理流程，而是设计了混合卷积神经网络和循环神经网络架构，通过单一网络连接视觉数据和自然语言表述。这种方法享有神经网络的诸多优势，包括使用简单同质的计算（易于在硬件上并行化），以及端到端训练带来的强大性能。

## 论文大纲
1. 引言
2. 深度学习基础（监督学习、优化、反向传播、神经网络）
3. Deep Visual-Semantic Alignments (CVPR 2015)
4. Deep Fragment Embeddings (NIPS 2014)
5. DenseCap: Dense Captioning (CVPR 2016)
6. 结论

## 致谢
- 导师：Fei-Fei Li
- 感谢 Chris Manning, Percy Liang, Vladlen Koltun, Andrew Ng, Daphne Koller, Sebastian Thrun
- 合作者：Justin Johnson, Stephen Miller, Adam Coates, Armand Joulin, Olga Russakovsky, Jon Krause, Richard Socher
- 在 Google 和 DeepMind 的实习经历
- 资助：ONR MURI, Intel, Yahoo! Labs, NVIDIA

## 解读
这是 Andrej Karpathy 的博士毕业论文，他教会电脑"看图说话"。电脑看到一张照片，不光能认出里面有"人"、"狗"、"船"，还能说出"一个小朋友在公园里遛狗"。就像教一个初学者看到图画书时，能够讲出画里的故事一样。