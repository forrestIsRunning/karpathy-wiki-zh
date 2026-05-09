# Deep Fragment Embeddings for Bidirectional Image Sentence Mapping

## Metadata
- **Title:** Deep Fragment Embeddings for Bidirectional Image Sentence Mapping
- **Authors:** Andrej Karpathy, Armand Joulin, Li Fei-Fei
- **Venue:** NIPS 2014
- **Year:** 2014
- **URL:** https://cs.stanford.edu/people/karpathy/nips2014.pdf

## Abstract
We introduce a model for bidirectional retrieval of images and sentences through a deep, multi-modal embedding of visual and natural language data. Unlike previous models that directly map images or sentences into a common embedding space, our model works on a finer level and embeds fragments of images (objects) and fragments of sentences (typed dependency tree relations) into a common space. We then introduce a structured max-margin objective that allows our model to explicitly associate these fragments across modalities.

Extensive experimental evaluation shows that reasoning on both the global level of images and sentences and the finer level of their respective fragments improves performance on image-sentence retrieval tasks. Additionally, our model provides interpretable predictions for the image-sentence retrieval task since the inferred inter-modal alignment of fragments is explicit.

## Method
- **Image fragments:** Object detections using RCNN (Region Convolutional Neural Network), using top 19 detected locations plus the entire image as fragments.
- **Sentence fragments:** Dependency tree relations (typed triplets from dependency parses).
- **Objective:** Structured max-margin objective combining:
  1. **Global Ranking Objective** - image-sentence pairs should be consistent with ground truth correspondences.
  2. **Fragment Alignment Objective** - explicitly learns the appearance of sentence fragments in the visual domain.

## Datasets
- Pascal1K, Flickr8K, Flickr30K
- Reported dramatic improvements over state-of-the-art methods on image-sentence retrieval tasks.

## Related Work Context
- Builds on ideas from Frome et al. (DeViSE), Socher et al. (DT-RNN), and Girshick et al. (RCNN).
- One of the early works on fine-grained multimodal alignment between visual and language data.

## 三岁版
这个研究教电脑玩"连连看"游戏：给电脑看一张照片和一句话，让它判断"这句话说的是这张图吗？"。但这次不是看整体，而是把照片里的小物件（比如"球"、"帽子"）和句子里的关键词（"球"、"帽子"）配对。就像小朋友玩配对卡片游戏，把画着苹果的卡片和写着"苹果"的卡片放在一起。