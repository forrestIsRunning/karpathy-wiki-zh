# Object Discovery in 3D Scenes via Shape Analysis

## Metadata
- **Title:** Object Discovery in 3D Scenes via Shape Analysis
- **Authors:** Andrej Karpathy, Stephen Miller, Li Fei-Fei
- **Venue:** International Conference on Robotics and Automation (ICRA 2013)
- **Year:** 2013
- **URL:** https://cs.stanford.edu/~karpathy/discovery/
- **Dataset:** 58 indoor scenes captured via open-source Kinect Fusion implementation

## 摘要

本文提出了一种从室内环境 3D 网格中发现物体模型的方法。该流水线将场景分解为候选网格片段，并根据"物体性"（objectness）——一种区分物体与杂物的质量指标——对每个片段进行排序。

我们提出了五种内在形状度量指标：紧凑度、对称性、平滑度、局部凸性和全局凸性。我们还引入了一种重复性度量，其基本思想是：频繁出现的几何形状更有可能对应于完整的物体。

## 结果
- 在通过开源 Kinect Fusion 实现采集的 58 个室内场景上进行了评估。
- 在区分物体与杂物方面取得了 0.92 的平均精度（Average Precision）。
- 数据集已公开发布。
- 在监督和无监督两种设置下均进行了评估。

## 代码与数据
- 已发布代码（C++, Matlab），需 Point Cloud Library。
- 已发布 58 个场景的 .ply 格式彩色网格文件（kinfu_scenes.zip, 178.4 MB）。
- 提供了用于标注数据的标注界面。

## BibTeX
```
@inproceedings{Karpathy_ICRA2013,
  author = "Andrej Karpathy and Stephen Miller, and Li Fei-Fei",
  title = "Object Discovery in 3D Scenes via Shape Analysis",
  booktitle = "International Conference on Robotics and Automation (ICRA)",
  year = "2013",
}
```

## 致谢
部分受 Intel ISTC 研究基金资助。Stephen Miller 受 Hertz Foundation Google Fellowship 和 Stanford Graduate Fellowship 资助。

## 解读
这项研究教电脑看 3D 房间（就像用 3D 扫描仪拍下来的房间），让它自己发现房间里有哪些"东西"。电脑学会通过形状来判断——圆圆的可能是"球"，方方的可能是"桌子"——不需要人告诉它这是什么。就像第一次走进一个房间，自己就能看出"这里是沙发，那里是台灯"一样。