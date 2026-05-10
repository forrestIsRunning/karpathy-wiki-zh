# Deep Dive into LLMs like ChatGPT

- **Source:** [YouTube](https://www.youtube.com/watch?v=7xTGNNLPyMI)
- **Author:** Andrej Karpathy
- **Subscribers:** 1.4M subscribers
- **Date:** Feb 5, 2025
- **Views:** 6,315,048 views
- **Video ID:** 7xTGNNLPyMI

## Description

This is a general audience deep dive into the Large Language Model (LLM) AI technology that powers ChatGPT and related products. It is covers the full training stack of how the models are developed, along with mental models of how to think about their "psychology", and how to get the best use them in practical applications. I have one "Intro to LLMs" video already from ~year ago, but that is just a re-recording of a random talk, so I wanted to loop around and do a lot more comprehensive version.

Instructor
Andrej was a founding member at OpenAI (2015) and then Sr. Director of AI at Tesla (2017-2022), and is now a founder at Eureka Labs, which is building an AI-native school. His goal in this video is to raise knowledge and understanding of the state of the art in AI, and empower people to effectively use the latest and greatest in their work.
Find more at https://karpathy.ai/ and https://x.com/karpathy

Chapters
00:00:00 introduction
00:01:00 pretraining data (internet)
00:07:47 tokenization
00:14:27 neural network I/O
00:20:11 neural network internals
00:26:01 inference
00:31:09 GPT-2: training and inference
00:42:52 Llama 3.1 base model inference
00:59:23 pretraining to post-training
01:01:06 post-training data (conversations)
01:20:32 hallucinations, tool use, knowledge/working memory
01:41:46 knowledge of self
01:46:56 models need tokens to think
02:01:11 tokenization revisited: models struggle with spelling
02:04:53 jagged intelligence
02:07:28 supervised finetuning to reinforcement learning
02:14:42 reinforcement learning
02:27:47 DeepSeek-R1
02:42:07 AlphaGo
02:48:26 reinforcement learning from human feedback (RLHF)
03:09:39 preview of things to come
03:15:15 keeping track of LLMs
03:18:34 where to find LLMs
03:21:46 grand summary

Links
ChatGPT https://chatgpt.com/
FineWeb (pretraining dataset): https://huggingface.co/spaces/Hugging...
Tiktokenizer: https://tiktokenizer.vercel.app/
Transformer Neural Net 3D visualizer: https://bbycroft.net/llm
llm.c Let's Reproduce GPT-2 https://github.com/karpathy/llm.c/dis...
Llama 3 paper from Meta: https://arxiv.org/abs/2407.21783
Hyperbolic, for inference of base model: https://app.hyperbolic.xyz/
InstructGPT paper on SFT: https://arxiv.org/abs/2203.02155
HuggingFace inference playground: https://huggingface.co/spaces/hugging...
DeepSeek-R1 paper: https://arxiv.org/abs/2501.12948
TogetherAI Playground for open model inference: https://api.together.xyz/playground
AlphaGo paper (PDF): https://discovery.ucl.ac.uk/id/eprint...
AlphaGo Move 37 video:    • Video  
LM Arena for model rankings: https://lmarena.ai/
AI News Newsletter: https://buttondown.com/ainews
LMStudio for local inference https://lmstudio.ai/

The visualization UI I was using in the video: https://excalidraw.com/
The specific file of Excalidraw we built up: https://drive.google.com/file/d/1EZh5...
Discord channel for Eureka Labs and this video:   / discord  

Educational Use Licensing
This video is freely available for educational and internal training purposes. Educators, students, schools, universities, nonprofit institutions, businesses, and individual learners may use this content freely for lessons, courses, internal training, and learning activities, provided they do not engage in commercial resale, redistribution, external commercial use, or modify content to misrepresent its intent.

## 三岁版

这个视频是安德烈讲的一个很长很详细的课，告诉我们像 ChatGPT 这样的"聪明电脑"是怎么做出来的。他先讲电脑是怎么从网上学东西的，就像小朋友看书认字一样；然后讲电脑里面有一个很大的"数学大脑"，里面有很多数字在算来算去。他还告诉我们，这些电脑虽然很聪明，但也会"做梦"（说一些不真实的话），就像小朋友会编故事一样。最后他教我们怎么更好地使用这些工具，就像教小朋友怎么正确使用一个新玩具。

