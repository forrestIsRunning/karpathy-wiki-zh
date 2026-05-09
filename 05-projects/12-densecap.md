# DenseCap: Fully Convolutional Localization Networks for Dense Captioning

**Website:** https://cs.stanford.edu/people/karpathy/densecap/
**GitHub:** https://github.com/jcjohnson/densecap
**Authors:** Justin Johnson*, Andrej Karpathy*, Fei-Fei Li (* equal contribution)
**Conference:** CVPR 2016 (Oral)

## Abstract

We introduce the dense captioning task, which requires a computer vision system to both localize and describe salient regions in images in natural language. The dense captioning task generalizes object detection when the descriptions consist of a single word, and Image Captioning when one predicted region covers the full image.

To address the localization and description task jointly we propose a Fully Convolutional Localization Network (FCLN) architecture that processes an image with a single, efficient forward pass, requires no external region proposals, and can be trained end-to-end with a single round of optimization. The architecture is composed of a Convolutional Network, a novel dense localization layer, and a Recurrent Neural Network language model that generates the label sequences.

We evaluate our network on the [Visual Genome dataset](https://visualgenome.org/), which comprises 94,000 images and 4,100,000 region-grounded captions. We observe both speed and accuracy improvements over baselines based on current state of the art approaches in both generation and retrieval settings.

## Code and Resources

Available on [GitHub](https://github.com/jcjohnson/densecap):
- Training/test code (Torch/Lua)
- Pretrained model
- Live webcam demo
- Dense Captioning metric evaluation code

## Example Results

### Dense Captioning
Predictions from the model, cherry-picked for high-resolution, rich scenes. Browse the full results on the interactive predictions visualizer page (30MB) — visualizer code included on GitHub.

### Region Search
The DenseCap model can also be run "backwards" to search for text queries. For example, take descriptions such as "head of a giraffe" and look through images to find regions likely to generate that description. This does not merely caption images and look for string overlaps; it forwards the model and checks the probability of generating the query conditioned on every detected region of interest.

## BibTeX

```
@inproceedings{densecap,
  title={DenseCap: Fully Convolutional Localization Networks for Dense Captioning},
  author={Johnson, Justin and Karpathy, Andrej and Fei-Fei, Li},
  booktitle={Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition},
  year={2016}
}
```

## Acknowledgements

NVIDIA Corporation for GPU donation. Supported by ONR MURI grant, Intel research grant, and NSF ISS-1115313.

---

*Fetched from https://cs.stanford.edu/people/karpathy/densecap/ on 2026-05-09*

## 三岁版

DenseCap 是"看图说话升级版"。neuraltalk 只能给整张图写一句话，但 DenseCap 能一张图里找出好多好多东西，然后给每个东西都配一句话。比如一张有很多动物的图，它能说出"这里有只长颈鹿"、"那边有只斑马"、"树上还有一只小鸟"。就像一个很细心的导游！