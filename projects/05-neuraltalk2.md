# NeuralTalk2

**GitHub:** https://github.com/karpathy/neuraltalk2
**Stars:** 5.6k | **Forks:** 1.3k | **Language:** Jupyter Notebook
**License:** MIT

## 项目介绍

用循环神经网络（RNN）给你的图片配文字。比最初的 NeuralTalk 更快、更好。相比原版，这个实现是**批量处理的、使用 Torch、可以在 GPU 上运行、并且支持 CNN 微调**。这些改进加在一起，语言模型的训练速度大幅提升（大约 100 倍）。

当前代码（以及预训练模型）的 CIDEr 得分约为 0.9，在 [codalab 排行榜](https://codalab.org/) 上大约排在第 8 位。

**更新（2016 年 9 月 22 日）：** Google Brain 团队发布了 TensorFlow 版本的 [im2txt](https://github.com/tensorflow/models/tree/master/im2txt) 模型。核心模型与 NeuralTalk2 非常相似，但效果应该更好。本仓库留作教学用途和 Torch 实现的参考。

neuraltalk2 就像给照片配"看图说话"的 AI。你看一张照片，它能告诉你"这是一只小狗在草地上跑"。它先看懂图片里有什么，然后用学过的"话"组织成句子说出来。比第一版快了一百倍，就像从走路变成坐小汽车！

## 环境要求

使用 Lua 编写，需要 Torch。额外包：`nn`、`nngraph`、`image`、`cjson`。GPU 需要：`cutorch`、`cunn`、`cudnn`。训练需要：`loadcaffe`（用于 VGGNet）、`torch-hdf5`、`h5py`。

## 评测（为你的图片配文字）

下载[预训练检查点](https://github.com/karpathy/neuraltalk2#pretrained-checkpoint-link)（600MB，包含微调后的 VGGNet 权重）。将图片放入一个文件夹，然后运行：

```
$ th eval.lua -model /path/to/model -image_folder /path/to/image/directory -num_images 10
```

使用 `-num_images -1` 处理所有图片。评测脚本会创建 `vis/vis.json`，可以使用 `python -m SimpleHTTPServer` 进行可视化。

**仅 CPU：** 下载 CPU 模型检查点，使用 `-gpuid -1`。

**集束搜索（Beam Search）：** 默认开启。使用 `-beam_size 1` 可以加快速度，但精度会降低。

## 在 MS COCO 上训练

1. 在 `coco/` 文件夹中运行预处理笔记本
2. 运行 `prepro.py` 创建 hdf5/json 数据集
3. 下载 VGG-16 Caffe 检查点
4. 运行 `th train.lua -input_h5 coco/cocotalk.h5 -input_json coco/cocotalk.json`

使用 `-language_eval 1` 在训练过程中评估 BLEU/METEOR/CIDEr 指标。

## 许可证

MIT

---

*数据获取自 https://github.com/karpathy/neuraltalk2 (2026-05-09)*