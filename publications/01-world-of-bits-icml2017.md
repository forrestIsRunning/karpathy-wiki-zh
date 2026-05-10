# World of Bits: An Open-Domain Platform for Web-Based Agents

## Metadata
- **Title:** World of Bits: An Open-Domain Platform for Web-Based Agents
- **Authors:** Tianlin Shi, Andrej Karpathy, Linxi Fan, Jonathan Hernandez, Percy Liang
- **Venue:** Proceedings of the 34th International Conference on Machine Learning (ICML 2017)
- **Publisher:** PMLR, Volume 70, Pages 3135-3144
- **Year:** 2017
- **URL:** http://proceedings.mlr.press/v70/shi17a.html
- **PDF:** http://proceedings.mlr.press/v70/shi17a/shi17a.pdf

## 摘要

虽然模拟游戏环境极大地推动了强化学习研究的发展，但现有环境缺乏计算机视觉或自然语言处理中那种开放领域的真实感。本文介绍了 World of Bits (WoB)，一个旨在推动开放域真实网页环境中强化学习研究的平台。WoB 要求智能体使用底层的键盘和鼠标操作来完成真实的互联网任务。本文解决了两大关键挑战：(1) 策划大量多样化的网页任务；(2) 尽管网页具有 transient 特性，仍要确保明确的奖励结构和可重复性。其方法是通过众包工作者根据自然语言问题创建任务，并在真实网站上演示解决方案；通过缓存 HTTP 流量来创建可重复的网页离线近似版本。实验表明，通过行为克隆和强化学习训练的智能体能够成功完成一系列网页任务。

## 笔记
- 提出了一个基于网页的强化学习平台，允许智能体通过键盘和鼠标操作与真实网站交互。
- 利用 HTTP 缓存保证可重复性。
- 结合行为克隆和强化学习进行智能体训练。

## 解读
这项研究构建了一个名为"World of Bits"的平台，教电脑像人类一样上网。电脑需要学会自己用鼠标点击、用键盘打字，完成在网上购物或查找资料的任务。就像教一个初学者自己上网操作一样，只不过是对电脑而言的。