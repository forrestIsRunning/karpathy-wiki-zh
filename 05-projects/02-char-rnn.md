# char-rnn

**GitHub:** https://github.com/karpathy/char-rnn
**Stars:** 12k | **Forks:** 2.6k | **Language:** Lua
**License:** MIT

## Description

Multi-layer Recurrent Neural Networks (RNN, LSTM, and GRU) for training/sampling from character-level language models. The model takes one text file as input and trains a Recurrent Neural Network that learns to predict the next character in a sequence. The RNN can then be used to generate text character by character that will look like the original training data.

The context of this code base is described in detail in [Karpathy's blog post](https://karpathy.github.io/2015/05/21/rnn-effectiveness/).

This code is really just a slightly more fancy version of a [100-line gist](https://gist.github.com/karpathy/d4dee566867f8291f086) written in Python/numpy. The code in this repo additionally: allows for multiple layers, uses an LSTM instead of a vanilla RNN, has more supporting code for model checkpointing, and is much more efficient since it uses mini-batches and can run on a GPU.

**Note:** Justin Johnson (@jcjohnson) later re-implemented char-rnn from scratch as [torch-rnn](https://github.com/jcjohnson/torch-rnn), with a much nicer/smaller/cleaner/faster Torch code base using Adam for optimization.

## Requirements

Written in Lua and requires Torch. Additional packages needed via LuaRocks: `nngraph`, `optim`, `nn`. GPU support requires `cutorch` and `cunn`. OpenCL GPU support via `cltorch` and `clnn`.

## Usage

### Data
All input data is stored inside the `data/` directory. An example dataset of Shakespeare's works is included. For custom data, create a single file `input.txt` in a folder in `data/`.

### Training
Start training using `train.lua`:
```
$ th train.lua -gpuid -1
```
The `-gpuid -1` flag tells the code to train using CPU. There are many other flags available — consult `$ th train.lua -help`.

Key parameters:
- `rnn_size`: number of neurons per layer
- `num_layers`: number of layers (default 2, recommend 2/3)
- `dropout`: dropout rate for regularization
- `batch_size`: number of parallel data streams
- `seq_length`: sequence length / backpropagation time window

### Sampling
Generate new text from a checkpoint:
```
$ th sample.lua cv/some_checkpoint.t7 -gpuid -1
```
Important parameter: `-temperature` (range 0-1, default 1). Lower temperature = more conservative predictions, higher temperature = more diversity but more mistakes. Can also prime the model with `-primetext`.

## Tips and Tricks

Monitor the difference between training loss and validation loss:
- If training loss is much lower than validation loss, the network may be overfitting — decrease network size or increase dropout.
- If training/validation loss are about equal, the model is underfitting — increase model size.

## License

MIT

---

*Fetched from https://github.com/karpathy/char-rnn on 2026-05-09*