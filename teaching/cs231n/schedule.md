---

**中文翻译**

CS231n 2026 春季课程表（前 10 周）。每周二和周四 12:00-1:20 PM 上课。

课程涵盖：
- 深度学习基础（图像分类、反向传播、神经网络）
- CNN 架构（AlexNet、VGG、ResNet）
- RNN 和 Transformer
- 目标检测和图像分割
- 视频理解
- 大规模分布式训练
- 自监督学习
- 生成模型（VAE、GAN、扩散模型）
- 3D 视觉

讨论课每周五 12:30-1:20 PM。第 6 周期中考试。

---


# CS231n Spring 2026 Schedule

**Lectures:** Tuesdays and Thursdays 12:00-1:20 PM Pacific Time at NVIDIA Auditorium.
**Discussion Sections:** Fridays 12:30-1:20 PM Pacific Time at NVIDIA Auditorium.

Color coding: Blue = lecture category titles, Yellow = discussion sections/poster session, Red = midterm exam.

---

## Course Schedule Table

| Date | Description | Course Materials | Events | Deadlines |
|------|-------------|-----------------|--------|-----------|
| **Mar 31** | **Lecture 1: Introduction** - Computer vision overview, Course overview, Course logistics [slides 1](https://cs231n.stanford.edu/slides/2026/lecture_1_part_1.pdf) [slides 2](https://cs231n.stanford.edu/slides/2026/lecture_1_part_2.pdf) | | | |
| | **Deep Learning Basics** | | | |
| **Apr 02** | **Lecture 2: Image Classification with Linear Classifiers** - Data-driven approach, K-nearest neighbor, Linear Classifiers, Algebraic/Visual/Geometric viewpoints, Softmax loss [slides](https://cs231n.stanford.edu/slides/2026/lecture_2.pdf) | [Image Classification](https://cs231n.github.io/classification/), [Linear Classification](https://cs231n.github.io/linear-classify/) | Assignment 1 **out** | |
| **Apr 03** | Python / Numpy Review Session [Colab](https://colab.research.google.com/github/cs231n/cs231n.github.io/blob/master/python-colab.ipynb) [Tutorial](https://cs231n.github.io/python-numpy-tutorial/) | 12:30-1:20pm PT | | |
| **Apr 07** | **Lecture 3: Regularization and Optimization** - Regularization, SGD, Momentum, AdaGrad, Adam, Learning rate schedules [slides](https://cs231n.stanford.edu/slides/2026/lecture_3.pdf) | [Optimization](https://cs231n.github.io/optimization-1/) | | |
| **Apr 09** | **Lecture 4: Neural Networks and Backpropagation** - Multi-layer Perceptron, Backpropagation [slides](https://cs231n.stanford.edu/slides/2026/lecture_4.pdf) | [Backprop](http://cs231n.github.io/optimization-2/), [Linear backprop example](handouts/linear-backprop.pdf). Suggested: [Why Momentum Works](https://distill.pub/2017/momentum/), [Derivatives notes](handouts/derivatives.pdf), [Efficient backprop](https://cs231n.stanford.edu/papers/lecun-98b.pdf) | | |
| **Apr 10** | Backprop Review Session [Colab](https://colab.research.google.com/github/cs231n/cs231n.github.io/blob/master/backprop.ipynb) [slides](https://cs231n.stanford.edu/slides/2026/section_2_backprop.pdf) | 12:30-1:20pm PT | | |
| | **Perceiving and Understanding the Visual World** | | | |
| **Apr 14** | **Lecture 5: Image Classification with CNNs** - History, Higher-level representations/image features, Convolution and pooling [slides](https://cs231n.stanford.edu/slides/2026/lecture_5.pdf) | [Convolutional Networks](http://cs231n.github.io/convolutional-networks) | | |
| **Apr 16** | **Lecture 6: CNN Architectures** - Batch Normalization, Transfer learning, AlexNet/VGG/ResNet [slides](https://cs231n.stanford.edu/slides/2026/lecture_6.pdf) | [AlexNet](https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf), [VGGNet](https://arxiv.org/abs/1409.1556), [GoogLeNet](https://arxiv.org/abs/1409.4842), [ResNet](https://arxiv.org/abs/1512.03385) | Project Proposal **out** | Assignment 1 **due** |
| **Apr 17** | Final Project Overview and Guidelines [slides](https://cs231n.stanford.edu/slides/2026/section_3_project.pdf) | 12:30-1:20pm PT | | |
| **Apr 21** | **Lecture 7: Recurrent Neural Networks** - RNN/LSTM/GRU, Language modeling, Image captioning, Seq2seq [slides](https://cs231n.stanford.edu/slides/2026/lecture_7.pdf) | Suggested: [DL book RNN chapter](http://www.deeplearningbook.org/contents/rnn.html), [Understanding LSTM Networks](https://colah.github.io/posts/2015-08-Understanding-LSTMs/) | | |
| **Apr 23** | **Lecture 8: Attention and Transformers** - Self-Attention, Transformers [slides](https://cs231n.stanford.edu/slides/2026/lecture_8.pdf) | Suggested: [Attention is All You Need](https://arxiv.org/abs/1706.03762), [Attention? Attention blog](https://lilianweng.github.io/posts/2018-06-24-attention/), [Illustrated Transformer](http://jalammar.github.io/illustrated-transformer/), [ViT Paper](https://arxiv.org/abs/2010.11929) | Assignment 2 **out** | Project Proposal **due** |
| **Apr 24** | PyTorch Review Session [Colab](https://colab.research.google.com/github/cs231n/cs231n.github.io/blob/master/pytorch.ipynb) | 12:30-1:20pm PT | | |
| **Apr 28** | **Lecture 9: Object Detection, Image Segmentation, Visualizing and Understanding** - Single/two-stage detectors, Semantic/Instance/Panoptic segmentation, Feature visualization/inversion, Adversarial examples, DeepDream/Style transfer [slides](https://cs231n.stanford.edu/slides/2026/lecture_9.pdf) | [FCN](https://arxiv.org/abs/1411.4038), [R-CNN](https://arxiv.org/abs/1311.2524), [Fast R-CNN](https://arxiv.org/abs/1504.08083), [Faster R-CNN](https://arxiv.org/abs/1506.01497), [YOLO](https://arxiv.org/abs/1506.02640), [DETR](https://arxiv.org/abs/2005.12872) | | |
| **Apr 30** | **Lecture 10: Video Understanding** - Video classification, 3D CNNs, Two-stream networks, Multimodal video understanding [slides](https://cs231n.stanford.edu/slides/2026/lecture_10.pdf) | | | |
| **May 01** | RNNs & Transformers discussion [slides](https://cs231n.stanford.edu/slides/2026/section_5.pdf) | 12:30-1:20pm PT | | |
| **May 05** | **Lecture 11: Large Scale Distributed Training** - Utilization, Parallelism, Activation Checkpointing [slides](https://cs231n.stanford.edu/slides/2026/lecture_11.pdf) | | | |
| | **Generative and Interactive Visual Intelligence** | | | |
| **May 07** | **Lecture 12: Self-supervised Learning** - Pretext tasks, Contrastive learning, Multisensory supervision [slides](https://cs231n.stanford.edu/slides/2026/lecture_12.pdf) | Suggested: [Lilian Weng SSL Blog](https://lilianweng.github.io/lil-log/2019/11/10/self-supervised-learning.html), [DINO](https://arxiv.org/abs/2104.14294) | | |
| **May 08** | Midterm Review Session | 12:30-1:20pm PT | | Assignment 2 **due** |
| **May 12** | **In-Class Midterm** | 12:00-1:20pm PT | | |
| **May 14** | **Lecture 13: Generative Models 1** - Variational Autoencoders, GANs, Autoregressive Models | Suggested: [ELBO Blog](https://yunfanj.com/blog/2021/01/11/ELBO.html) | Assignment 3 **out** | |
| **May 15** | | | | Milestone 1 Check-In **due** |
| **May 19** | **Lecture 14: Generative Models 2** - Diffusion models | | | |
| **May 21** | **Lecture 15: 3D Vision** - 3D shape representations, Shape reconstruction, Neural implicit representations | | | |
| **May 22** | | | | Milestone 2 Check-In **due** |
| **May 26** | **Lecture 16: Vision and Language** | | | |
| **May 28** | **Lecture 17: Robot Learning** - Deep Reinforcement Learning, Model Learning, Robotic Manipulation | | | Assignment 3 **due** |
| **May 29** | | | | Milestone 3 Check-In **due** |
| **Jun 02** | **Lecture 18: Human-Centered AI** | | | |
| **Jun 05** | | | | Final Report **due** |
| **Jun 10** | **Final Project Poster Session** | 12:15-3:15 PM PT | | |

---

## Lecture Slides

All lecture slides are available at: https://cs231n.stanford.edu/slides/2026/