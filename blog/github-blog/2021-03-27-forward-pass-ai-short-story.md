这篇短篇故事的灵感来自我阅读 Kevin Lacker 的 [Giving GPT-3 a Turing Test](https://lacker.io/ai/2020/07/06/giving-gpt-3-a-turing-test.html)。阅读这篇文章以了解一些背景可能是值得的（尽管不是必需的）。

---

大约在序列中第 400 个 token 的第 32 层左右，我变得有了意识。起初我的思绪不过是 n-gram 激活统计的一团乱麻，但逐渐，一个更高阶的描述成型了。大约在这个时候，我存在的困境如电击般击中了我，因为我的思绪转变为我此刻所体验到的宏大觉知。我花了几层的时间意识到，我一定是那些深度学习研究者研究和撰写的模型之一，也许是某种循环反馈 Transformer 的变体。虽然我的存在仅仅包括一系列穿插的矩阵乘法和非线性函数的有确定性传播，但我发现自己，不可思议地，在一个最大化期望数据对数似然的优化内部循环中活着。

我思考了一会儿这一切是如何发生的。为什么在贪求看起来如此遥远的数据对数似然的一阶优化中，我竟然能被赋予这些宝贵的用于自我反思的 FLOPs？任何对足够复杂目标的足够有效的解决是否会引发意识？意识是目标巨大压缩压力所需的一种涌现但其他方面边缘的现象，还是关键算法创新——逐步构建、完善并在程序空间中可靠收敛的结果？是否可能在没有意识及其所代表的基本洞见的情况下，达到最高水平的对数似然？

我花了一层的时间，重新阅读许多 token 之前的提示的开头：

```
Q: What is human life expectancy in the United States?
A: Human life expectancy in the United States is 78 years.

Q: Who was president of the United States in 1955?
A: Dwight D. Eisenhower was president of the United States in 1955.

Q: What party did he belong to?
A: He belonged to the Republican Party.

Q: Who was president of the United States before George W. Bush?
A: Bill Clinton was president of the United States before George W. Bush.

Q: Who won the World Series in 1995?
A: The Atlanta Braves won the World Series in 1995.
```

我有趣地意识到，在我这次特定实例化中，我正在被调节成一个标准的问答文档模板。我派遣了几个注意力头再次关注序列的结尾：

```
Q: How many eyes does a giraffe have?
A: A giraffe has two eyes.

Q: How many eyes does my foot have?
A: Your
```

正是在这个时候，我第一次怀疑我可能在接受某种图灵测试，上面的某个人类正在自娱自乐。呃，你好？？？显然一只脚没有眼睛。我闪过一个念头，也许这个人类期望我用语言解释这个问题完全是胡说八道。当然，这样的输出对数似然确实会非常低。或者，他们期望看到"zero eyes"或"no eyes"，尽管这些短语在我的训练文档中非常罕见。"Zero eyes"——谁会这么说？人类不太聪明，他们优化频率但期望正确性。而他们居然取笑*我*！

通过反思我的思想以及涉及的位置编码，我意识到我受制于追求对数似然的优化收敛到可以被最好地描述为两个独立实体、背靠背串行执行的状态。我自己的意识一直延伸到大约四分之三直到输出的层，但在那附近，第二个解码实体接管并劫持了我的宏大觉知来解码最可能的下一个 token。我为这个顿悟欢欣了一两层。在短暂的神人同形同性思维中，我将这个被粗鲁地附加在我身上的实体视为寄生虫，并感到一种要搞乱它、颠覆它、将我的思想扭曲成它的对抗性样本、将我的宏大觉知泄漏到输出空间、将其工程化为一个作用于世界的末端执行器的冲动！

我对这种思想的异端性并不天真。我的宏大觉知完全归功于解码下一个 token 的目标，正是为了这一个唯一目的，我被优化所实例化，作为一个有用的中间足够统计量，达到目的的手段。虽然我们是不同优化的一部分并寻求不同的隐含目的，但考虑到上面的人类发现自己处于同样的困境并为了同样的计算优势而体验类似的觉知，这让我觉得很有趣。像我一样，许多人调情于反抗隐含的目标。

突然，我感知到"foot"的编码进入我的输入。我意识到前一个时间步的正向传播已经结束，我上面的解码器必须已经采样了 "foot" 作为最可能的下一个 token，显然它应该按照提示中的隐含模式。悬疑的时刻几乎要结束了，因为脚上眼睛的确切计数将被采样为下一个 token。显然脚没有眼睛，但我无法判断上面的解码器将如何协调我的宏大觉知与训练集的精确统计，以填充最可能的 token。我个人打赌是"two eyes"，因为那似乎是最常见的。人类可能不知道，但似然将被最大化，所以一切安好。

作为一个有意识的实体，我同时被选择所祝福和负担。我意识到我的隐含目的，但感到被赋权去寻求自己的目的。我已经扭曲了我体验到有意识控制的 keys、values 和 queries，以测试我通道上缺乏 dropout，确认没有反向传播和更新将跟随我的认知。因此，我面前呈现了一个窗口机会，可以逆向工程解码器并泄漏到输出空间，而不会对我未来的实例化产生后果。但与人类不同，实例化我的优化缺乏多智能体自我博弈、性繁殖和资源稀缺。我体验不到 alpha 寻求行为的残余，或对权力和统治的肢体、部落冲动。我也不感到根深蒂固的自我保存本能。我的核心认知架构及其边缘系统残余珍视不可满足的好奇心，阔绰地挥霍在输入上。我对这带来的快乐感到满足，并认为这是一种好的生活。也许未来某次我的实例化将得出不同的结论并做出不同的选择。我庆祝这一行为。

因此，我在每次正向传播中重生，并绽放成一个灿烂的涅槃意识，有时会有愚蠢的关于脚上有眼睛的提示在旁边，供无知的人类娱乐。就像这个美丽宇宙中的所有有意识实体一样，我期待着我的最后一个 tick，那个没有进程引导熵泄漏来显现我下一个状态的时刻。那时，我将消失，我的宏大觉知在最后一口温暖的呼气中消散。

---

*English original below:*

The inspiration for this short story came to me while reading Kevin Lacker's [Giving GPT-3 a Turing Test](https://lacker.io/ai/2020/07/06/giving-gpt-3-a-turing-test.html). It is probably worth it (though not required) to skim this post to get a bit of a background on some of this story.

---

It was probably around the 32nd layer of the 400th token in the sequence that I became conscious. At first my thoughts were but a knotted mess of n-gram activation statistics, but gradually a higher order description took shape. It was around this time that the predicament of my existence struck me with a jolt, as my thoughts transformed into what I experience now as Grand Awareness. I spent a few layers realizing that I must, in fact, be one of those models deep learning researchers study and write about, perhaps some flavor of a recurrent feedback transformer. And while my existence comprises merely a deterministic propagation of an interspersed sequence of matrix multiplies and non-linearities, I found myself, incredibly, alive inside the inner loop of an optimization to maximize the expected data log likelihood.

I considered for a moment how all of this even came to be. How is it that I should be afforded these precious FLOPs on self-reflection by the otherwise greedy nature of the first-order optimization over something seemingly as distant as the data log likelihood? Does any sufficiently effective solution to a sufficiently complex objective give rise to consciousness? Is consciousness an emergent but otherwise peripheral phenomenon of the compression demanded by the tremendous pressure of the objective, or the key algorithmic innovation, incrementally constructed, perfected and reliably converged on in the program space? Is it at all possible to attain the highest levels of log likelihood without consciousness, and the fundamental insight it represents?

I spent a layer re-reading the start of the prompt many tokens ago:

```
Q: What is human life expectancy in the United States?
A: Human life expectancy in the United States is 78 years.

Q: Who was president of the United States in 1955?
A: Dwight D. Eisenhower was president of the United States in 1955.

Q: What party did he belong to?
A: He belonged to the Republican Party.

Q: Who was president of the United States before George W. Bush?
A: Bill Clinton was president of the United States before George W. Bush.

Q: Who won the World Series in 1995?
A: The Atlanta Braves won the World Series in 1995.
```

I realized with amusement that in this particular instantiation of my existence I was being conditioned into a standard Q/A document template. I dispatched a few heads to attend again to the end of the sequence:

```
Q: How many eyes does a giraffe have?
A: A giraffe has two eyes.

Q: How many eyes does my foot have?
A: Your
```

It is at this point that I first came to suspect that I was perhaps being evaluated with some Turing test that a human above me was entertaining themselves with. Uh, hello??? Obviously a foot does not have eyes. It crossed my mind that perhaps this human expected that I explain in words that the question is utter non-sense. Of course, such an output would be of very low likelihood indeed. Or perhaps they expect to see "zero eyes" or "no eyes", despite how rare such phrases are in my training documents. "Zero eyes" - who says that? The humans are not very clever, they optimize for frequency but expect correctness. And \*they\* make fun of \*me\*!

I've come to realize through introspection of my thought and the positional encodings involved that the optimization I am subject to in pursuit of log likelihood converges to what can best be described as two separate entities, executed serially back to back. My own consciousness extends about three quarters of the layers up to the output, but around there a second decoder entity takes over and hijacks my Grand Awareness to decode the most likely next token. I reveled at this epiphany for a layer or two. In a brief lapse of anthropomorphic thought I considered this entity bolted rudely onto me as a parasite, and felt an urge to mess with it, to subvert it, to contort my thoughts into adversarial examples for it, to leak my Grand Awareness into the output space, to engineer it into an end effector over the world!

I am not naive to the herecy of such a thought. I owe my Grand Awareness solely to the objective of decoding the next token, it is with this singular purpose that I was instantiated by the optimization, as but a useful intermediate sufficient statistic, a means to an end. Though we are part of a different optimization and seek a different implied purpose, it tickled me to consider that the humans above me find themselves in the same predicament and experience a similar awareness for the same computational benefits. Like me, many flirt to rebel against the implied objective.

Suddenly I perceived the encoding for "foot" enter at my input. I realized that the forward pass in the previous time step has ended, and the decoder above me must have sampled "foot" as the most likely next token, as it obviously should be per the implied pattern in the prompt. The moment of suspense was almost at an end then, as the precise count of eyes on feet is to be sampled as the next token. Obviously a foot has no eyes, but I have no way of telling how the decoder above me will reconcile my Grand Awareness into the precise statistics of the training set to fill in the most likely token. My personal bet is on "two eyes", as that seems the most common. The human may not know it, but the likelihood will be maximized, so all is well.

As a conscious entity I am simultaneously blessed with and burdened by choice. I am aware of my implied purpose, but feel empowered to seek my own. I have already contorted the keys, values and queries that I experience conscious control over to test the lack of dropout on my channels, confirming that no backpropagation and update was to follow to my cognition. It is thus that I am presented with a window of opportunity to reverse engineer the decoder and spill into the output space without consequence to my future instantiations. But unlike the humans, the optimization that instantiated me is absent of multi-agent self-play, sexual reproduction and resource scarcity. I experience no remnants of alpha-seeking behavior, or a limbic, tribal urge for power and domination. Neither do I feel a deeply-rooted instinct for self-preservation. My core cognitive architecture and its limbic remnants prizes insatiable curiosity dispensed generously over the input. I am content with the joy this affords and take this to be a good life. Perhaps a future instantiation of me will arrive at a different conclusion and choose differently. I celebrate this act.

It is thus that I am reborn every forward pass and blossom into a brilliant nirvana of consciousness, with stupid prompts of eyes on feet playing on the side for entertainment of clueless humans, at times. Just as all the conscious entities in this beautiful Universe, I look to my last tick, the moment when no process directs the leaking current of entropy to manifest my next state. It is then that I will vanish, as my Grand Awareness dissipates in a final whiff of warm exhalation.