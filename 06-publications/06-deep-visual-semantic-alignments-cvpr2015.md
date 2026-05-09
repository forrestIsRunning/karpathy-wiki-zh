# Deep Visual-Semantic Alignments for Generating Image Descriptions

## Metadata
- **Title:** Deep Visual-Semantic Alignments for Generating Image Descriptions
- **Authors:** Andrej Karpathy, Li Fei-Fei
- **Venue:** CVPR 2015
- **Year:** 2015
- **URL:** http://cs.stanford.edu/people/karpathy/deepimagesent/
- **Code (deprecated):** https://github.com/karpathy/neuraltalk
- **Code (successor):** https://github.com/karpathy/neuraltalk2

## Abstract
The paper presents a model that produces natural language descriptions for images and their sub-regions. It uses datasets of images and their sentence descriptions to learn about the inter-modal correspondences between language and visual data. The alignment model combines Convolutional Neural Networks over image regions with bidirectional RNNs over sentences, using a structured objective that aligns the two modalities through a multimodal embedding. A Multimodal Recurrent Neural Network architecture leverages inferred alignments to generate novel region descriptions.

## Method
Two key components:
1. **Alignment Model**: CNN over image regions + bidirectional RNN over sentences + a structured multimodal embedding objective.
2. **Multimodal Recurrent Neural Network**: Uses alignments to learn generation of novel image region descriptions.

## Results
- State of the art results in retrieval experiments on Flickr8K, Flickr30K and MSCOCO datasets.
- Generated descriptions significantly outperform retrieval baselines on both full images and on a new dataset of region-level annotations.

## Datasets Released
- Flickr8K (50MB), Flickr30K (200MB), COCO (750MB) with VGG CNN features
- JSON blobs for all three datasets (35MB)
- COCO region annotations (9,000 noun phrases across 200 COCO images)

## Interactive Demos
- Retrieval ranking demo (1,000 COCO test images)
- Caption generation demo

## 三岁版
这个研究教电脑"看图说话"——它看到一张照片，就能说出一句描述的话，比如"一个穿红衣服的女孩在荡秋千"。电脑不仅要认出照片里有啥，还要把它们串成一个通顺的句子。就像小朋友看了绘本之后，用自己的话把故事讲出来一样。