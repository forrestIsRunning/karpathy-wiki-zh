# Deep Visual-Semantic Alignments for Generating Image Descriptions

**CVPR 2015 (Oral)**
:link: http://cs.stanford.edu/people/karpathy/deepimagesent/

## 三岁版

> 电脑看一张照片，然后写出一句话描述它。
> 比如看到一张"狗在草地上跑"的照片，电脑写出 "A dog running on grass"。
> 这看起来简单，但对电脑来说超级难——它要先认出"这是狗"、"这是草地"、"狗在跑",然后用正确的语法说出来。

## 核心贡献

1. **多模态对齐**：在图片和文字之间建立对应关系——把图片的区域和文字的片段"对齐"
2. **双向映射**：从图片→文字（看图说话）,以及文字→图片（用文字找图）
3. **深度神经网络**：用 CNN 处理图片，用 RNN 处理文字，组合成一个端到端系统

## 影响

这篇论文是图像描述（Image Captioning）领域的里程碑，为后续所有工作奠定了基础。

---

# DenseCap: Dense Captioning

**CVPR 2016 (Oral)**
:link: https://cs.stanford.edu/people/karpathy/densecap/

## 三岁版

> Deep Visual-Semantic Alignments 是"给整张图写一句话"。
> DenseCap 更进一步——给图里的**每一个重要区域**都写一句话。
> 比如一张街景图，它会说："左上角有一辆红色的车"、"中间有一个人在走路"、"右下角有一个交通灯"。

## 核心贡献

- 把"整图描述"变成"多区域描述"
- 全卷积定位网络，不需要候选区域预处理
- 在 Visual Genome 数据集上达到最好效果

---

# Large-Scale Video Classification with Convolutional Neural Networks

**CVPR 2014 (Oral)**
:link: https://cs.stanford.edu/people/karpathy/deepvideo/

## 三岁版

> 之前的 CNN 只看单张图片，这篇论文让 CNN 看视频。
> 视频 = 很多张快速的图片连在一起播放。
> 这篇论文用 YouTube 的海量视频训练 AI，让它学会识别视频里在发生什么。

## 核心贡献

- 在 YouTube 百万级视频上训练
- 提出多种融合时间信息的 CNN 架构
- 早期将深度学习应用于大规模视频理解的里程碑

---

# PixelCNN++

**ICLR 2017**
:link: https://openreview.net/pdf?id=BJrFC6ceg

## 三岁版

> PixelCNN 是一个能"画图"的 AI —— 它从左上角的第一个像素开始，一个像素一个像素地画出整张图。
> PixelCNN++ 改进了它，让画出来的图更清晰、训练更快。

---

# World of Bits: An Open-Domain Platform for Web-Based Agents

**ICML 2017**
:link: http://proceedings.mlr.press/v70/shi17a/shi17a.pdf

## 三岁版

> 让 AI 像人一样使用网站——点按钮、填表格、选选项。
> 就像你教一个机器人怎么在网上订机票。

---

# Visualizing and Understanding Recurrent Networks

**ICLR 2016 Workshop**
:link: http://arxiv.org/abs/1506.02078

## 三岁版

> 打开 RNN（循环神经网络）的"黑盒子"，看看里面到底是怎么工作的。
> 就像拆开一个玩具看看里面的齿轮怎么转动。

---

# PhD Thesis: Connecting Images and Natural Language

**Stanford 2016**
:link: https://cs.stanford.edu/people/karpathy/main.pdf

## 三岁版

> Karpathy 的博士论文，总结了他所有关于"让 AI 看懂图片并用语言描述"的研究。
> 就像把所有积木搭在一起，展示最终能搭出什么。

---

# 其他论文

## ImageNet Large Scale Visual Recognition Challenge (IJCV 2015)
- 1000+ 作者参与的 ImageNet 挑战总结报告
- 过去 5 年计算机视觉的进展汇总

## Deep Fragment Embeddings for Bidirectional Image-Sentence Mapping (NIPS 2014)
- 不只看图片和句子的整体，而是看"片段"级别的对应
- 实现了图片和文本的双向检索

## Grounded Compositional Semantics for Finding and Describing Images with Sentences (TACL 2013)
- 与 Richard Socher、Andrew Ng 等人合作
- 把语言组合语义和视觉内容联系起来

## Object Discovery in 3D scenes via Shape Analysis (ICRA 2013)
- 让机器人自动发现 3D 场景中的物体
- 不依赖人工标注

## Emergence of Object-Selective Features in Unsupervised Feature Learning (NIPS 2012)
- 与 Adam Coates、Andrew Ng 合作
- 无监督学习——不给标签，让 AI 自己学会识别物体

## Locomotion Skills for Simulated Quadrupeds (SIGGRAPH 2011)
- 教四足机器人学会走路和跑步
- 物理模拟环境

## Curriculum Learning for Motor Skills (AI 2012)
- "课程学习"——像教小孩一样，从简单到困难训练机器人