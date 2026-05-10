# DenseCap: Fully Convolutional Localization Networks for Dense Captioning

## Metadata
- **Title:** DenseCap: Fully Convolutional Localization Networks for Dense Captioning
- **Authors:** Justin Johnson (equal contribution), Andrej Karpathy (equal contribution), Li Fei-Fei
- **Venue:** CVPR 2016 (Oral)
- **Year:** 2016
- **URL:** https://cs.stanford.edu/people/karpathy/densecap/
- **Code:** https://github.com/jcjohnson/densecap

## 摘要

本文来自 Stanford Vision Lab，发表于 CVPR 2016 (Oral)。该任务提出了"密集描述"（dense captioning），要求系统同时定位图像中的显著区域并用自然语言对其进行描述。作者提出了全卷积定位网络（FCLN）架构，将定位和描述联合处理。该架构通过单次高效前向传播处理图像，无需外部区域建议，并支持一轮端到端训练。该架构结合了卷积网络、一种新颖的密集定位层和一个 RNN 语言模型。

## 核心贡献
1. **密集描述**作为一项新任务——当描述由单个单词构成时，它泛化了目标检测；当单个区域覆盖整张图像时，它泛化了图像描述（Image Captioning）。
2. **FCLN 架构**——单次前向传播，无需外部区域建议。
3. 在"逆向"模式下，模型可以通过计算每个检测区域生成给定查询的概率，在大规模图像中搜索任意文本查询（区域搜索）。

## 数据集与评估
- 在 **Visual Genome 数据集**上进行评估（94,000 张图像，410 万条区域相关的描述）。
- 在图像描述生成和检索两种任务上都展示了对基线的速度和精度提升。

## BibTeX
```
@inproceedings{densecap,
  title={DenseCap: Fully Convolutional Localization Networks for Dense Captioning},
  author={Johnson, Justin and Karpathy, Andrej and Fei-Fei, Li},
  booktitle={Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition},
  year={2016}
}
```

## 解读
这项研究教会电脑更厉害地"看图说话"。之前的电脑只能给整张照片写一句话，这项研究则教会电脑给照片里的每一个"小东西"都写一句话——比如"红色的球"、"追球的小狗"、"绿色的草地"。就像小朋友看一本图画书，能指出每个角落分别画了什么。