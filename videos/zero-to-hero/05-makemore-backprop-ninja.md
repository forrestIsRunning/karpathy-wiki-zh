# Building makemore Part 4: Becoming a Backprop Ninja

**中文说明：** 这是 Karpathy 的 "Zero to Hero" 系列中的一集。该系列从零开始构建神经网络，最终到达 GPT。本集的具体内容和观看链接如下。

---

# Building makemore Part 4: Becoming a Backprop Ninja

- **Source:** [YouTube](https://www.youtube.com/watch?v=q8SA3rM6ckI)
- **Author:** Andrej Karpathy
- **Date:** Oct 11, 2022
- **Views:** 340,901 views
- **Video ID:** q8SA3rM6ckI

## Description

We take the 2-layer MLP (with BatchNorm) from the previous video and backpropagate through it manually without using PyTorch autograd's loss.backward(): through the cross entropy loss, 2nd linear layer, tanh, batchnorm, 1st linear layer, and the embedding table. Along the way, we get a strong intuitive understanding about how gradients flow backwards through the compute graph and on the level of efficient Tensors, not just individual scalars like in micrograd. This helps build competence and intuition around how neural nets are optimized and sets you up to more confidently innovate on and debug modern neural networks.

!!!!!!!!!!!!
I recommend you work through the exercise yourself but work with it in tandem and whenever you are stuck unpause the video and see me give away the answer. This video is not super intended to be simply watched. The exercise is here:
https://colab.research.google.com/dri...
!!!!!!!!!!!!

Links:
makemore on github: https://github.com/karpathy/makemore
jupyter notebook I built in this video: https://github.com/karpathy/nn-zero-t...
collab notebook: https://colab.research.google.com/dri...
my website: https://karpathy.ai
my twitter:   / karpathy  
our Discord channel:   / discord  

Supplementary links:
Yes you should understand backprop:   / yes-you-should-understand-backprop  
BatchNorm paper: https://arxiv.org/abs/1502.03167
Bessel’s Correction: http://math.oxford.emory.edu/site/mat...
Bengio et al. 2003 MLP LM https://www.jmlr.org/papers/volume3/b... 

Chapters:
00:00:00 intro: why you should care & fun history
00:07:26 starter code
00:13:01 exercise 1: backproping the atomic compute graph
01:05:17 brief digression: bessel’s correction in batchnorm
01:26:31 exercise 2: cross entropy loss backward pass
01:36:37 exercise 3: batch norm layer backward pass
01:50:02 exercise 4: putting it all together
01:54:24 outro

