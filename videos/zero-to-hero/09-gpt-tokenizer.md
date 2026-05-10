# Let's build the GPT Tokenizer

**中文说明：** 这是 Karpathy 的 "Zero to Hero" 系列中的一集。该系列从零开始构建神经网络，最终到达 GPT。本集的具体内容和观看链接如下。

---

# Let's build the GPT Tokenizer

- **Source:** [YouTube](https://www.youtube.com/watch?v=zduSFxRajkE)
- **Author:** Andrej Karpathy
- **Video ID:** zduSFxRajkE
- **Date:** Feb 20, 2024
- **Views:** 1,090,066 views

## Description

The Tokenizer is a necessary and pervasive component of Large Language Models (LLMs), where it translates between strings and tokens (text chunks). Tokenizers are a completely separate stage of the LLM pipeline: they have their own training sets, training algorithms (Byte Pair Encoding), and after training implement two fundamental functions: encode() from strings to tokens, and decode() back from tokens to strings. In this lecture we build from scratch the Tokenizer used in the GPT series from OpenAI. In the process, we will see that a lot of weird behaviors and problems of LLMs actually trace back to tokenization. We'll go through a number of these issues, discuss why tokenization is at fault, and why someone out there ideally finds a way to delete this stage entirely.

Chapters:
00:00:00 intro: Tokenization, GPT-2 paper, tokenization-related issues
00:05:50 tokenization by example in a Web UI (tiktokenizer)
00:14:56 strings in Python, Unicode code points
00:18:15 Unicode byte encodings, ASCII, UTF-8, UTF-16, UTF-32
00:22:47 daydreaming: deleting tokenization
00:23:50 Byte Pair Encoding (BPE) algorithm walkthrough
00:27:02 starting the implementation
00:28:35 counting consecutive pairs, finding most common pair
00:30:36 merging the most common pair
00:34:58 training the tokenizer: adding the while loop, compression ratio
00:39:20 tokenizer/LLM diagram: it is a completely separate stage
00:42:47 decoding tokens to strings
00:48:21 encoding strings to tokens
00:57:36 regex patterns to force splits across categories
01:11:38 tiktoken library intro, differences between GPT-2/GPT-4 regex
01:14:59 GPT-2 encoder.py released by OpenAI walkthrough
01:18:26 special tokens, tiktoken handling of, GPT-2/GPT-4 differences
01:25:28 minbpe exercise time! write your own GPT-4 tokenizer
01:28:42 sentencepiece library intro, used to train Llama 2 vocabulary
01:43:27 how to set vocabulary set? revisiting gpt.py transformer
01:48:11 training new tokens, example of prompt compression
01:49:58 multimodal [image, video, audio] tokenization with vector quantization
01:51:41 revisiting and explaining the quirks of LLM tokenization
02:10:20 final recommendations
02:12:50 ??? :)

Exercises:
Advised flow: reference this document and try to implement the steps before I give away the partial solutions in the video. The full solutions if you're getting stuck are in the minbpe code https://github.com/karpathy/minbpe/bl...

Links:
Google colab for the video: https://colab.research.google.com/dri...
GitHub repo for the video: minBPE https://github.com/karpathy/minbpe
Playlist of the whole Zero to Hero series so far:    • The spelled-out intro to neural networks a...  
our Discord channel:   / discord  
my Twitter:   / karpathy  

Supplementary links:
tiktokenizer https://tiktokenizer.vercel.app
tiktoken from OpenAI: https://github.com/openai/tiktoken
sentencepiece from Google https://github.com/google/sentencepiece

