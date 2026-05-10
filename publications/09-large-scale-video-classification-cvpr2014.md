# Large-Scale Video Classification with Convolutional Neural Networks

## Metadata
- **Title:** Large-Scale Video Classification with Convolutional Neural Networks
- **Authors:** Andrej Karpathy, George Toderici, Sanketh Shetty, Thomas Leung, Rahul Sukthankar, Li Fei-Fei
- **Venue:** CVPR 2014
- **Year:** 2014
- **URL:** https://cs.stanford.edu/people/karpathy/deepvideo/
- **Dataset:** https://github.com/gtoderici/sports-1m-dataset

## Abstract
Convolutional Neural Networks (CNNs) have been established as a powerful class of models for image recognition problems. Encouraged by these results, we provide an extensive empirical evaluation of CNNs on large-scale video classification using a new dataset of 1 million YouTube videos belonging to 487 classes. We study multiple approaches for extending the connectivity of a CNN in time domain to take advantage of local spatio-temporal information and suggest a multiresolution, foveated architecture as a promising way of speeding up the training.

Our best spatio-temporal networks display significant performance improvements compared to strong feature-based baselines (55.3% to 63.9%), but only a surprisingly modest improvement compared to single-frame models (59.3% to 60.9%). We further study the generalization performance of our best model by retraining the top layers on the UCF-101 Action Recognition dataset and observe significant performance improvements compared to the UCF-101 baseline model (63.3% up from 43.9%).

## Sports-1M Dataset
- 1,133,158 video URLs annotated automatically with 487 Sports labels using the YouTube Topics API.
- Licensed under Creative Commons 3.0.
- Code and dataset available on GitHub.

## Key Findings
- CNN-based video classification with spatio-temporal fusion.
- Surprisingly modest improvement over single-frame models (only +1.6%), suggesting frame-level appearance already captures significant signal.
- Multi-resolution foveated architecture for efficient training.
- Good transfer learning performance on UCF-101.

## BibTeX
```
@inproceedings{KarpathyCVPR14,
  title     = {Large-scale Video Classification with Convolutional Neural Networks},
  author    = {Andrej Karpathy and George Toderici and Sanketh Shetty and Thomas Leung and Rahul Sukthankar and Li Fei-Fei},
  year      = {2014},
  booktitle = {CVPR}
}
```

## 三岁版
这个研究教电脑"看视频认东西"。他们给电脑看了一百万个YouTube视频（全是运动类的），电脑要认出视频里是"打篮球"还是"游泳"。结果发现，电脑光看视频里的一帧画面（一张快照）就已经很厉害了，多看几帧帮助不大。就像让小朋友光看一张照片就能猜到是在做什么运动。