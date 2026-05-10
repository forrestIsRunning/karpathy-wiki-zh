# Large-Scale Video Classification with Convolutional Neural Networks

## Metadata
- **Title:** Large-Scale Video Classification with Convolutional Neural Networks
- **Authors:** Andrej Karpathy, George Toderici, Sanketh Shetty, Thomas Leung, Rahul Sukthankar, Li Fei-Fei
- **Venue:** CVPR 2014
- **Year:** 2014
- **URL:** https://cs.stanford.edu/people/karpathy/deepvideo/
- **Dataset:** https://github.com/gtoderici/sports-1m-dataset

## 摘要

卷积神经网络（CNN）已经被证明是解决图像识别问题的强大模型。受这些结果的鼓舞，我们利用一个包含 100 万个 YouTube 视频（分属 487 个类别）的新数据集，对 CNN 在大规模视频分类上的应用进行了广泛的实证评估。我们研究了多种在时间域上扩展 CNN 连接性的方法，以利用局部时空信息，并提出了一种多分辨率、中央凹式架构，作为加速训练的有效方案。

我们最佳的时空网络相比基于强特征提取的基线方法表现出了显著提升（从 55.3% 提升至 63.9%），但与单帧模型相比仅取得了一般性的改进（从 59.3% 提升至 60.9%），这一结果令人惊讶。我们进一步通过在 UCF-101 动作识别数据集上重新训练最高层来研究所提最佳模型的泛化性能，并观察到了相比 UCF-101 基线模型的显著提升（从 43.9% 提升至 63.3%）。

## Sports-1M 数据集
- 1,133,158 个视频 URL，使用 YouTube Topics API 自动标注了 487 个运动标签。
- 基于 Creative Commons 3.0 许可。
- 代码和数据集已在 GitHub 上发布。

## 关键发现
- 基于 CNN 的带有时空融合的视频分类。
- 相比单帧模型的提升幅度小得出奇（仅 +1.6%），这表明单帧层面的外观信息已经包含了大量判别信号。
- 用于高效训练的多分辨率中央凹式架构。
- 在 UCF-101 上良好的迁移学习表现。

## BibTeX
```
@inproceedings{KarpathyCVPR14,
  title     = {Large-scale Video Classification with Convolutional Neural Networks},
  author    = {Andrej Karpathy and George Toderici and Sanketh Shetty and Thomas Leung and Rahul Sukthankar and Li Fei-Fei},
  year      = {2014},
  booktitle = {CVPR}
}
```

## 解读
这项研究教电脑"看视频认东西"。他们给电脑看了一百万个 YouTube 视频（全是运动类的），电脑要认出视频里是"打篮球"还是"游泳"。结果发现，电脑光看视频里的一帧画面（一张快照）就已经很厉害了，多看几帧帮助不大。就像让小朋友仅凭一张照片就能猜到是在做什么运动。