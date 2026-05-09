---
title: "Verifiability"
date: 2025-11-17
url: https://karpathy.bearblog.dev/verifiability/
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