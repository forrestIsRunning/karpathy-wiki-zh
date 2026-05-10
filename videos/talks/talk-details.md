# Karpathy 重要演讲详解

---

## State of GPT @ Microsoft Build 2023

**通俗解释：**
> 这是 Karpathy 关于 GPT 最全面的演讲。他解释了：
> 1. GPT 是怎么训练出来的（从读万卷书到变聪明）
> 2. 训练 ChatGPT 的完整流程
> 3. 什么是"预训练"、"微调"、"RLHF"
>
> 他说 GPT 的训练就像上学：先读很多很多书（预训练），然后学怎么回答问题和听话（微调），最后在老师的指导下变得更有礼貌和安全（RLHF）。

:link: [YouTube](https://www.youtube.com/watch?v=bZQun8Y4L2A) | Slides: [stateofgpt.pdf](https://karpathy.ai/stateofgpt.pdf)

---

## Deep Dive into LLMs like ChatGPT

**通俗解释：**
> 打开 ChatGPT 的"肚子"，看看里面有什么。
> - 它不是一个数据库，不靠"查资料"回答
> - 它是一个"接词游戏"大师——每看到一个词，就猜下一个词是什么
> - 它训练的时候看了整个互联网的文字
>
> Karpathy 把大语言模型比作"梦中的大脑"——它会基于学过的模式创造内容，但也会"做梦"（产生幻觉）。

:link: [YouTube](https://www.youtube.com/watch?v=7xTGNNLPyMI)

---

## How I use LLMs

**通俗解释：**
> Karpathy 分享他日常怎么用 AI 工具。
> - 他用 AI 当"写作助手"——提出想法，让 AI 帮忙完善
> - 他用 AI 当"编程伙伴"——一起写代码、找bug
> - 他用 AI 当"研究助手"——快速总结长文章
>
> 他的核心观点：**别把 AI 当搜索引擎，要把它当合作者**。

:link: [YouTube](https://www.youtube.com/watch?v=EWvNQjAaOHw)

---

## Intro to Large Language Models

**通俗解释：**
> LLM（大语言模型）入门视频。
> 什么是大语言模型？简单说：一个超级会"猜词"的程序。
> 它看了几万亿个字，学会了"通常人们会这么说"。
> 然后你给它一个开头，它自己接着写下去。

:link: [YouTube](https://www.youtube.com/watch?v=zjkBMFhNj_g)

---

## Dwarkesh Podcast 2025

**通俗解释：**
> DWARKESH 播客深度访谈。Karpathy 讨论了 AI 的未来发展、开源和闭源的博弈、以及他为什么离开大公司做独立教育。

:link: [YouTube](https://www.youtube.com/watch?v=lXUZvyajciY)

---

## YC AI Startup School 2025

**通俗解释：**
> 给 AI 创业者分享经验。Karpathy 谈了他对大模型现状的看法，以及创业公司应该关注什么方向。

:link: [YouTube](https://www.youtube.com/watch?v=LCEmiRjPEtQ)

---

## GPU Mode 2024

**通俗解释：**
> 深入 GPU 编程的技术演讲。讲的是怎么让神经网络在 GPU 上跑得更快。

:link: [YouTube](https://www.youtube.com/watch?v=FH5wiwOyPX4&t=3246s)

---

## No Priors Podcast 2024

**通俗解释：**
> 和 Sarah Guo 的对话。讨论了 AI 领域的趋势、AI 安全和开源的重要性。

:link: [YouTube](https://www.youtube.com/watch?v=hM_h0UA7upI)

---

## Lex Fridman Podcast 2022

**通俗解释：**
> 和 Lex Fridman 长达 4 个小时的深度对话。
> 聊了自动驾驶、AI 安全、神经网络、特斯拉、OpenAI 等等。
> 这是了解 Karpathy 思想最好的入门访谈之一。

:link: [YouTube](https://www.youtube.com/watch?v=cdiD-9MMpb0)

---

## Tesla AI Day 2021

**通俗解释：**
> Karpathy 在 Tesla AI Day 上展示了特斯拉自动驾驶的完整技术栈。
> - 摄像头怎么捕捉图像
> - 神经网络怎么处理这些图像
> - 怎么做出驾驶决策
> - 怎么在特斯拉自研芯片上实时运行

:link: [YouTube](https://youtu.be/j0z4FweCy4M?t=2900)

---

## AI for Full Self-Driving @ CVPR 2021

**通俗解释：**
> 给计算机视觉领域的同行讲解特斯拉怎么用 AI 实现自动驾驶。
> 重点讲了"端到端学习"在自动驾驶中的应用。

:link: [YouTube](https://www.youtube.com/watch?v=g6bOwQdCJrc)

---

## AI for Full Self-Driving @ ScaledML 2020

**通俗解释：**
> 讲大规模机器学习在自动驾驶中的应用。数据怎么收集、模型怎么训练、怎么部署到车上。

:link: [YouTube](https://www.youtube.com/watch?v=hx7BXih7zx8)

---

## Tesla Autonomy Day 2019

**通俗解释：**
> 特斯拉完全自动驾驶技术日。Karpathy 展示了 Autopilot 视觉团队的进展。

:link: [YouTube](https://www.youtube.com/watch?v=Ucp0TTmvqOE&t=6678)

---

## Building the Software 2.0 Stack @ Spark-AI 2018

**通俗解释：**
> 这是 Software 2.0 概念的实践版演讲。
> 讲了怎么构建"不是写代码而是训练模型"的完整技术栈。
> 从数据标注到模型训练到部署，全链路讲解。

:link: [YouTube](https://www.youtube.com/watch?v=y57wwucbXR8)

---

## Multi-Task Learning in the Wilderness @ ICML 2019

**通俗解释：**
> "多任务学习"不是实验玩具，而是在真实世界中非常实用的技术。
> 在特斯拉，一个神经网络同时做多个任务（检测车道线、识别行人、读交通灯）。

:link: [SlidesLive](https://slideslive.com/38917690/multitask-learning-in-the-wilderness)

---

## PyTorch at Tesla @ PyTorch DevCon 2019

**通俗解释：**
> 特斯拉怎么用 PyTorch 训练自动驾驶模型。
> 从研究到生产的完整流程。

:link: [YouTube](https://www.youtube.com/watch?v=oBklltKXtDE)

---

## Heroes of Deep Learning with Andrew Ng 2017

**通俗解释：**
> 和 Andrew Ng 的对话访谈。Karpathy 分享了他从学术界到工业界的经历和感悟。

:link: [YouTube](https://www.youtube.com/watch?v=xxu4IqwKw0w)

---

## Robot Brains Podcast 2021

**通俗解释：**
> 和 Pieter Abbeel（机器人学习专家）的深度对话。
> 聊了自动驾驶、AI 的未来、深度学习的发展方向。

:link: [Podcast](https://www.therobotbrains.ai/who-is-andrej-karpathy)