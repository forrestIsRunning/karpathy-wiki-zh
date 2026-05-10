---
title: "2025 LLM Year in Review"
date: 2025-12-19
url: https://karpathy.bearblog.dev/year-in-review-2025/
---

**中文翻译**

2025 年是 LLM 进步显著的一年。Karpathy 列出了 6 个概念层面改变格局的范式转变：

**1. 可验证奖励的强化学习 (RLVR)**。2025 年新增了 RLVR 作为 LLM 训练的主要阶段。通过在可自动验证的任务（数学、编程）上训练，LLM 自发形成了"推理"能力——分解问题、来回验证等策略。大部分能力进步来自这个新阶段的算力投入。

**2. 幽灵 vs 动物 / 锯齿智能**。2025 年行业开始真正内化 LLM"形状"——我们不是在"进化/培养动物"，而是在"召唤幽灵"。LLM 在不同领域表现差异巨大，同时是天才和傻瓜。

**3. Cursor / 新 LLM 应用层**。Cursor 展示了 LLM App 的新范式：做"上下文工程"、编排多次 LLM 调用、提供 GUI 界面、提供"自主性滑条"。

**4. Claude Code / 住在你电脑上的 AI**。Claude Code 是 LLM Agent 的第一个令人信服的展示——在开发者本地运行，有私密环境、数据和上下文。

**5. Vibe Coding**。2025 年 AI 跨越了门槛——可以通过英语描述构建各种程序。Karpathy 发明了这个词。编程不再是专业人员的专利。

**6. Nano Banana / LLM GUI**。Gemini Nano Banana 展示了 LLM GUI 的可能性——不只是生成图像，而是文本生成、图像生成和世界知识的联合能力。LLM 应该用图像、信息图、幻灯片等人类偏好的格式与我们交流。

**TLDR**：2025 年是激动人心的一年。LLM 正成为一种新型智能，比预期聪明得多也愚蠢得多。行业连其 10% 的潜力都还没实现。

---



2025 LLM Year in Review

*19 Dec, 2025*

![unnamed](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/unnamed.webp)

2025 has been a strong and eventful year of progress in LLMs. The following is a list of personally notable and mildly surprising "paradigm changes" - things that altered the landscape and stood out to me conceptually.

### 1. Reinforcement Learning from Verifiable Rewards (RLVR)

At the start of 2025, the LLM production stack in all labs looked something like this:

1. Pretraining (GPT-2/3 of ~2020)
1. Supervised Finetuning (InstructGPT ~2022) and
1. Reinforcement Learning from Human Feedback (RLHF ~2022)

This was the stable and proven recipe for training a production-grade LLM for a while. In 2025, Reinforcement Learning from Verifiable Rewards (RLVR) emerged as the de facto new major stage to add to this mix. By training LLMs against automatically verifiable rewards across a number of environments (e.g. think math/code puzzles), the LLMs spontaneously develop strategies that look like "reasoning" to humans - they learn to break down problem solving into intermediate calculations and they learn a number of problem solving strategies for going back and forth to figure things out (see DeepSeek R1 paper for examples). These strategies would have been very difficult to achieve in the previous paradigms because it's not clear what the optimal reasoning traces and recoveries look like for the LLM - it has to find what works for it, via the optimization against rewards.

Unlike the SFT and RLHF stage, which are both relatively thin/short stages (minor finetunes computationally), RLVR involves training against objective (non-gameable) reward functions which allows for a lot longer optimization. Running RLVR turned out to offer high capability/$, which gobbled up the compute that was originally intended for pretraining. Therefore, most of the capability progress of 2025 was defined by the LLM labs chewing through the overhang of this new stage and overall we saw ~similar sized LLMs but a lot longer RL runs. Also unique to this new stage, we got a whole new knob (and and associated scaling law) to control capability as a function of test time compute by generating longer reasoning traces and increasing "thinking time". OpenAI o1 (late 2024) was the very first demonstration of an RLVR model, but the o3 release (early 2025) was the obvious point of inflection where you could intuitively feel the difference.

