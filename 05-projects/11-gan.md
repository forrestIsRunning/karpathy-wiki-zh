# Generative Adversarial Networks in JS

**Website:** https://cs.stanford.edu/people/karpathy/gan/

## Description

An interactive browser-based demo of Generative Adversarial Networks (GANs). Implements the GAN framework introduced by Ian Goodfellow et al. using a 2-layer network from scalar to scalar (with 30 hidden units and tanh nonlinearities) for modeling both generator and discriminator networks.

The demo attempts to reproduce a figure from the original GAN paper, but as a live, interactive webpage. The author notes "things are not quite as nice in practice."

### Interactive Controls

- **Reset** — restart the training
- **Toggle 1D/2D** — switch between 1D and 2D data distributions
- **Increase/Decrease learning rate** — adjust training speed

### Color Code

- True data distribution
- Generator network from uniform noise in U[0,1]
- Discriminator network

---

*Fetched from https://cs.stanford.edu/people/karpathy/gan/ on 2026-05-09*

## 三岁版

GAN 就像一个会"造假的画家"和"小侦探"在你面前玩看画猜真假的游戏。造假画家努力画出以假乱真的画，小侦探努力找出哪张是假的。两个人越玩越厉害，最后造假画家画出来的东西就几乎和真的一模一样了！这个网页让你直接在浏览器里看它们玩游戏。