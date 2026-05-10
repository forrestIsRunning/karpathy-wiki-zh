---

**中文翻译**

这是斯坦福 CS231n 课程笔记网站（cs231n.github.io）的内容汇总，涵盖深度学习在计算机视觉中的应用。

**模块 0：准备**
- 软件环境设置
- Python / Numpy 教程（含 Jupyter 和 Colab）

**模块 1：神经网络**
- 图像分类：数据驱动方法、K 近邻、线性分类器
- 损失函数和优化：Softmax、SVM、SGD
- 反向传播和神经网络
- 神经网络训练技巧：激活函数、权重初始化、批量归一化、正则化

**模块 2：卷积神经网络**
- CNN 架构：卷积层、池化层
- 经典架构：AlexNet、VGG、GoogleNet、ResNet

**模块 3：视觉理解和生成**
- 目标检测和图像分割
- 可视化与理解
- 图像描述和 Transformer
- 自监督学习
- 生成模型：VAE、GAN、扩散模型

每个模块都有对应的课后笔记和作业。

---


# CS231n Course Notes (cs231n.github.io)

**Website:** https://cs231n.github.io/

These notes accompany the Stanford CS class CS231n: Deep Learning for Computer Vision. For questions/concerns/bug reports, submit a pull request to the git repo: https://github.com/cs231n/cs231n.github.io

---

## Spring 2026 Assignments

1. **Assignment #1:** Image Classification, kNN, Softmax, Fully-Connected Neural Network, Fully-Connected Nets
   - https://cs231n.github.io/assignments2026/assignment1/

2. **Assignment #2:** Batch Normalization, Dropout, Convolutional Nets, Network Visualization, Image Captioning with RNNs
   - https://cs231n.github.io/assignments2026/assignment2/

3. **Assignment #3:** Image Captioning with Transformers, Self-Supervised Learning, Diffusion Models, CLIP and DINO Models
   - Releasing May 14

---

## Module 0: Preparation

- **Software Setup** - https://cs231n.github.io/setup-instructions/
- **Python / Numpy Tutorial (with Jupyter and Colab)** - https://cs231n.github.io/python-numpy-tutorial/

---

## Module 1: Neural Networks

1. **Image Classification: Data-driven Approach, k-Nearest Neighbor, train/val/test splits**
   - https://cs231n.github.io/classification/
   - Keywords: L1/L2 distances, hyperparameter search, cross-validation

2. **Linear Classification: Support Vector Machine, Softmax**
   - https://cs231n.github.io/linear-classify/
   - Keywords: parametric approach, bias trick, hinge loss, cross-entropy loss, L2 regularization, web demo

3. **Optimization: Stochastic Gradient Descent**
   - https://cs231n.github.io/optimization-1/
   - Keywords: optimization landscapes, local search, learning rate, analytic/numerical gradient

4. **Backpropagation, Intuitions**
   - https://cs231n.github.io/optimization-2/
   - Keywords: chain rule interpretation, real-valued circuits, patterns in gradient flow

5. **Neural Networks Part 1: Setting up the Architecture**
   - https://cs231n.github.io/neural-networks-1/
   - Keywords: model of a biological neuron, activation functions, neural net architecture, representational power

6. **Neural Networks Part 2: Setting up the Data and the Loss**
   - https://cs231n.github.io/neural-networks-2/
   - Keywords: preprocessing, weight initialization, batch normalization, regularization (L2/dropout), loss functions

7. **Neural Networks Part 3: Learning and Evaluation**
   - https://cs231n.github.io/neural-networks-3/
   - Keywords: gradient checks, sanity checks, babysitting the learning process, momentum (+nesterov), second-order methods, Adagrad/RMSprop, hyperparameter optimization, model ensembles

8. **Putting it together: Minimal Neural Network Case Study**
   - https://cs231n.github.io/neural-networks-case-study/
   - Keywords: minimal 2D toy data example

---

## Module 2: Convolutional Neural Networks

1. **Convolutional Neural Networks: Architectures, Convolution / Pooling Layers**
   - https://cs231n.github.io/convolutional-networks/
   - Keywords: layers, spatial arrangement, layer patterns, layer sizing patterns, AlexNet/ZFNet/VGGNet case studies, computational considerations

2. **Understanding and Visualizing Convolutional Neural Networks**
   - https://cs231n.github.io/understanding-cnn/
   - Keywords: tSNE embeddings, deconvnets, data gradients, fooling ConvNets, human comparisons

3. **Transfer Learning and Fine-tuning Convolutional Neural Networks**
   - https://cs231n.github.io/transfer-learning/

---

## Student-Contributed Posts

- **Taking a Course Project to Publication** - https://cs231n.github.io/choose-project/
- **Recurrent Neural Networks** - https://cs231n.github.io/rnn/