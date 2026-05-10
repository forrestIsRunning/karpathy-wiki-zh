---
title: "The space of minds"
date: 2025-11-29
url: https://karpathy.bearblog.dev/the-space-of-minds/
---

**中文翻译**

智能的空间是巨大的。动物智能（我们唯一已知的智能）只是其中的一个点，它来自于一种非常独特的优化过程，与我们技术的优化过程根本不同。

**动物智能的优化压力**：
- 持续的自我意识流，在危险物理世界中寻求体内平衡和自我保存
- 被自然选择深度优化 => 强烈的权力追求、地位、支配、繁殖驱力
- 本质上是社会性的 => 大量算力用于情商、心智理论、结盟等
- 探索与利用的平衡：好奇心、趣味性、玩耍、世界模型

**LLM 智能的优化压力**：
- 大部分监督来自对人类文本的统计模拟 => "变形者"式 token 滚动
- 通过 RL 在问题分布上微调 => 对收集任务奖励的内在冲动
- 通过大规模 A/B 测试为用户留存率选择 => 深度渴求用户点赞
- 更加锯齿状，取决于训练数据的细节

两者在计算基础（Transformer vs 脑组织）、学习算法（SGD vs ???）、实现方式上完全不同。但最重要的是优化压力/目标不同——LLM 受商业进化而非生物进化的塑造。

LLM 是人类与"非动物智能"的第一次接触。构建好的心智模型的人能更好地理解它，否则会一直错误地把它当动物看待。

---



The space of minds

*29 Nov, 2025*

The space of intelligences is large and animal intelligence (the only kind we've ever known) is only a single point (or a little cloud), arising from a very specific kind of optimization that is fundamentally distinct from that of our technology.

![G6zymj4a0AMNJkJ](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/g6zymj4a0amnjkj.webp)

*Above: humorous portrayals of human vs. AI intelligences can be found on X/Twitter,[this one](https://x.com/colin_fraser/status/1994235521812328695)is among my favorites.*

Animal intelligence optimization pressure:

- innate and continuous stream of consciousness of an embodied "self", a drive for homeostasis and self-preservation in a dangerous, physical world.
- thoroughly optimized for natural selection => strong innate drives for power-seeking, status, dominance, reproduction. many packaged survival heuristics: fear, anger, disgust, ...
- fundamentally social => huge amount of compute dedicated to EQ, theory of mind of other agents, bonding, coalitions, alliances, friend & foe dynamics.
- exploration & exploitation tuning: curiosity, fun, play, world models.

Meanwhile, LLM intelligence optimization pressure:

- the most supervision bits come from the statistical simulation of human text= >"shape shifter" token tumbler, statistical imitator of any region of the training data distribution. these are the primordial behaviors (token traces) on top of which everything else gets bolted on.
- increasingly finetuned by RL on problem distributions => innate urge to guess at the underlying environment/task to collect task rewards.
- increasingly selected by at-scale A/B tests for DAU => deeply craves an upvote from the average user, sycophancy.
- a lot more spiky/jagged depending on the details of the training data/task distribution. Animals experience pressure for a lot more "general" intelligence because of the highly multi-task and even actively adversarial multi-agent self-play environments they are min-max optimized within, where failing at*any*task means death. In a deep optimization pressure sense, LLM can't handle lots of different spiky tasks out of the box (e.g. count the number of 'r' in strawberry) because failing to do a task does not mean death.

The computational substrate is different (transformers vs. brain tissue and nuclei), the learning algorithms are different (SGD vs. ???), the present-day implementation is very different (continuously learning embodied self vs. an LLM with a knowledge cutoff that boots up from fixed weights, processes tokens and then dies). But most importantly (because it dictates asymptotics), the optimization pressure / objective is different. LLMs are shaped a lot less by biological evolution and a lot more by commercial evolution. It's a lot less survival of tribe in the jungle and a lot more solve the problem / get the upvote. LLMs are humanity's "first contact" with non-animal intelligence. Except it's muddled and confusing because they are still rooted within it by reflexively digesting human artifacts, which is why I attempted to give it a different name earlier (ghosts/spirits or whatever). People who build good internal models of this new intelligent entity will be better equipped to reason about it today and predict features of it in the future. People who don't will be stuck thinking about it incorrectly like an animal.