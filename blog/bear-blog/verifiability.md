---
title: "Verifiability"
date: 2025-11-17
url: https://karpathy.bearblog.dev/verifiability/
---

**中文翻译**

Karpathy 认为 AI 最好的类比不是电或工业革命，而是一种**新的计算范式**。

如果用这个视角回看 1980 年代计算机对工作的影响，最关键的预测特征是**可指定性**——你的工作是否可以用机械的算法来描述？打字员、记账员等最容易被自动化。

现在 AI 让我们能够编写以前无法手写的新程序。我们通过指定目标（分类精度、奖励函数）并用梯度下降搜索程序空间来找到好用的神经网络。在这个新编程范式下，最关键的预测特征变成了**可验证性**。

如果一个任务/工作是**可验证的**，那么它就可以直接或通过强化学习进行优化，神经网络的训练效果会极其好。环境必须：
- 可重置（可以重新开始尝试）
- 高效（可以进行大量尝试）
- 有奖励机制（有自动过程奖励每次尝试）

一个任务越可验证，就越容易被新范式自动化。如果不可验证，就只能依赖神经网络的泛化能力或模仿学习。

这就是 LLM 进步呈现"锯齿形"前沿的原因：可验证的任务（数学、编程、拼图）进步神速，可能超过顶级专家的水平；而其他任务（创意、战略、需要常识的任务）则相对滞后。

**一句话总结**：
- 软件 1.0 容易自动化"你能指定"的内容
- 软件 2.0 容易自动化"你能验证"的内容

---



Verifiability

*17 Nov, 2025*

AI has been compared to various historical precedents: electricity, industrial revolution, etc., I think the strongest analogy is that of AI as a new computing paradigm because both are fundamentally about the automation of digital information processing.

If you were to forecast the impact of computing on the job market in ~1980s, the most predictive feature of a task/job you'd look at is**specifiability**, i.e. are you just mechanically transforming information according to rote, easy to specify algorithm (examples being typing, bookkeeping, human calculators, etc.)? Back then, this was the class of programs that the computing capability of that era allowed us to write (by hand, manually). I call hand-written programs "Software 1.0".

With AI now, we are able to write new programs that we could never hope to write by hand before. We do it by specifying objectives (e.g. classification accuracy, reward functions), and we search the program space via gradient descent to find neural networks that work well against that objective. This is my[Software 2.0 blog post](https://karpathy.medium.com/software-2-0-a64152b37c35)from a while ago. In this new programming paradigm then, the new most predictive feature to look at is**verifiability**. If a task/job is verifiable, then it is optimizable directly or via reinforcement learning, and a neural net can be trained to work extremely well. It's about to what extent an AI can "practice" something. The environment has to be:

- resettable (you can start a new attempt),
- efficient (a lot attempts can be made) and
- rewardable (there is some automated process to reward any specific attempt that was made).

The more a task/job is verifiable, the more amenable it is to automation in the new programming paradigm. If it is not verifiable, it has to fall out from neural net magic of generalization fingers crossed, or via weaker means like imitation. This is what's driving the "jagged" frontier of progress in LLMs. Tasks that are verifiable progress rapidly, including possibly beyond the ability of top experts (e.g. math, code, amount of time spent watching videos, anything that looks like puzzles with correct answers), while many others lag by comparison (creative, strategic, tasks that combine real-world knowledge, state, context and common sense).

- Software 1.0 easily automates what you can specify.
- Software 2.0 easily automates what you can verify.