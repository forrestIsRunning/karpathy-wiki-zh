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