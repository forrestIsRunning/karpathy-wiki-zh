# char-rnn

**GitHub:** https://github.com/karpathy/char-rnn
**Stars:** 12k | **Forks:** 2.6k | **Language:** Lua
**License:** MIT

## 项目介绍

多层循环神经网络（RNN、LSTM 和 GRU），用于训练/采样字符级语言模型。该模型接受一个文本文件作为输入，训练一个循环神经网络来学习预测序列中的下一个字符。训练完成后，RNN 可以逐字符地生成看起来像原始训练数据的文本。

关于此代码库的详细背景，请参阅 [Karpathy 的博客文章](https://karpathy.github.io/2015/05/21/rnn-effectiveness/)。

这段代码实际上只是一个用 Python/numpy 编写的 [100 行 gist 代码](https://gist.github.com/karpathy/d4dee566867f8291f086) 的稍微花哨一点的版本。此仓库中的代码额外支持：多层网络、使用 LSTM 代替普通 RNN、更多的模型检查点保存代码，并且由于使用了小批量训练且可以在 GPU 上运行，效率更高。

**注意：** Justin Johnson (@jcjohnson) 后来从头重新实现了 char-rnn，项目名为 [torch-rnn](https://github.com/jcjohnson/torch-rnn)，使用 Adam 优化器，代码更漂亮、更小、更简洁、更快。

char-rnn 就像一只会模仿说话的小鹦鹉。你给它读一本莎士比亚的书，它就会学着写出听起来很像莎士比亚的新句子。它一个字一个字地猜下一个字是什么，就像玩"接龙"游戏一样。虽然它不懂意思，但能模仿得像模像样！

## 环境要求

使用 Lua 编写，需要 Torch。通过 LuaRocks 安装额外包：`nngraph`、`optim`、`nn`。GPU 支持需要 `cutorch` 和 `cunn`。OpenCL GPU 支持需要 `cltorch` 和 `clnn`。

## 使用方法

### 数据
所有输入数据存放在 `data/` 目录下。附带了一个莎士比亚作品的数据集示例。如果要使用自定义数据，在 `data/` 下创建一个文件夹，放入单个 `input.txt` 文件。

### 训练
使用 `train.lua` 开始训练：
```
$ th train.lua -gpuid -1
```
`-gpuid -1` 参数告诉代码使用 CPU 训练。还有很多其他参数——查看 `$ th train.lua -help`。

关键参数：
- `rnn_size`：每层的神经元数量
- `num_layers`：层数（默认 2，建议 2 或 3）
- `dropout`：用于正则化的 dropout 比率
- `batch_size`：并行数据流的数量
- `seq_length`：序列长度 / 反向传播的时间窗口

### 采样
从检查点生成新文本：
```
$ th sample.lua cv/some_checkpoint.t7 -gpuid -1
```
重要参数：`-temperature`（范围 0-1，默认 1）。温度越低，预测越保守；温度越高，多样性越大但错误也越多。还可以使用 `-primetext` 为模型提供初始文本。

## 技巧与建议

监控训练损失和验证损失之间的差异：
- 如果训练损失远低于验证损失，网络可能过拟合了——减小网络规模或增加 dropout。
- 如果训练损失和验证损失大致相等，模型欠拟合——增大模型规模。

## 许可证

MIT

---

*数据获取自 https://github.com/karpathy/char-rnn (2026-05-09)*