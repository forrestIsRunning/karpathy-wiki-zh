# PixelCNN++: Improving the PixelCNN with Discretized Logistic Mixture Likelihood and Other Modifications

## Metadata
- **Title:** PixelCNN++: Improving the PixelCNN with Discretized Logistic Mixture Likelihood and Other Modifications
- **Authors:** Tim Salimans, Andrej Karpathy, Xi Chen, Diederik P. Kingma (all at OpenAI)
- **Venue:** ICLR 2017 (Poster)
- **Year:** 2017
- **URL:** https://openreview.net/forum?id=BJrFC6ceg
- **Code:** https://github.com/openai/pixel-cnn

## Abstract Summary
The paper presents an improved implementation of PixelCNNs (tractable-likelihood generative models). The authors describe five key modifications to the original model:

1. A **discretized logistic mixture likelihood** for pixels instead of a 256-way softmax, which speeds up training.
2. Conditioning on **whole pixels** rather than individual R/G/B sub-pixels to simplify the model structure.
3. **Downsampling** to capture multi-resolution structure efficiently.
4. **Short-cut connections** to further accelerate optimization.
5. **Dropout** for regularization.

The authors report state-of-the-art log likelihood results on CIFAR-10, demonstrating the effectiveness of these changes.

## Key Contributions
- Discretized logistic mixture likelihood as a replacement for 256-way softmax
- Simplified model structure by conditioning on whole pixels
- Improved efficiency through downsampling and shortcut connections
- State-of-the-art generative modeling results on CIFAR-10

## 三岁版
这个研究教电脑学会"画画"——给它看很多图片，电脑就能学会自己画出新的、从来没见过的图片。好比小朋友看了很多猫的照片之后，自己也能画出一只猫来。他们还发明了一些"小技巧"让电脑画得更快更好。