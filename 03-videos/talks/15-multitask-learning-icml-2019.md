# Multi-Task Learning in the Wilderness @ ICML 2019

- **Speaker:** Andrej Karpathy (Tesla)
- **Event:** ICML 2019
- **Date:** June 2019
- **URL:** https://slideslive.com/38917690/multitask-learning-in-the-wilderness
- **Source:** SlidesLive

> Note: The SlidesLive page returned HTTP 403 and could not be fetched programmatically. The description below is based on information from karpathy.ai and related sources.

## Description

At ICML 2019, Andrej Karpathy delivered a talk titled "Multi-Task Learning in the Wilderness," discussing the challenges and practical approaches to multi-task learning (MTL) in real-world production systems. Drawing from his experience leading Tesla's AI team, he covered:

- The gap between academic MTL research and real-world deployment
- Challenges of training neural networks that must handle multiple tasks simultaneously (e.g., object detection, lane prediction, depth estimation for self-driving)
- Practical engineering considerations for large-scale multi-task models
- Data efficiency and how shared representations benefit multiple tasks
- The concept of "Software 2.0" applied to multi-task learning pipelines

This talk was part of an ICML 2019 workshop focused on real-world challenges in multi-task learning.

[View Talk on SlidesLive](https://slideslive.com/38917690/multitask-learning-in-the-wilderness)

## 三岁版

这是安德烈在 ICML（一个顶级的机器学习大会）上做的演讲，讲的是"多任务学习"——就是怎么让一个 AI 同时学会做好几件事。他举了特斯拉自动驾驶的例子：一辆车需要同时识别路上的行人、看懂路标、判断距离、预测其他车的动向……就像一个人的大脑要同时处理好多事情。他发现学术界的方法在现实中不太管用，所以分享了很多他们在特斯拉实际工作中摸索出来的"野路子"经验。