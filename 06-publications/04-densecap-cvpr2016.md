# DenseCap: Fully Convolutional Localization Networks for Dense Captioning

## Metadata
- **Title:** DenseCap: Fully Convolutional Localization Networks for Dense Captioning
- **Authors:** Justin Johnson (equal contribution), Andrej Karpathy (equal contribution), Li Fei-Fei
- **Venue:** CVPR 2016 (Oral)
- **Year:** 2016
- **URL:** https://cs.stanford.edu/people/karpathy/densecap/
- **Code:** https://github.com/jcjohnson/densecap

## Abstract
This is a CVPR 2016 (Oral) paper from Stanford Vision Lab. The task introduces "dense captioning," requiring systems to both localize and describe salient regions in images in natural language. The authors propose a Fully Convolutional Localization Network (FCLN) architecture that handles localization and description jointly. It processes an image with a single, efficient forward pass, requires no external region proposals, and supports end-to-end training in one optimization round. The architecture combines a Convolutional Network, a novel dense localization layer, and an RNN language model.

## Key Contributions
1. **Dense captioning** as a new task -- it generalizes object detection when the descriptions consist of a single word and Image Captioning when one region covers the whole image.
2. **FCLN architecture** -- single forward pass, no external region proposals needed.
3. In "backwards" mode, the model can search images for arbitrary text queries (region search) by computing the probability of generating the query given each detected region.

## Dataset & Evaluation
- Evaluated on the **Visual Genome dataset** (94,000 images, 4.1 million region-grounded captions).
- Demonstrated speed and accuracy improvements over baselines in both generation and retrieval settings.

## BibTeX
```
@inproceedings{densecap,
  title={DenseCap: Fully Convolutional Localization Networks for Dense Captioning},
  author={Johnson, Justin and Karpathy, Andrej and Fei-Fei, Li},
  booktitle={Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition},
  year={2016}
}
```

## 三岁版
这个研究教电脑更厉害地"看图说话"。之前的电脑只能给整张照片写一句话，这个研究教电脑给照片里的每一个"小东西"都写一句话——比如"红色的球"、"追球的小狗"、"绿色的草地"。就像小朋友看一本图画书，能指出每个角落分别画了什么。