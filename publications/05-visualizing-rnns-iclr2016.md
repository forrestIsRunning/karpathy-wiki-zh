# Visualizing and Understanding Recurrent Networks

## Metadata
- **Title:** Visualizing and Understanding Recurrent Networks
- **Authors:** Andrej Karpathy, Justin Johnson, Li Fei-Fei
- **Venue:** ICLR 2016 Workshop
- **Year:** 2015 (submitted June 5, 2015; revised November 17, 2015)
- **arXiv:** http://arxiv.org/abs/1506.02078
- **Subjects:** Machine Learning (cs.LG); Computation and Language (cs.CL); Neural and Evolutionary Computing (cs.NE)

## Abstract
Recurrent Neural Networks (RNNs), and specifically a variant with Long Short-Term Memory (LSTM), are enjoying renewed interest as a result of successful applications in a wide range of machine learning problems that involve sequential data. However, while LSTMs provide exceptional results in practice, the source of their performance and their limitations remain rather poorly understood. Using character-level language models as an interpretable testbed, we aim to bridge this gap by providing an analysis of their representations, predictions and error types.

Key findings:
- The experiments reveal the existence of interpretable cells that keep track of long-range dependencies such as line lengths, quotes and brackets.
- A comparative analysis with finite horizon n-gram models traces the source of the LSTM improvements to long-range structural dependencies.
- The paper provides analysis of the remaining errors and suggests areas for further study.

## Notes
- One of the first papers to provide detailed visualization and analysis of LSTM internals.
- Used character-level language models as a testbed for interpretability.
- Revealed that LSTM cells learn interpretable patterns (line length tracking, quote/bracket matching).

## DOI
https://doi.org/10.48550/arXiv.1506.02078

## 三岁版
这个研究"打开"了电脑的"大脑"，看看它到底是怎么思考的。他们发现电脑里有一些"小开关"专门负责记住很长的句子——比如能记住这句话前面有没有出现过"（"，后面是不是该出现"）"了。就像看看小朋友脑子里是怎么记住妈妈说的长长的话的。