# DenseCap: 用于密集描述的全卷积定位网络

**Website:** https://cs.stanford.edu/people/karpathy/densecap/
**GitHub:** https://github.com/jcjohnson/densecap
**作者:** Justin Johnson*, Andrej Karpathy*, Fei-Fei Li (* 同等贡献)
**会议:** CVPR 2016 (口头报告)

## 摘要

我们提出了密集描述（dense captioning）任务，这要求计算机视觉系统能够同时定位并用自然语言描述图像中的显著区域。当描述仅包含单个词时，密集描述任务泛化为目标检测；当预测区域覆盖整张图像时，则泛化为图像描述（Image Captioning）。

为了联合解决定位和描述任务，我们提出了一种全卷积定位网络（FCLN）架构，该架构通过单次高效的前向传播处理图像，不需要外部区域建议，并且可以通过一轮优化进行端到端训练。该架构由卷积网络、新型密集定位层和生成标签序列的循环神经网络语言模型组成。

我们在 [Visual Genome 数据集](https://visualgenome.org/) 上评估了我们的网络，该数据集包含 94,000 张图像和 4,100,000 条基于区域的描述。在生成和检索两种设置下，我们都观察到相比基于当前最先进方法的基线，速度和精度都有提升。

DenseCap 是"看图说话升级版"。neuraltalk 只能给整张图写一句话，但 DenseCap 能在一张图里找出好多好多东西，然后给每个东西都配一句话。比如一张有很多动物的图，它能说出"这里有只长颈鹿"、"那边有只斑马"、"树上还有一只小鸟"。就像一个很细心的导游！

## 代码和资源

可在 [GitHub](https://github.com/jcjohnson/densecap) 上获取：
- 训练/测试代码（Torch/Lua）
- 预训练模型
- 实时网络摄像头演示
- 密集描述评估指标代码

## 示例结果

### 密集描述
模型给出的预测结果，精心挑选的高分辨率、内容丰富场景。在交互式预测可视化页面（30MB）上浏览完整结果——可视化代码包含在 GitHub 中。

### 区域搜索
DenseCap 模型也可以"反向"运行来搜索文本查询。例如，输入像"长颈鹿的头"这样的描述，模型会在图像中寻找可能生成该描述的区域。这不仅仅是给图像配文字然后找字符串重叠；而是通过前向模型，检查在每个检测到的感兴趣区域上生成查询的概率。

## BibTeX

```
@inproceedings{densecap,
  title={DenseCap: Fully Convolutional Localization Networks for Dense Captioning},
  author={Johnson, Justin and Karpathy, Andrej and Fei-Fei, Li},
  booktitle={Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition},
  year={2016}
}
```

## 致谢

感谢 NVIDIA Corporation 捐赠 GPU。本研究得到 ONR MURI 资助、Intel 研究资助和 NSF ISS-1115313 的支持。

---

*数据获取自 https://cs.stanford.edu/people/karpathy/densecap/ (2026-05-09)*