# Deep Visual-Semantic Alignments for Generating Image Descriptions

## Metadata
- **Title:** Deep Visual-Semantic Alignments for Generating Image Descriptions
- **Authors:** Andrej Karpathy, Li Fei-Fei
- **Venue:** CVPR 2015
- **Year:** 2015
- **URL:** http://cs.stanford.edu/people/karpathy/deepimagesent/
- **Code (deprecated):** https://github.com/karpathy/neuraltalk
- **Code (successor):** https://github.com/karpathy/neuraltalk2

## 摘要

本文提出了一个能够为图像及其子区域生成自然语言描述的模型。它利用图像及其句子描述数据集来学习语言与视觉数据之间的跨模态对应关系。该对齐模型将对图像区域使用卷积神经网络与对句子使用双向 RNN 相结合，通过一个结构化目标函数将两种模态对齐到多模态嵌入空间中。一个多模态循环神经网络架构利用推断出的对齐关系来生成新颖的区域描述。

## 方法
两大核心组件：
1. **对齐模型**：图像区域的 CNN + 句子的双向 RNN + 结构化多模态嵌入目标。
2. **多模态循环神经网络**：利用对齐关系学习生成新颖的图像区域描述。

## 结果
- 在 Flickr8K、Flickr30K 和 MSCOCO 数据集上的检索实验中取得了当时最优的结果。
- 生成的描述在完整图像以及一个新的区域级标注数据集上均显著优于检索基线。

## 发布的数据集
- Flickr8K (50MB), Flickr30K (200MB), COCO (750MB)，附 VGG CNN 特征
- 所有三个数据集的 JSON 文件 (35MB)
- COCO 区域标注（覆盖 200 张 COCO 图像的 9,000 个名词短语）

## 交互式演示
- 检索排名演示（1,000 张 COCO 测试图像）
- 图像描述生成演示

## 解读
这项研究教会电脑"看图说话"——它看到一张照片，就能说出一句描述的话，比如"一个穿红衣服的女孩在荡秋千"。电脑不仅要认出照片里有什么，还要把它们串成一个通顺的句子。就像看了绘本之后，用自己的话把故事讲出来一样。