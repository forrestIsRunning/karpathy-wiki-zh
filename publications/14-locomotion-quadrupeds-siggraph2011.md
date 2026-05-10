# Locomotion Skills for Simulated Quadrupeds

## Metadata
- **Title:** Locomotion Skills for Simulated Quadrupeds
- **Authors:** Stelian Coros, Andrej Karpathy, Ben Jones, Lionel Reveret, Michiel van de Panne
- **Venue:** ACM Transactions on Graphics (Proceedings of SIGGRAPH 2011)
- **Year:** 2011
- **URL:** http://www.cs.ubc.ca/~van/papers/2011-TOG-quadruped/index.html

## 描述

本文提出了一个基于物理的四足模拟步态与技能集成系统。模拟的狗能够执行多种动作：行走、小跑、踱步、慢跑、横向疾驰、旋转疾驰、跳上/跳下平台、越过障碍物、坐、躺、站立、以及从摔倒中恢复。

## 技术方法

控制器依赖于几个关键抽象：步态图、双腿框架模型、柔性脊柱模型，以及通过 Jacobian 转置广泛应用的内部虚拟力。优化过程对这些控制抽象进行调参，以实现稳健的步态和具有期望运动风格的跳跃。

## 结果与评估
- 评估了步态在受到推挤干扰和在不平地形上行走时的鲁棒性。
- 将模拟运动与真实狗的拍摄运动数据进行了比较。
- 展示了四足动物运动和行为技能的广泛能力集。

## 可用资料
- 论文 PDF (2.1 MB) 和补充材料 (0.4 MB)
- Windows 二进制代码及说明文档
- 嵌入式视频（无音频）

## 资助
- NSERC（加拿大自然科学与工程研究委员会）
- GRAND NCE（图形、动画与新媒体）

## 所属机构
- 不列颠哥伦比亚大学
- 迪士尼苏黎世研究中心
- INRIA / 格勒诺布尔大学 / CNRS

## 解读
这项研究在电脑里做了一只"机器狗"，教它怎么走路、跑步、跳跃，甚至能从摔倒状态自己爬起来。这只虚拟狗狗能像真狗一样走、小跑、狂奔、跳过障碍物。就像给电脑里的小狗装上了一个"运动控制器"，告诉它四条腿该怎么动。