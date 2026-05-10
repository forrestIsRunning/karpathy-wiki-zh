# NeuralTalk2

**GitHub:** https://github.com/karpathy/neuraltalk2
**Stars:** 5.6k | **Forks:** 1.3k | **Language:** Jupyter Notebook
**License:** MIT

## Description

Recurrent Neural Network captions your images. Much faster and better than the original NeuralTalk. Compared to the original, this implementation is **batched, uses Torch, runs on a GPU, and supports CNN finetuning**. All of these together result in quite a large increase in training speed for the Language Model (~100x).

This current code (and the pretrained model) gets ~0.9 CIDEr, which would place it around spot #8 on the [codalab leaderboard](https://codalab.org/).

**Update (September 22, 2016):** The Google Brain team released the [im2txt](https://github.com/tensorflow/models/tree/master/im2txt) model in TensorFlow. The core model is very similar to NeuralTalk2 but should work significantly better. This repo is left up for educational purposes and as a Torch implementation.

## Requirements

Written in Lua and requires Torch. Additional packages: `nn`, `nngraph`, `image`, `cjson`. For GPU: `cutorch`, `cunn`, `cudnn`. For training: `loadcaffe` (for VGGNet), `torch-hdf5`, `h5py`.

## Evaluation (Caption Your Images)

Download the [pretrained checkpoint](https://github.com/karpathy/neuraltalk2#pretrained-checkpoint-link) (600MB, includes finetuned VGGNet weights). Place images in a folder and run:

```
$ th eval.lua -model /path/to/model -image_folder /path/to/image/directory -num_images 10
```

Use `-num_images -1` to process all images. The eval script creates `vis/vis.json` which can be visualized with `python -m SimpleHTTPServer`.

**CPU only:** Download the CPU model checkpoint and use `-gpuid -1`.

**Beam Search:** Enabled by default. Use `-beam_size 1` for faster but less accurate results.

## Training on MS COCO

1. Run preprocessing notebook in `coco/` folder
2. Run `prepro.py` to create hdf5/json dataset
3. Download VGG-16 Caffe checkpoint
4. Run `th train.lua -input_h5 coco/cocotalk.h5 -input_json coco/cocotalk.json`

Use `-language_eval 1` to evaluate BLEU/METEOR/CIDEr during training.

## License

MIT

---

*Fetched from https://github.com/karpathy/neuraltalk2 on 2026-05-09*

## 三岁版

neuraltalk2 就像给照片配"看图说话"的 AI。你看一张照片，它能告诉你"这是一只小狗在草地上跑"。它先看懂图片里有什么，然后用学过的"话"组织成句子说出来。比第一版快了一百倍，就像从走路变成坐小汽车！