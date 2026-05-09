# Connecting Images and Natural Language

## Metadata
- **Title:** Connecting Images and Natural Language
- **Author:** Andrej Karpathy
- **Degree:** Doctor of Philosophy (Computer Science)
- **Institution:** Stanford University
- **Date:** August 2016
- **Adviser:** Fei-Fei Li
- **Reading Committee:** Fei-Fei Li, Percy Liang, Christopher Manning
- **URL:** https://cs.stanford.edu/people/karpathy/main.pdf
- **Online:** http://purl.stanford.edu/wf528qt3314

## Abstract
A long-standing goal in the field of artificial intelligence is to develop agents that can perceive and understand the rich visual world around us and who can communicate with us about it in natural language.

Significant strides have been made towards this goal over the last few years due to simultaneous advances in computing infrastructure, data gathering and algorithms. The progress has been especially rapid in visual recognition, where computers can now classify images into categories with a performance that rivals that of humans, or even surpasses it in some cases such as classifying breeds of dogs. However, despite much encouraging progress, most of the advances in visual recognition still take place in the context of assigning one or a few discrete labels to an image (e.g. person, boat, keyboard, etc.).

In this dissertation we develop models and techniques that allow us to connect the domain of visual data and the domain of natural language utterances, enabling translation between elements of the two domains. In particular:

1. First we introduce a model that embeds both images and sentences into a common multi-modal embedding space. This space then allows us to identify images that depict an arbitrary sentence description and conversely, we can identify sentences that describe any image.
2. Second, we develop an image captioning model that takes an image and directly generates a sentence description without being constrained to a finite collection of human-written sentences to choose from.
3. Lastly, we describe a model that can take an image and both localize and describe all of its salient parts. We demonstrate that this model can also be used backwards to take any arbitrary description (e.g. "white tennis shoes") and efficiently localize the described concept in a large collection of images.

From the modeling perspective, instead of designing and staging explicit algorithms to process images and sentences in complex processing pipelines, our contribution lies in the design of hybrid convolutional and recurrent neural network architectures that connect visual data and natural language utterances with a single network. This approach enjoys many of the benefits of neural networks including the use of simple, homogeneous computations that are easy to parallelize on hardware, and strong performance due to end-to-end training.

## Dissertation Outline
1. Introduction
2. Deep Learning Background (Supervised Learning, Optimization, Backpropagation, Neural Networks)
3. Deep Visual-Semantic Alignments (CVPR 2015)
4. Deep Fragment Embeddings (NIPS 2014)
5. DenseCap: Dense Captioning (CVPR 2016)
6. Conclusions

## Acknowledgments
- Adviser: Fei-Fei Li
- Thanks to Chris Manning, Percy Liang, Vladlen Koltun, Andrew Ng, Daphne Koller, Sebastian Thrun
- Collaborators: Justin Johnson, Stephen Miller, Adam Coates, Armand Joulin, Olga Russakovsky, Jon Krause, Richard Socher
- Internships at Google and DeepMind
- Funding: ONR MURI, Intel, Yahoo! Labs, NVIDIA

## 三岁版
这是Andrej Karpathy的博士毕业论文，他教电脑学会"看图说话"。电脑看到一张照片，不光能认出里面有"人"、"狗"、"船"，还能说出"一个小朋友在公园里遛狗"。就像教一个三岁小孩看到图画书时，能讲出画里的故事一样。