# Zero to Hero 系列

> Karpathy 最著名的教程系列。从零开始，一步步构建 GPT。

## 三岁版

这个系列教你：
1. 先从最简单的开始——预测"下一个字母"是什么
2. 慢慢学会预测"下一个词"
3. 最后你竟然能自己从零写出一个**迷你版 ChatGPT**！

就像学搭积木：先搭一块，再搭更多，最后搭出一个城堡。

## 官方课程介绍

来自 https://karpathy.ai/zero-to-hero.html：

> "一门从零开始在代码中构建神经网络的课程。我们从反向传播的基础开始，逐步构建到现代深度神经网络，如 GPT。在我看来，语言模型是学习深度学习的绝佳起点，即使你最终想去其他领域（如计算机视觉），因为大多数知识都是可以迁移的。"

**先修要求：** 扎实的 Python 编程 + 入门级数学（如导数、高斯分布）

## 系列目录

:link: 课程主页: https://karpathy.ai/zero-to-hero.html
:link: YouTube 播放列表: https://www.youtube.com/playlist?list=PLAqhIrjkxbuWI23v9cThsA9GvCAUhRvKZ

| # | 时长 | 视频 | 内容 | 难度 |
|---|------|------|------|------|
| 1 | 2h25m | The spelled-out intro to neural networks and backpropagation: building micrograd | 从最基础开始：搭建第一个神经网络，理解反向传播，完全手把手 | :green_book: |
| 2 | 1h57m | The spelled-out intro to language modeling: building makemore | bigram 字符级语言模型，引入 torch.Tensor | :green_book: |
| 3 | 1h15m | Building makemore Part 2: MLP | 多层感知器字符级语言模型，ML 基础知识（学习率、超参数、过拟合） | :green_book: |
| 4 | 1h55m | Building makemore Part 3: Activations & Gradients, BatchNorm | 激活函数、梯度统计分析、Batch Normalization | :orange_book: |
| 5 | 1h55m | Building makemore Part 4: Becoming a Backprop Ninja | **反向传播忍者**——不用 PyTorch autograd，手动反向传播 | :red_circle: |
| 6 | 56m | Building makemore Part 5: Building a WaveNet | 树状结构深度网络，到达 WaveNet 架构 | :red_circle: |
| 7 | 1h56m | Let's build GPT: from scratch, in code, spelled out. | **核心视频**：从零构建 GPT！跟着 Attention Is All You Need + GPT-2/3 论文 | :red_circle: |
| 8 | 2h13m | Let's build the GPT Tokenizer | 分词器——LLM 中从字符串到 token 的翻译层 | :orange_book: |
| 9 | 待定 | Attention 机制深度讲解 | Transformer 的核心——注意力机制（持续更新中） | :red_circle: |

## 学习方法（Karpathy 的建议）

1. **跟着代码写**——不要只看，要自己打一遍
2. **卡住了很正常**——停下来，再看一遍，查资料
3. **完成比完美重要**——系列很长，慢慢来

## 为什么这个系列这么牛

1. **不用框架**——从零开始写，用纯 Python + 一点点 PyTorch
2. **代码在手**——所有代码开源
3. **极慢教学**——每个细节都讲，不跳步
4. **最终到达 GPT**——你真的能理解 ChatGPT 是怎么工作的

## 先修知识

- 基础的 Python
- 一点点高中数学（导数就够了）
- 耐心和好奇心

## 三句话总结

1. 从零开始用 Python 构建神经网络
2. 一步步走到 GPT 架构
3. 最终让你真正理解大语言模型怎么工作