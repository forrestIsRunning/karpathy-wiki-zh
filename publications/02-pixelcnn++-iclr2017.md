# PixelCNN++: Improving the PixelCNN with Discretized Logistic Mixture Likelihood and Other Modifications

## Metadata
- **Title:** PixelCNN++: Improving the PixelCNN with Discretized Logistic Mixture Likelihood and Other Modifications
- **Authors:** Tim Salimans, Andrej Karpathy, Xi Chen, Diederik P. Kingma (all at OpenAI)
- **Venue:** ICLR 2017 (Poster)
- **Year:** 2017
- **URL:** https://openreview.net/forum?id=BJrFC6ceg
- **Code:** https://github.com/openai/pixel-cnn

## 摘要总结

本文提出了 PixelCNN 的改进实现（PixelCNN 是一种可计算似然的生成模型）。作者描述了五项关键改进：

1. 使用**离散化逻辑混合似然**替代逐像素的 256 路 softmax，加速了训练过程。
2. 以**整个像素**而非单独的 R/G/B 子像素为条件，简化了模型结构。
3. 使用**下采样**高效捕捉多分辨率结构。
4. 引入**捷径连接**进一步加速优化。
5. 使用**Dropout**进行正则化。

作者在 CIFAR-10 上报告了当时最优的对数似然结果，证明了这些改进的有效性。

## 核心贡献
- 用离散化逻辑混合似然替代 256 路 softmax
- 通过以整个像素为条件简化模型结构
- 通过下采样和捷径连接提高效率
- 在 CIFAR-10 上取得了当时最优的生成建模结果

## 解读
这项研究教电脑学会"画画"——给它看大量图片，电脑就能学会自己画出全新的、从未见过的图片。好比小朋友看了很多猫的照片之后，自己也能画出一只猫来。他们还发明了一些"小技巧"让电脑画得更快更好。