### 2. Ghosts vs. Animals / Jagged Intelligence

2025 is where I (and I think the rest of the industry also) first started to internalize the "shape" of LLM intelligence in a more intuitive sense. We're not "evolving/growing animals", we are "summoning ghosts". Everything about the LLM stack is different (neural architecture, training data, training algorithms, and especially optimization pressure) so it should be no surprise that we are getting very different entities in the intelligence space, which are inappropriate to think about through an animal lens. Supervision bits-wise, human neural nets are optimized for survival of a tribe in the jungle but LLM neural nets are optimized for imitating humanity's text, collecting rewards in math puzzles, and getting that upvote from a human on the LM Arena. As verifiable domains allow for RLVR, LLMs "spike" in capability in the vicinity of these domains and overall display amusingly jagged performance characteristics - they are at the same time a genius polymath and a confused and cognitively challenged grade schooler, seconds away from getting tricked by a jailbreak to exfiltrate your data.

![G6zymj4a0AMNJkJ](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/g6zymj4a0amnjkj.webp)

(human intelligence: blue, AI intelligence: red. I like this version of the meme (I'm sorry I lost the reference to its original post on X) for pointing out that human intelligence is also jagged in its own different way.)

Related to all this is my general apathy and loss of trust in benchmarks in 2025. The core issue is that benchmarks are almost by construction verifiable environments and are therefore immediately susceptible to RLVR and weaker forms of it via synthetic data generation. In the typical benchmaxxing process, teams in LLM labs inevitably construct environments adjacent to little pockets of the embedding space occupied by benchmarks and grow jaggies to cover them. Training on the test set is a new art form.

What does it look like to crush all the benchmarks but still not get AGI?

I have written a lot more on the topic of this section here:

- [Animals vs. Ghosts](https://karpathy.bearblog.dev/animals-vs-ghosts/)
- [Verifiability](https://karpathy.bearblog.dev/verifiability/)
- [The Space of Minds](https://karpathy.bearblog.dev/the-space-of-minds)

### 3. Cursor / new layer of LLM apps

What I find most notable about Cursor (other than its meteoric rise this year) is that it convincingly revealed a new layer of an "LLM app" - people started to talk about "Cursor for X". As I highlighted in my Y Combinator talk this year ([transcript](https://www.donnamagi.com/articles/karpathy-yc-talk)and[video](https://www.youtube.com/watch?v=LCEmiRjPEtQ)), LLM apps like Cursor bundle and orchestrate LLM calls for specific verticals:

1. They do the "context engineering"
1. They orchestrate multiple LLM calls under the hood strung into increasingly more complex DAGs, carefully balancing performance and cost tradeoffs.
1. They provide an application-specific GUI for the human in the loop
1. They offer an "autonomy slider"

A lot of chatter has been spent in 2025 on how "thick" this new app layer is. Will the LLM labs capture all applications or are there green pastures for LLM apps? Personally I suspect that LLM labs will trend to graduate the generally capable college student, but LLM apps will organize, finetune and actually animate teams of them into deployed professionals in specific verticals by supplying private data, sensors and actuators and feedback loops.

### 4. Claude Code / AI that lives on your computer

Claude Code (CC) emerged as the first convincing demonstration of what an LLM Agent looks like - something that in a loopy way strings together tool use and reasoning for extended problem solving. In addition, CC is notable to me in that it runs on your computer and with your private environment, data and context. I think OpenAI got this wrong because they focused their early codex / agent efforts on cloud deployments in containers orchestrated from ChatGPT instead of simply`localhost`. And while agent swarms running in the cloud feels like the "AGI endgame", we live in an intermediate and slow enough takeoff world of jagged capabilities that it makes more sense to run the agents directly on the developer's computer. Note that the primary distinction that matters is not about where the "AI ops" happen to run (in the cloud, locally or whatever), but about everything else - the already-existing and booted up computer, its installation, context, data, secrets, configuration, and the low-latency interaction. Anthropic got this order of precedence correct and packaged CC into a delightful, minimal CLI form factor that changed what AI looks like - it's not just a website you go to like Google, it's a little spirit/ghost that "lives" on your computer. This is a new, distinct paradigm of interaction with an AI.

### 5. Vibe coding

2025 is the year that AI crossed a capability threshold necessary to build all kinds of impressive programs simply via English, forgetting that the code even exists. Amusingly, I coined the term "vibe coding" in[this shower of thoughts tweet](https://x.com/karpathy/status/1886192184808149383)totally oblivious to how far it would go :). With vibe coding, programming is not strictly reserved for highly trained professionals, it is something anyone can do. In this capacity, it is yet another example of what I wrote about in[Power to the people: How LLMs flip the script on technology diffusion](https://karpathy.bearblog.dev/power-to-the-people/), on how (in sharp contrast to all other technology so far) regular people benefit a lot more from LLMs compared to professionals, corporations and governments. But not only does vibe coding empower regular people to approach programming, it empowers trained professionals to write a lot more (vibe coded) software that would otherwise never be written. In nanochat, I vibe coded my own custom highly efficient BPE tokenizer in Rust instead of having to adopt existing libraries or learn Rust at that level. I vibe coded many projects this year as quick app demos of something I wanted to exist (e.g. see[menugen](https://karpathy.bearblog.dev/vibe-coding-menugen),[llm-council](https://github.com/karpathy/llm-council),[reader3](https://github.com/karpathy/reader3),[HN time capsule](https://github.com/karpathy/hn-time-capsule)). And I've vibe coded entire ephemeral apps just to find a single bug because why not - code is suddenly free, ephemeral, malleable, discardable after single use. Vibe coding will terraform software and alter job descriptions.

### 6. Nano banana / LLM GUI

Google Gemini Nano banana is one of the most incredible, paradigm-shifting models of 2025. In my world view, LLMs are the next major computing paradigm similar to computers of the 1970s, 80s, etc. Therefore, we are going to see similar kinds of innovations for fundamentally similar kinds of reasons. We're going to see equivalents of personal computing, of microcontrollers (cognitive core), or internet (of agents), etc etc. In particular, in terms of the UIUX, "chatting" with LLMs is a bit like issuing commands to a computer console in the 1980s. Text is the raw/favored data representation for computers (and LLMs), but it is not the favored format for people, especially at the input. People actually dislike reading text - it is slow and effortful. Instead, people love to consume information visually and spatially and this is why the GUI has been invented in traditional computing. In the same way, LLMs should speak to us in our favored format - in images, infographics, slides, whiteboards, animations/videos, web apps, etc. The early and present version of this of course are things like emoji and Markdown, which are ways to "dress up" and lay out text visually for easier consumption with titles, bold, italics, lists, tables, etc. But who is actually going to build the LLM GUI? In this world view, nano banana is a first early hint of what that might look like. And importantly, one notable aspect of it is that it's not just about the image generation itself, it's about the joint capability coming from text generation, image generation and world knowledge, all tangled up in the model weights.

---

**TLDR**. 2025 was an exciting and mildly surprising year of LLMs. LLMs are emerging as a new kind of intelligence, simultaneously a lot smarter than I expected and a lot dumber than I expected. In any case they are extremely useful and I don't think the industry has realized anywhere near 10% of their potential even at present capability. Meanwhile, there are so many ideas to try and conceptually the field feels wide open. And as I mentioned on my[Dwarkesh pod](https://www.dwarkesh.com/p/andrej-karpathy)earlier this year, I simultaneously (and on the surface paradoxically) believe that we will both see rapid and continued progress*and*that yet there is a lot of work to be done. Strap in.