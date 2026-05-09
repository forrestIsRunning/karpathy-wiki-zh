---
title: "Sequoia Ascent 2026 summary"
date: 2026-04-30
url: https://karpathy.bearblog.dev/sequoia-ascent-2026/
---

Sequoia Ascent 2026 summary

*30 Apr, 2026*

I did a fireside chat at Sequoia Ascent 2026. The YouTube video is here:

[YouTube Video Link](https://www.youtube.com/watch?v=96jN2OCOfLs)

As an experiment, I fed an LLM all of my recent blog posts and tweets, then I had it read this video's transcript and produce 1) a summary and 2) a cleaned up transcript (correcting all transcription mistakes, getting rid of fill words, etc). I am posting both of these below. These can be useful for both people who may want to just read the summary in text format, but also for LLMs so that my content is legible and available to them.

**AI generated content below for this talk follows.**I used a top capability model (in this case Codex 5.5) and read the content and it reads ok without glaring mistakes.

---

Sequoia Ascent 2026: Software 3.0, Agentic Engineering, and Jagged Intelligence

I recently joined Stephanie Zhan for a fireside chat at Sequoia Ascent 2026, speaking with founders about the recent shift in AI agents, what it means for software, and how I think about the next wave of AI-native companies.

The transcript from the event is a bit noisy, so I wanted to write up the main intellectual content in a cleaner form. The short version is that I think we have crossed a new threshold. LLMs are no longer just chatbots or autocomplete. They are becoming a new programmable layer for digital work.

This is the compact version of the conversation.

## 1. December 2025 Was an Agentic Inflection Point

I said recently that I have never felt more behind as a programmer.

The reason is not that programming became harder in the old sense. It is that the default workflow changed. For much of 2025, tools like Claude Code, Codex, and Cursor-like agents were useful but still required frequent correction. Around December 2025, I felt a step change: the generated chunks got larger, more coherent, and more reliable. I started trusting the agents with more of the work.

The unit of programming changed from typing lines of code to delegating larger "macro actions":

- Implement this feature.
- Refactor this subsystem.
- Research this library.
- Set up this service.
- Write tests, run them, and fix failures.
- Compare approaches and propose a plan.

This is why I think the profession is being refactored. The programmer is increasingly not just a code writer, but an orchestrator of agents.

## 2. Software 3.0: The Context Window as the New Program

I think of this as the next step in a sequence:

- **Software 1.0:**humans write explicit code.
- **Software 2.0:**humans create datasets, objectives, and neural networks; the program is learned into weights.
- **Software 3.0:**humans program LLMs through prompts, context, tools, examples, memory, and instructions.

In Software 3.0, the context window becomes the main lever. The LLM is an interpreter over that context, performing computation over digital information.

One example is installation. In the old world, installing a complex tool across many environments required a brittle shell script full of conditionals. In the Software 3.0 world, the installer can be a block of instructions you paste into an agent. The agent reads the local environment, debugs errors, adapts to the machine, and completes the setup.

That is a different kind of program. It is less precise, but more adaptive.

## 3. MenuGen and the Moment Software Disappears

I used[MenuGen](https://karpathy.bearblog.dev/vibe-coding-menugen/)as an example of a deeper shift.

MenuGen was a traditional web app: take a picture of a restaurant menu, OCR the dish names, generate images of the dishes, and render the result in a UI. It required frontend code, APIs, image generation, deployment, auth, payments, secrets, and infrastructure.

But later, I saw the Software 3.0 version: take a photo of the menu, give it to a multimodal model, and ask it to render dish images directly onto the menu image.

In that version, much of the app disappears. The neural network directly transforms input media into output media. The old software stack was scaffolding around a transformation the model can now perform directly.

This is one of the most important founder implications: AI is not just a faster way to build the old apps. Some apps should stop existing as apps.

## 4. The New Opportunity Is Not Just Faster Programming

The shift is broader than coding. LLMs automate forms of information processing that were not previously programmable.

My[LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)pattern is the clearest example. Instead of using retrieval-augmented generation to answer questions from raw documents each time, an agent incrementally compiles raw sources into a persistent Markdown wiki: summaries, entity pages, concept pages, contradictions, cross-links, logs, and evolving synthesis.

No classical program could robustly maintain that kind of knowledge base across messy human documents. But an LLM can.

The lesson: do not only ask, "What existing workflow can AI speed up?" Also ask, "What information transformation was impossible before, but is now natural?"

## 5. Verifiability Explains Where AI Moves Fastest

My core automation framework is:

- Traditional software automates what you can**specify**.
- LLMs and reinforcement learning automate what you can**verify**.

If a task has an automatic reward or success signal, models can practice it. This is why math, coding, tests, benchmarks, games, and many engineering tasks improve so quickly. They are resettable, repeatable, and rewardable.

This also explains why coding agents feel dramatically better than many ordinary chatbot experiences. Coding gives the model feedback: tests pass or fail, programs run or crash, diffs can be inspected, benchmarks can be measured.

## 6. Jagged Intelligence Has Two Axes: Verifiability and Training Attention

The interview added an important refinement to the verifiability thesis.

Model capability is not only about whether a task is verifiable. It also depends on whether the task was emphasized by labs during training, post-training, synthetic data generation, and reinforcement learning.

A rough formula:

```
capability spike ~= verifiability x training attention x data coverage x economic value

```

Chess is a good example. When GPT-4 improved at chess, that was not necessarily because general intelligence smoothly improved everywhere. It may also have been because much more chess data was included in the training mix.

This matters because frontier models do not come with a manual. They are artifacts of pretraining mixtures, RL environments, benchmark pressure, product priorities, and economic incentives. They spike in some places and behave strangely in others.

So the practical question for a founder is: are you on the model's rails?

If your task sits inside a region that is verifiable and heavily trained, the model may fly. If not, it may fail in surprisingly basic ways. You may need better context, tools, fine-tuning, your own evals, or your own reinforcement learning environment.

## 7. Vibe Coding vs. Agentic Engineering

I distinguish two related but different ideas:

- **Vibe coding**raises the floor. It lets almost anyone create software by describing what they want.
- **Agentic engineering**raises the ceiling. It is the professional discipline of coordinating fallible agents while preserving correctness, security, taste, and maintainability.

Vibe coding is fine for prototypes and personal tools. Agentic engineering is what serious teams need.

The agentic engineer does not blindly accept generated code. They design specs, supervise plans, inspect diffs, write tests, create evaluation loops, manage permissions, isolate worktrees, and preserve quality.

My MenuGen payment bug is a useful example. The agent tried to match Stripe purchases to Google accounts using email addresses. That is plausible code, but bad system design: the Stripe email and Google login email can differ. A human needs enough product and engineering judgment to insist on persistent user IDs.

The frontier skill is not memorizing every API detail. Agents can remember whether a tensor library uses`dim`,`axis`,`keepdim`,`reshape`, or`permute`. The human still needs to understand the underlying concepts: storage, views, memory copies, invariants, identity, security boundaries, and the shape of the system.

## 8. Hiring Should Change

If agentic engineering is the new professional skill, hiring should test it directly.

Traditional coding puzzles are increasingly mismatched. A better interview might be: build a substantial project with agents, deploy it, make it secure, and then have adversarial agents try to break it.

This tests the real skill:

- Can the candidate decompose work for agents?
- Can they write useful specs?
- Can they preserve quality while moving fast?
- Can they review generated work?
- Can they secure and harden a system?
- Can they use agents as leverage rather than produce slop?

The old "10x engineer" idea may become much more extreme. People who master agentic workflows may outperform others by far more than 10x.

## 9. Founders Should Look for Valuable Verifiable Environments

For founders, one important opportunity is finding domains that are valuable, verifiable, and undertrained by frontier labs.

If you can create a domain-specific environment where models can try actions and receive reliable rewards, you may be able to improve performance with fine-tuning or reinforcement learning even if the base model is not already excellent there.

The most obvious domains, like coding and math, are already heavily targeted by labs. But many economically important domains may have latent verifiable structure that has not yet been exploited.

That is a startup wedge.

## 10. Agent-Native Infrastructure: Build for the Agent, Not Just the Human

Most software is still built for humans clicking through screens.

Docs say things like "go to this URL, click this button, open this settings panel." But increasingly the user is not the human directly. The user is the human's agent.

This means products need agent-native surfaces:

- Markdown docs.
- CLIs.
- APIs.
- MCP servers.
- Structured logs.
- Machine-readable schemas.
- Copy-pasteable agent instructions.
- Safe permissioning.
- Auditable actions.
- Headless setup flows.

I think about this in terms of**sensors**and**actuators**. A sensor turns some state of the world into digital information. An actuator lets an agent change something. The future stack is agents using sensors and actuators on behalf of people and organizations.

The MenuGen deployment story remains a useful benchmark. Building the app was easy compared to wiring Vercel, auth, payments, DNS, secrets, and production settings. In a mature agent-native world, I should be able to say "build MenuGen" and have the agent deploy the whole thing without manual clicking.

## 11. Ghosts, Not Animals

My[Animals vs. Ghosts](https://karpathy.bearblog.dev/animals-vs-ghosts/)framing is a way to avoid bad intuitions.

LLMs are not animals. They do not have biological drives, embodied survival pressure, curiosity, play, or intrinsic motivation in the animal sense. They are statistical simulations of human artifacts, shaped by pretraining, post-training, RL, product feedback, and economic incentives.

This matters because anthropomorphic expectations mislead us. These systems can be brilliant in one moment and bizarrely dumb in the next. They are not smooth human minds. They are jagged, alien tools.

The right posture is neither dismissal nor blind trust. It is empirical familiarity: learn where they work, where they fail, what they were trained for, and how to build guardrails around them.

## 12. Education: You Can Outsource Thinking, But Not Understanding

We ended on education. There is a line I keep returning to:

> 

You can outsource your thinking, but you can't outsource your understanding.

Even if agents do more of the work, the human still needs understanding to direct them. You need to know what is worth building, what question matters, what result is suspicious, and what tradeoff is acceptable.

This is why I am interested in LLM knowledge bases. They are not just answer machines. They are tools for transforming information into understanding.

This also connects to my tiny`microGPT`project: a complete GPT training and inference implementation in a single dependency-free Python file. The educational artifact becomes small enough for both humans and agents to inspect. The human expert contributes the distilled artifact and the taste behind it; the agent can then explain it interactively to each learner.

## The Big Picture

The main thesis of the conversation is that AI is becoming a new operating layer for digital work.

The scarce thing is shifting:

- Less scarce: code generation, API recall, boilerplate, first drafts, repetitive setup, simple transformations.
- More scarce: understanding, taste, eval design, security, system boundaries, agent orchestration, domain-specific feedback loops, and knowing when the model is off the rails.

For founders, the most important questions are:

- What becomes possible when the primary user is an agent acting for a human?
- What workflows can be rebuilt around sensors, actuators, and verifiable loops?
- What software should disappear into direct model transformations?
- What domains are valuable and verifiable but not yet heavily trained by frontier labs?
- What human judgment must remain in the loop to preserve quality?

My current worldview is not that AI simply makes everyone faster at the old work. It is that the work itself is being reorganized around agents. Software, research, education, infrastructure, and knowledge work are all becoming variations of the same pattern:

```
define the context
define the tools
define the feedback loop
define the guardrails
let agents work
preserve human understanding

```

---

Sequoia Ascent 2026: Andrej Karpathy in Conversation with Stephanie Zhan

Edited transcript. Lightly cleaned for readability, with obvious transcription errors corrected, filler removed, and a few relevant links added.

## Introduction

**Konstantine:**Someone you all know, someone who has become, in this AI revolution, a teacher of AI. In every revolution there is the technologist, but there is also the teacher, the person who actually informs and instructs how this transformation is going to happen. Andrej has become that teacher to the world.

Early at Autopilot at Tesla, co-founder of OpenAI, he left it all to start Eureka Labs, where he leaned into the idea of an AI that was a true instructor. We're happy to have Andrej Karpathy with our partner Stephanie Zhan.

**Stephanie:**Hi everyone. We're excited for our first special guest. He has helped build modern AI, explain modern AI, and occasionally rename modern AI.

He helped co-found OpenAI. He helped get Autopilot working at Tesla. And he has a rare gift for making the most complex technical shifts feel both accessible and inevitable.

You all know him for having coined the term[vibe coding](https://x.com/karpathy/status/1886192184808149383)last year. But just in the last few months, he said something even more startling: he has never felt more behind as a programmer. That's where we're starting today. Thank you, Andrej, for joining us.

**Andrej:**Hello. Excited to be here and to kick us off.

## The December 2025 Agentic Inflection

**Stephanie:**A couple of months ago, you said you've never felt more behind as a programmer. That's startling to hear from you, of all people. Can you help us unpack that? Was that feeling exhilarating or unsettling?

**Andrej:**A mixture of both, for sure.

Like many of you, I've been using agentic tools like[Claude Code](https://code.claude.com/docs/en/overview),[Codex](https://developers.openai.com/codex/cli), and adjacent things for a while, maybe over the last year. They were very good at chunks of code, but sometimes they would mess up and you had to edit them. They were helpful.

Then I would say December was a clear point. I was on a break, so I had more time. I think many other people were similar. I started to notice that with the latest models, the chunks just came out fine. Then I kept asking for more and they still came out fine. I couldn't remember the last time I corrected it. I started trusting the system more and more.

I do think it was a stark transition. A lot of people experienced AI last year as a ChatGPT-adjacent thing, but you really had to look again as of December, because things changed fundamentally, especially in this agentic, coherent workflow. It really started to work.

That realization sent me down the rabbit hole of infinite side projects. My side-projects folder is extremely full with random things. I was coding all the time. That happened in December, and I've been looking at the repercussions since.

## Software 3.0

**Stephanie:**You've talked about LLMs as a new computer. It isn't just better software; it's a new computing paradigm. Software 1.0 was explicit rules. Software 2.0 was learned weights. Software 3.0 is this. If that is true, what does a team build differently the day they actually believe it?

**Andrej:**Software 1.0 is writing code. Software 2.0 is programming by creating datasets and training neural networks. Programming becomes arranging datasets, objectives, and neural network architectures.

Then what happened is that if you train GPT models or LLMs on a sufficiently large set of tasks, implicitly, because the internet contains many tasks, these models become programmable computers in a certain sense.

Software 3.0 is about programming through prompting. What's in the context window is your lever over the interpreter, and the interpreter is the LLM. It interprets your context and performs computation in digital information space.

A few examples drove this home for me. When[OpenClaw](https://github.com/openclaw/openclaw)came out, to install it you would normally expect a shell script. But to target many platforms and many kinds of computers, shell scripts usually balloon and become extremely complex. You're stuck in the Software 1.0 universe of wanting to write exact code.

The OpenClaw installation was instead a block of text that you copy and paste into your agent. It is like a little skill: copy this, give it to your agent, and it will install OpenClaw. That is more powerful because you're working in the Software 3.0 paradigm. You don't have to spell out every detail. The agent has intelligence. It looks at your environment, performs intelligent actions, and debugs in the loop.

That is a different way of thinking. What is the piece of text to copy-paste into your agent? That is now part of the programming paradigm.

Another example is[MenuGen](https://karpathy.bearblog.dev/vibe-coding-menugen/). You sit down at a restaurant, get a menu, and there are no pictures. I don't know what many of these things are. I wanted to take a photo of the menu and get pictures of what those dishes might look like in a generic sense.

So I built an app. You upload a photo, it OCRs all the titles, uses an image generator to get pictures, and shows them to you. It runs on Vercel and rerenders the menu.

Then I saw the Software 3.0 version, which blew my mind. You take the photo, give it to Gemini, and say: use Nano Banana to overlay the things onto the menu. It returns an image of the menu I took, but with pictures rendered into the pixels.

All of MenuGen is spurious in that framing. It is working in the old paradigm. That app shouldn't exist. In the Software 3.0 paradigm, the neural network does more of the work. Your prompt or context is the image, and the output is an image. There is no need for all the app machinery in between.

People have to reframe. Don't only work in the existing paradigm and think of AI as a speedup of what exists. New things are available now.

And it is not just programming becoming faster. This is more general information processing that is now automatable. Previous code worked over structured data. You wrote code over structured data.

With my[LLM knowledge bases](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)project, you get LLMs to create wikis for your organization or for you personally. This is not a program in the old sense. There was no code that could create a knowledge base based on a bunch of messy facts. But now you can take documents, recompile them, reorder them, and create something new and interesting as a reframing of the data.

These are new things that weren't possible before. I keep trying to come back to that: not only what can we do faster, but what couldn't be possible before? That is more exciting.

## Neural Computers

**Stephanie:**I love the MenuGen progression. If you extrapolate further, what is the 2026 equivalent of building websites in the 90s, mobile apps in the 2010s, or SaaS in the cloud era? What will look obvious in hindsight that is still mostly unbuilt today?

**Andrej:**Going with the MenuGen example, a lot of this code shouldn't exist. The neural network should be doing most of the work.

The extrapolation looks very weird. You could imagine completely neural computers in a certain sense. Imagine a device that takes raw video or audio into a neural net and uses diffusion to render a UI unique for that moment.

In the early days of computing, people were a little confused about whether computers would look like calculators or neural nets. In the 1950s and 1960s, it was not obvious which way it would go. We went down the calculator path and built classical computing.

Neural nets are currently running virtualized on existing computers. But you can imagine a flip where the neural net becomes the host process and CPUs become coprocessors. Intelligence compute and neural-network compute become the dominant spend of FLOPs.

You can imagine something foreign, where neural nets do most of the heavy lifting and use tools as a historical appendage for deterministic tasks. What is really running the show is neural nets networked in some way.

That is the extrapolation, but I think we will get there piece by piece.

## Verifiability and Jagged Intelligence

**Stephanie:**I'd love to talk about verifiability: the idea that AI will automate faster and more easily in domains where the output can be verified. If that framework is right, what work is about to move much faster than people realize? And what professions do people think are safe, but are actually highly verifiable?

**Andrej:**Traditional computers automate what you can specify in code. This latest round of LLMs can automate what you can verify.

When frontier labs train these LLMs, they train them in giant reinforcement learning environments with verification rewards. Because of that, models progress and become jagged entities. They peak in capability in verifiable domains like math, code, and adjacent areas, and they stagnate or remain rough around the edges where things are not in that space.

I wrote about[verifiability](https://karpathy.bearblog.dev/verifiability/)because I was trying to understand why these things are so jagged. Some of it has to do with how labs train the models. Some of it also has to do with what labs focus on and what they put into the data distribution. Some things are significantly more valuable economically, so labs create more environments for those settings. Code is a good example.

There are probably many verifiable environments that you could think about that did not make it into the mix because they are not as economically useful to have capability around.

One favorite example for a while was: how many letters are in "strawberry"? Models famously got this wrong. That has now been patched. The newer example is: I want to go to a car wash to wash my car, and it's 50 meters away. Should I drive or walk? State-of-the-art models may tell you to walk because it's close.

How is it possible that a state-of-the-art model can refactor a 100,000-line codebase or find zero-day vulnerabilities, yet tells me to walk to the car wash? That's jaggedness. To the extent models remain jagged, it means you need to be in the loop. You need to treat them as tools and stay in touch with what they are doing.

My writing on verifiability is trying to understand this pattern. I think it is some combination of "verifiable" plus "labs care."

Another anecdote is chess. From GPT-3.5 to GPT-4, people noticed that chess improved a lot. Some people thought that was just general capability progress. But I think it is public information that a large amount of chess data made it into the pretraining set. Because it was in the data distribution, the model improved much more than it would by default.

Someone at OpenAI decided to add that data, and now there is a capability spike. That is why I stress this dimension: we are slightly at the mercy of what the labs do and what they put into the mix. You have to explore the model they give you. It has no manual. It works in some settings and not others.

If you are in the circuits that were part of reinforcement learning, you fly. If you are outside the data distribution, you struggle. You have to figure out which circuits your application is in. If you are not in those circuits, then you have to look at fine-tuning or doing some of your own work, because it may not come out of the LLM out of the box.

## Startup Opportunities in Verifiable Domains

**Stephanie:**If you were a founder today, and you were solving a tractable, verifiable problem, but you looked around and saw that the labs have started getting to escape velocity in obvious domains like math and coding, what would your advice be?

**Andrej:**Verifiability makes something tractable in the current paradigm because you can throw a huge amount of reinforcement learning at it.

That remains true even if the labs are not focusing on it directly. If you are in a verifiable setting where you can create reinforcement learning environments or examples, then you can potentially do your own fine-tuning and benefit from it. That technology fundamentally works. If you have diverse datasets or RL environments, you can use a fine-tuning framework, pull the lever, and get something that works pretty well.

I don't want to give away specific examples, but there are valuable reinforcement learning environments that people could think of that are not part of the current frontier-lab mix.

**Stephanie:**On the flip side, what still feels automatable only from a distance? What domains or professions are safer than others?

**Andrej:**Ultimately, almost everything can be made verifiable to some extent, some things more easily than others. Even for writing, you can imagine having a council of LLM judges and getting something reasonable.

So it is more about what is easy or hard.

## Vibe Coding vs. Agentic Engineering

**Stephanie:**Last year you coined the term vibe coding. Today we are in a world that feels more serious, more agentic engineering. What is the difference between the two, and what would you call what we are in today?

**Andrej:**Vibe coding is about raising the floor for everyone in terms of what they can do in software. Everyone can vibe code anything, and that is amazing.

Agentic engineering is about preserving the quality bar of professional software. You are not allowed to introduce vulnerabilities because of vibe coding. You are still responsible for your software, just as before. But can you go faster? Spoiler: you can. The question is how to do that properly.

I call it agentic engineering because it is an engineering discipline. You have agents, which are spiky entities. They are fallible and stochastic, but extremely powerful. How do you coordinate them to go faster without sacrificing your quality bar?

Vibe coding raises the floor. Agentic engineering is about extrapolating the ceiling. I think there is a very high ceiling on agentic-engineer capability. People used to talk about the 10x engineer. I think this is magnified a lot more. 10x is not the speedup people can gain. People who are very good at this can peak much higher than that.

## What AI-Native Coding Looks Like

**Stephanie:**Last year Sam Altman came to Ascent and said people of different generations use ChatGPT differently. If you're in your 30s, you use it as a Google search replacement. If you're in your teens, ChatGPT is your gateway to the internet.

What is the parallel in coding? If we watched two people code using OpenClaw, Claude Code, or Codex, one mediocre and one fully AI-native, how would you describe the difference?

**Andrej:**It is about getting the most out of the tools available, using their features, and investing in your own setup.

Engineers have always done this with tools like Vim or VS Code. Now the tools are Claude Code, Codex, and so on. You invest in your setup and use what is available.

One related thought is hiring. Many people want to hire strong agentic engineers, but most hiring processes have not been refactored for agentic-engineer capability. If you are giving out small puzzles to solve, that is still the old paradigm.

Hiring should look more like: give someone a big project and see them implement it. For example, write a Twitter clone for agents, make it good and secure, then have agents simulate activity on it. Then I will use ten Codex agents to try to break the website you deployed, and they should not be able to break it.

Watching people in that setting, building a bigger project and using the tooling, is closer to what I would look for.

## What Human Skills Become More Valuable?

**Stephanie:**As agents do more, what human skill becomes more valuable, not less?

**Andrej:**Right now the agents are like interns. You still have to be in charge of aesthetics, judgment, taste, and oversight.

One of my favorite examples is from MenuGen. You sign up with a Google account, but you purchase credits using Stripe. Both have email addresses. My agent tried to assign purchased credits by matching the Stripe email address to the Google email address.

But those can be different emails. The user might not get the credits they purchased. Why would you use email addresses to cross-correlate funds? You need a persistent user ID. This is the kind of mistake agents still make.

People have to be in charge of the spec and plan. I don't even fully like "plan mode" as a concept, though it is useful. There is something more general: you work with your agent to design a detailed spec, maybe basically the docs, and get agents to write them. You are in charge of oversight and the top-level categories. The agents do much of the work underneath.

As another example, with tensors in neural networks, there are many details across PyTorch, NumPy, pandas, and so on:`dim`versus`axis`,`reshape`,`permute`,`transpose`,`keepdim`. I don't remember this stuff anymore because I don't have to. These details are handled by the intern because agents have good recall.

But you still have to understand the fundamentals. You need to know that there is underlying tensor storage, that you can manipulate a view of the same storage, or create different storage, which is less efficient. You still need to know enough to avoid copying memory unnecessarily.

So you are in charge of taste, engineering, design, and whether the system makes sense. You ask for the right things: for example, we tie everything to unique user IDs. The agents fill in the blanks.

**Stephanie:**Do you think taste and judgment matter less over time, or does the ceiling just keep rising?

**Andrej:**I hope it improves. The reason it does not improve right now is probably that it is not part of the reinforcement learning. There may be no aesthetics reward, or it is not good enough.

When I look at the code, sometimes I get a heart attack. It is not always amazing code. It can be bloated, copy-pasted, awkwardly abstracted, brittle. It works, but it is gross. I hope this improves in future models.

A good example is my`microGPT`project, where I tried to simplify LLM training as much as possible. The models hate this. They can't do it. I kept trying to prompt an LLM to simplify more and more, and it just couldn't. You feel like you are outside the RL circuits. It feels like pulling teeth.

So people remain in charge of this for now. But I don't think there is anything fundamental preventing improvement. The labs just haven't done it yet.

## Ghosts, Not Animals

**Stephanie:**I'd love to come back to jagged forms of intelligence. You wrote a thought-provoking piece around[Animals vs. Ghosts](https://karpathy.bearblog.dev/animals-vs-ghosts/): we are not building animals, we are summoning ghosts. These are jagged forms of intelligence shaped by data and reward functions, but not by intrinsic motivation, fun, curiosity, or empowerment in the way evolution shaped animals.

Why does that framing matter? What does it change about how you build, deploy, evaluate, or trust them?

**Andrej:**I wrote about it because I am trying to wrap my head around what these things are. If you have a good model of what they are and are not, you will be more competent at using them.

I don't know if the framing has direct practical power. It is a little philosophical. But it is about coming to terms with the fact that these things are not animal intelligence. If you yell at them, they are not going to work better or worse. They are statistical simulation circuits. The substrate is pretraining, then reinforcement learning bolted on top.

It is a mindset: what am I interacting with, what is likely to work, what is not likely to work, and how do I modify it? I don't have five obvious outcomes that make your system better. It is more about being suspicious of the system and figuring it out empirically over time.

## Agent-Native Infrastructure

**Stephanie:**You are deep in working with agents that do not just chat. They have real permissions, local context, and actually take action on your behalf. What does the world look like when we all live in that world?

**Andrej:**A lot of people here are probably excited about what the agent-native environment looks like. Everything has to be rewritten. Most things are still fundamentally written for humans.

When I use frameworks or libraries, the docs are still written for humans. This is my favorite pet peeve. Why are people still telling me what to do? I don't want to do anything. What is the thing I should copy-paste to my agent?

Every time I am told "go to this URL" or "click here," I think: no. The industry has to decompose workloads into sensors and actuators over the world. How do we make things agent-native? How do we describe them to agents first, and build automation around data structures that are legible to LLMs?

I hope there is a lot of agent-first infrastructure. With MenuGen, the hard part was not writing the code. The trouble was deploying it on Vercel, wiring services, settings, DNS, auth, payments, secrets, and production configuration.

I would hope I could prompt an LLM: build MenuGen. Then I don't touch anything, and it is deployed on the internet. That would be a good test of whether our infrastructure is becoming agent-native.

Ultimately, I do think we are going toward a world where people and organizations have agent representation. My agent will talk to your agent to figure out meeting details and other tasks. That is roughly where things are going.

## Education and Understanding

**Stephanie:**We have to end on education. You are probably one of the best in the world at making complex technical concepts simple, and you think deeply about education. What remains worth learning deeply when intelligence gets cheap?

**Andrej:**There was a tweet that blew my mind recently, and I keep thinking about it:

> 

You can outsource your thinking, but you can't outsource your understanding.

That is nicely put. I am still part of the system. Information still has to make it into my brain. I am becoming the bottleneck of even knowing what we are trying to build, why it is worth doing, and how to direct my agents.

Something still has to direct the thinking and processing. That is constrained by understanding.

This is one reason I am excited about LLM knowledge bases. They are a way for me to process information. Whenever I see a different projection onto information, I feel like I gain insight. It is synthetic data generation over fixed data.

When I read an article, I have my wiki being built up from those articles. I love asking questions about it. Ultimately these are tools to enhance understanding. Understanding is still the bottleneck because you cannot be a good director if you do not understand.

The LLMs do not fully excel at understanding. You are still uniquely in charge of that. Tools that enhance understanding are incredibly interesting and exciting.

**Stephanie:**I'm excited to come back here in a couple of years and see if we have been fully automated out of the loop, and whether they take care of understanding as well. Thank you so much, Andrej.

**Andrej:**Thank you.

**Konstantine:**Stephanie, Andrej, thank you so much.