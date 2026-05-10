2014 年 [ImageNet 大规模视觉识别挑战赛](http://www.image-net.org/challenges/LSVRC/2014/)（ILSVRC）的结果在几天前[发布](http://www.image-net.org/challenges/LSVRC/2014/results)了。《纽约时报》也[报道了此事](http://bits.blogs.nytimes.com/2014/08/18/computer-eyesight-gets-a-lot-more-accurate/)。ILSVRC 是计算机视觉领域最大的挑战赛之一，每年都有团队竞争在该数据集上达到最先进水平。该挑战基于 ImageNet 数据集的一个子集，该数据集最初由 [Deng 等人 2009 年](http://www.image-net.org/papers/imagenet_cvpr09.pdf)收集，自 2010 年以来一直由我们斯坦福的实验室组织。今年，该挑战赛的参与人数创下了纪录，比去年增加了 50%，分类和检测任务都取得了惊人的进步，记录被打破。

>（我个人的）**ILSVRC 2014 总结**：团队数量增加 50%。分类和检测性能提升 50%。到处都是 ConvNet 集成。Google 团队获胜。

当然，远不止这些，所有细节和收获将在即将于 9 月 12 日在苏黎世举行的 [ECCV 2014 研讨会](http://image-net.org/challenges/LSVRC/2014/eccv2014)上详细讨论。

此外，我们刚刚（9 月 2 日）在 arXiv 上发表了一篇预印本，描述了 ILSVRC 的完整历史和大量相关分析，[请在 arXiv 上查看](http://arxiv.org/abs/1409.0575)。本文将重点介绍我贡献的论文部分（第 6.4 节：大规模图像分类的人类准确率）并描述其背景。

### ILSVRC 分类任务

为了这篇文章的目的，我想特别关注图像分类，因为这是许多其他计算机视觉任务的共同基础。分类任务由训练集中的 120 万张图像组成，每张图像标注为 1000 个类别之一，涵盖各种各样的物体、动物、场景，甚至一些抽象的几何概念，如 *"hook"* 或 *"spiral"*。测试集的 10 万张图像随数据集一起发布，但标签被隐藏以防止团队在测试集上过拟合。团队需要预测 5 个（共 1000 个）类别，如果至少有一个预测与真实标签一致，则认为该图像分类正确。测试集评估在我们这边进行，将预测结果与我们的真实标签集进行比较。

示例图像。[这里](http://cs.stanford.edu/people/karpathy/cnnembed/)查看全尺寸图像。

### GoogLeNet 的惊人表现

大约一周前我查看了结果，对 GoogLeNet 在分类任务上的获胜提交特别感兴趣，它在 ILSVRC 测试集上仅达到了 6.7% 的 Hit@5 错误率。我对分类任务的范围和难度相对熟悉：这些是无约束的互联网图像。它们是视角、光照条件和各种想象得到的变体的丛林。这就引出了一个问题：*人类的表现如何？*

计算机视觉中现在有几个任务，我们的模型性能接近甚至*超越*人类。这些任务的例子包括人脸验证、各种医学成像任务、汉字识别等。然而，这些任务中的许多都相当受限，因为它们假设输入图像来自一个非常特定的分布。例如，人脸验证模型可能只接受对齐、居中且归一化的图像作为输入。在许多方面，ImageNet 更难，因为图像直接来自"互联网丛林"。我们的模型有可能在如此无约束的任务上达到人类性能吗？

### 计算人类准确率

简而言之，我认为获胜团队的惊人表现只有在与人类准确率对比时才有意义。我也处于能够评估它的独特位置（因为我和 ILSVRC 组织者共享办公空间），所以我着手量化人类准确率，并描述人类预测与获胜模型预测之间的差异。

*等等，人类准确率不是 100%吗？* 谢谢，这是个好问题。并不是，因为 ILSVRC 数据集的标注方式与我们在这里分类的方式不同。例如，为了收集"边境梗"类别的图像，组织者在互联网上搜索该查询并检索了大量图像。然后通过让人类回答一个二选一的"这是不是边境梗？"来对它们进行一些过滤。通过筛选的就成了"边境梗"类别，其他 1000 个类别也是如此。因此，数据不是以判别方式收集的，而是以二元方式收集的，并且也存在错误和不准确的情况。有些图像有时也可能包含多个 ILSVRC 类别，等等。

*CIFAR-10 插曲。* 有趣的是，大约 4 年前我在 CIFAR-10 上进行了类似（但更快且不那么详细）的人类分类准确率分析。当时最先进水平是 Adam Coates 的 77%，而我自己的准确率是 94%。我认为现在最好的 ConvNet 大约能到 92%。关于那篇文章可以在[这里](https://karpathy.github.io/2011/04/27/manually-classifying-cifar10/)找到。我从没想过几年后我会为 ImageNet 做同样的事情 :)

有一个问题需要澄清。你可能会问：*但等等，ImageNet 测试集的标签最初就是从人类那里获得的。为什么要重新标注一遍？人类性能按定义不是 0%吗？* 有点道理，但也不完全对。重要的是要记住，ImageNet 是以二元任务的形式进行标注的。例如，为了收集狗类"凯尔皮"的图像，查询被提交给搜索引擎，然后使用 Amazon Mechanical Turk 上的人类来完成过滤噪声的二元任务。而 ILSVRC 分类任务则是 1000 路分类。它不是用于收集数据的那种二元任务。

### 标注界面

我开发了一个标注界面来帮助评估人类性能。它看起来与下面的截图类似但不完全相同：

标注界面的截图。[亲自尝试](http://cs.stanford.edu/people/karpathy/ilsvrc/)。

该界面由左侧的测试图像和右侧列出的 1000 个类别组成。每个类别后面跟着训练集中的 13 个示例图像，以便人类更容易视觉扫描类别。类别还按照 ImageNet 层次结构的拓扑顺序排序，将语义相似的概念放在列表中相邻的位置。例如，所有机动车辆相关的类别在列表中连续排列。最后，该界面基于 Web，因此很容易自然地滚动浏览类别，或通过文本搜索。

**尝试一下！** 我向所有人提供[标注界面](http://cs.stanford.edu/people/karpathy/ilsvrc/)，以便你也可以亲自尝试标注 ILSVRC 并得出自己的结论。这个版本与我们用于收集数据的版本相比有一些修改。我添加了两个按钮（显示答案和显示 Google 预测），当然，这个版本中显示的图像是*验证*图像，而不是测试集图像。GoogLeNet 验证集预测由 Google 团队慷慨提供。

### 一路上的障碍

**这很难。** 在我测试界面时，用 1000 个类别中选 5 个来标注图像的任务很快就变得极其困难，即使对一些在 ILSVRC 及其类别上工作了一段时间的实验室朋友来说也是如此。一开始我们以为可以把它放到 AMT 上。然后我们想到可以招募付费的本科生。然后我组织了一场只有我们实验室（专业标注人员）参与的密集标注派对。然后我开发了一个修改版的界面，使用 GoogLeNet 预测将类别数量从 1000 个缩减到大约 100 个。但仍然太难了——人们不断遗漏类别，错误率达到了 13-15% 的范围。最后我意识到，要想达到与 GoogLeNet 竞争的级别，最高效的方法是让我自己坐下来，经历痛苦漫长的训练过程和随后的仔细标注过程。

**花了很长时间。** 我最终在 500 张验证图像上训练，然后切换到 1500 张图像的测试集。标注速度大约每分钟一张，但随时间推移而下降。我只享受了前大约 200 张，剩下的我只是*为了科学*而做。（最后我们说服了另一位专业标注人员花几个小时进行标注，但他们只标注了 280 张图像，训练较少，只达到了大约 12% 的错误率。）标注时间分布强烈双峰：有些图像很容易识别，而有些图像（如细粒度品种的狗、鸟或猴子的图像）可能需要几分钟的集中努力。我变得非常擅长识别狗的品种。

**这是值得的。** 基于我处理的图像样本，GoogLeNet 的分类错误率为 6.8%（完整 10 万张图像测试集上的错误率为 6.7%）。我自己的最终错误率是 **5.1%**，大约好 1.7%。如果你在它们相等的零假设下计算统计显著性（即用 Z 检验比较两个比例），你会得到单侧 p 值 0.022。换句话说，基于相对常用的 0.05 阈值，这个结果在统计上是显著的。最后，我发现这段经历很有教育意义：看到这么多图像、问题和 ConvNet 预测后，你开始对失败模式形成一个非常好的模型。

> 我的错误率是 5.1%，而 GoogLeNet 的错误率是 6.8%。仍有差距需要缩小。

标注 ILSVRC 类别实际困难的代表性示例。啊，一只可爱的狗！你愿意花 5 分钟滚动浏览 120 种狗来猜它是什么品种吗？

### 错误分析

我们检查了人类和 GoogLeNet 的错误，以了解常见错误类型及其比较。以下分析和见解是专门从 GoogLeNet 预测中得出的，但我怀疑其他方法中也可能存在许多相同的错误。让我从我们的 [ILSVRC 论文](http://arxiv.org/abs/1409.0575)中复制粘贴分析内容：

**GoogLeNet 和人类都容易受到的错误类型：**

1. **多个物体。** GoogLeNet 和人类都在包含多个 ILSVRC 类别的图像（通常远多于五个）上挣扎，几乎没有线索表明哪个物体是图像的焦点。这个错误只在分类设置中存在，因为每张图像被约束为只有一个正确标签。总共，我们将 24 个（24%）GoogLeNet 错误和 12 个（16%）人类错误归因于这一类别。值得注意的是，人类在这种错误类型上可能略有优势，因为有时很容易识别图像中最突出的物体。
2. **错误的标注。** 我们发现 1500 张图像中约有 5 张（0.3%）在真实标签中被错误标注。这给人类和 GoogLeNet 带来了大致相等数量的错误。

**GoogLeNet 比人类更容易受到的错误类型：**

1. **物体太小或太细。** GoogLeNet 在识别图像中非常小或非常细的物体时挣扎，即使该物体是唯一存在的物体。例子包括一个人戴着太阳镜站立的图像、一个人手持羽毛笔的图像、或花茎上的一只小蚂蚁。我们估计大约 22 个（21%）GoogLeNet 错误属于这一类别，而人类错误中没有。换句话说，在我们的图像样本中，没有一张图像因人类无法识别非常小或非常细的物体而被错误标注。这种差异可以归因于人类可以非常有效地利用上下文和可供性来准确推断小物体的身份。
2. **图像滤镜。** 许多人用滤镜增强他们的照片，这会扭曲图像的对比度和颜色分布。我们发现 13 张（13%）GoogLeNet 错误分类的图像包含滤镜。因此，我们认为 GoogLeNet 对这些失真不太鲁棒。相比之下，人类错误中只有一张图像包含滤镜，但我们不认为错误的来源是滤镜。
3. **抽象表示。** 我们发现 GoogLeNet 在以抽象形式描绘感兴趣物体的图像上挣扎，例如 3D 渲染图像、绘画、素描、毛绒玩具或雕像。我们将大约 6 个（6%）GoogLeNet 错误归因于这种错误类型，并相信人类显著更鲁棒，在我们的样本中没有看到此类错误。
4. **其他来源。** 其他相对不常出现的错误来源包括物体部分的极端特写、非常规视角（如旋转图像）、能从阅读文字能力中显著受益的图像、严重遮挡的物体以及包含多张图像拼贴的图像。总的来说，我们发现人类对所有这类错误类型都更鲁棒。

代表性验证图像，突出常见错误来源。从左到右：包含多个物体的图像、极端特写和不典型视角的图像、带滤镜的图像、能从阅读文字能力中受益的图像、包含非常小和细长物体的图像、抽象表示的图像，以及 GoogLeNet 正确识别但人类会非常困难的细粒度图像示例。

**人类比 GoogLeNet 更容易受到的错误类型：**

1. **细粒度识别。** 我们发现人类在细粒度识别（例如狗、猴子、蛇、鸟）上明显更差，即使它们清晰可见。考虑到数据集中有超过 120 种狗。我们估计 28 个（37%）人类错误属于这一类别，而 GoogLeNet 错误中只有 7 个（7%）。
2. **类别不熟悉。** 标注者有时可能不知道作为选项存在的真实标签类别。当被指出是 ILSVRC 类别时，通常很清楚该标签适用于该图像。随着标注者对 ILSVRC 类别越来越熟悉，这些错误逐渐减少。大约 18 个（24%）人类错误属于这一类别。
3. **训练数据不足。** 标注者只看到每个类别名称下的 13 个示例图像。然而，13 张图像并不总能充分传达允许的类别变化。例如，如果"凯尔皮"的所有示例都是黑色毛发的狗，那么一只棕色狗可能被错误地排除。但如果列出了超过 13 张图像，就会清楚"凯尔皮"可能有棕色毛发。大约 4 个（5%）人类错误属于这一类别。

### 结论

我们调查了训练有素的人类标注者在多达 1500 张 ILSVRC 测试集图像样本上的表现。结果表明，训练有素的人类标注者能够以大约 1.7%（p = 0.022）的优势超越最佳模型（GoogLeNet）。

我们预计一些错误来源可能相对容易消除（例如对滤镜、旋转、拼贴的鲁棒性，有效推理多尺度等），而其他错误可能更加难以捉摸（例如识别物体的抽象表示）。另一方面，绝大多数人类错误来自细粒度类别和类别不熟悉。我们预计前者可以通过细粒度专家标注者显著减少，而后者可以通过更多练习和对 ILSVRC 类别的更大熟悉度来减少。

很明显，人类很快就只能通过付出大量努力、专业知识和时间来超越最先进的图像分类模型。

> "很明显，人类很快就只能通过付出大量努力、专业知识和时间来超越最先进的图像分类模型。"

至于我个人从这一周练习中的收获，我不得不说，从定性的角度来看，ConvNet 的性能给我留下了非常深刻的印象。除非图像表现出一些不规则或棘手的部分，ConvNet 都能自信而鲁棒地预测正确标签。如果你喜欢冒险，请亲自尝试[标注界面](http://cs.stanford.edu/people/karpathy/ilsvrc/)并得出你自己的结论。

更新（2015 年 2 月 14 日）：

现在已经有好几个报告的结果超越了我的 5.1% ImageNet 错误率。看到如此迅速的进步，我感到惊讶。同时，我认为我们应该记住以下几点：

> 人类准确率不是一个点。它存在于一个权衡曲线上。

我们以错误率来权衡人类的努力和专业知识：我是那个曲线上 5.1% 的一个点。我几乎没有训练和较少耐心的实验室伙伴是另一个点，错误率高达 15%。基于一些考虑我的确切错误类型并假设哪些可能比其他的更容易修复的计算，说一个由非常专注的专家标注者组成的集成可能会将错误率降至 3%，而约 2% 是一个乐观的错误率下限，这并非不合理。我知道这不像只有一个数字那么令人兴奋，但这是正确的思考方式。

---

*English original below:*

The results of the 2014 [ImageNet Large Scale Visual Recognition Challenge](http://www.image-net.org/challenges/LSVRC/2014/) (ILSVRC) were [published](http://www.image-net.org/challenges/LSVRC/2014/results) a few days ago. The New York Times [wrote about it](http://bits.blogs.nytimes.com/2014/08/18/computer-eyesight-gets-a-lot-more-accurate/) too. ILSVRC is one of the largest challenges in Computer Vision and every year teams compete to claim the state-of-the-art performance on the dataset. The challenge is based on a subset of the ImageNet dataset that was first collected by [Deng et al. 2009](http://www.image-net.org/papers/imagenet_cvpr09.pdf), and has been organized by our lab here at Stanford since 2010. This year, the challenge saw record participation with 50% more participants than last year, and records were shattered with staggering improvements in both classification and detection tasks.

> (My personal) **ILSVRC 2014 TLDR**: 50% more teams. 50% improved classification and detection. ConvNet ensembles all over the place. Google team wins.

Of course there's much more to it, and all details and takeaways will be discussed at length in Zurich, at the upcoming [ECCV 2014 workshop](http://image-net.org/challenges/LSVRC/2014/eccv2014) happening on September 12.

Additionally, we just (September 2nd) published an arXiv preprint describing the entire history of ILSVRC and a large amount of associated analysis, [check it out on arXiv](http://arxiv.org/abs/1409.0575). This post will zoom in on a portion of the paper that I contributed to (Section 6.4 Human accuracy on large-scale image classification) and describe some of its context.

#### ILSVRC Classification Task

For the purposes of this post, I would like to focus, in particular, on image classification because this task is the common denominator for many other Computer Vision tasks. The classification task is made up of 1.2 million images in the training set, each labeled with one of 1000 categories that cover a wide variety of objects, animals, scenes, and even some abstract geometric concepts such as *"hook"*, or *"spiral"*. The 100,000 test set images are released with the dataset, but the labels are withheld to prevent teams from overfitting on the test set. The teams have to predict 5 (out of 1000) classes and an image is considered to be correct if at least one of the predictions is the ground truth. The test set evaluation is carried out on our end by comparing the predictions to our own set of ground truth labels.

![](https://karpathy.github.io/assets/cnntsne.jpeg)

Example images from the classification task. Find full-scale images [here](http://cs.stanford.edu/people/karpathy/cnnembed/).

#### GoogLeNet's Impressive Performance

I was looking at the results about a week ago and became particularly intrigued by GoogleLeNet's winning submission for the classification task, which achieved a Hit@5 error rate of only 6.7% on the ILSVRC test set. I was relatively familiar with the scope and difficulty of the classification task: these are unconstrained internet images. They are a jungle of viewpoints, lighting conditions, and variations of all imaginable types. This begged the question: *How do humans compare?*

There are now several tasks in Computer Vision where the performance of our models is close to human, or even *superhuman*. Examples of these tasks include face verification, various medical imaging tasks, Chinese character recognition, etc. However, many of these tasks are fairly constrained in that they assume input images from a very particular distribution. For example, face verification models might assume as input only aligned, centered, and normalized images. In many ways, ImageNet is harder since the images come directly from the "jungle of the interwebs". Is it possible that our models are reaching human performance on such an unconstrained task?

#### Computing Human Accuracy

In short, I thought that the impressive performance by the winning team would only make sense if it was put in perspective with human accuracy. I was also in the unique position of being able to evaluate it (given that I share office space with ILSVRC organizers), so I set out to quantify the human accuracy and characterize the differences between human predictions with those of the winning model.

*Wait, isn't human accuracy 100%?* Thank you, good question. It's not, because the ILSVRC dataset was not labeled in the same way we are classifying it here. For example, to collect the images for the class "Border Terrier" the organizers searched the query on internet and retrieved a large collection of images. These were then filtered a bit with humans by asking them a binary "Is this a Border Terrier or not?". Whatever made it through became the "Border Terrier" class, and similar for all the other 1000 images. Therefore, the data was not collected in a discriminative but a binary manner, and is also subject to mistakes and inaccuracies. Some images can sometimes also contain multiple of the ILSVRC classes, etc.

*CIFAR-10 digression.* It's fun to note that about 4 years ago I performed a similar (but much quicker and less detailed) human classification accuracy analysis on CIFAR-10. This was back when the state of the art was at 77% by Adam Coates, and my own accuracy turned out to be 94%. I think the best ConvNets now get about 92%. The post about that can be found [here](https://karpathy.github.io/2011/04/27/manually-classifying-cifar10/). I never imagined I'd be doing the same for ImageNet a few years down the road:)

There's one issue to clarify on. You may ask: *But wait, the ImageNet test set labels were obtained from humans in the first place. Why go about re-labeling it all over again? Isn't human performance 0% by definition?* Kind of, but not really. It is important to keep in mind that ImageNet was annotated as a binary ask. For example, to collect images of the dog class "Kelpie", the query was submitted to search engines and then humans on Amazon Mechanical Turk were used for the binary task of filtering out the noise. The ILSVRC classification task, on the other hand, is 1000-way classification. It's not a binary task such as the one used to collect the data.

#### Labeling Interface

I developed a labeling interface that would help us evaluate the human performance. It looked similar to, but not identical, to the screenshot below:

![](https://karpathy.github.io/assets/ilsvrc1.png)

A crop of a screenshot of the [labeling interface](http://cs.stanford.edu/people/karpathy/ilsvrc/) for the ILSVRC validation data. Try it out for yourself.

The interface consisted of the test image on the left, and 1000 classes listed on the right. Each class was followed by 13 example images from the training set so that the categories were easier for a human to scan visually. The categories were also sorted in the topological order of the ImageNet hierarchy, which places semantically similar concepts nearby in the list. For example, all motor vehicle-related classes are arranged contiguously in the list. Finally, the interface is web-based so it is easy to naturally scroll through the classes, or search for them by text.

**Try it out!** I'm making the [the labeling interface](http://cs.stanford.edu/people/karpathy/ilsvrc/) available to everyone so that you can also try labeling ILSVRC yourselves and draw your own conclusions. There are a few modifications in this version from the one we used to collect the data. I added two buttons (Show answer, and Show google prediction), and of course, the images shown in this version are the *validation* images, not the test set images. The GoogLeNet validation set predictions were graciously provided by the Google team.

#### Roadblocks along the way

**It was hard.** As I beta-tested the interface, the task of labeling images with 5 out of 1000 categories quickly turned out to be extremely challenging, even for some friends in the lab who have been working on ILSVRC and its classes for a while. First we thought we would put it up on AMT. Then we thought we could recruit paid undergrads. Then I organized a labeling party of intense labeling effort only among the (expert labelers) in our lab. Then I developed a modified interface that used GoogLeNet predictions to prune the number of categories from 1000 to only about 100. It was still too hard - people kept missing categories and getting up to ranges of 13-15% error rates. In the end I realized that to get anywhere competitively close to GoogLeNet, it was most efficient if I sat down and went through the painfully long training process and the subsequent careful annotation process myself.

**It took a while.** I ended up training on 500 validation images and then switched to the test set of 1500 images. The labeling happened at a rate of about 1 per minute, but this decreased over time. I only enjoyed the first ~200, and the rest I only did *#forscience*. (In the end we convinced one more expert labeler to spend a few hours on the annotations, but they only got up to 280 images, with less training, and only got to about 12%). The labeling time distribution was strongly bimodal: Some images are easily recognized, while some images (such as those of fine-grained breeds of dogs, birds, or monkeys) can require multiple minutes of concentrated effort. I became very good at identifying breeds of dogs.

**It was worth it.** Based on the sample of images I worked on, the GoogLeNet classification error turned out to be 6.8% (the error on the full test set of 100,000 images is 6.7%). My own error in the end turned out to be **5.1%**, approximately 1.7% better. If you crunch through the statistical significance calculations (i.e. comparing the two proportions with a Z-test) under the null hypothesis of them being equal, you get a one-sided p-value of 0.022. In other words, the result is statistically significant based on a relatively commonly used threshold of 0.05. Lastly, I found the experience to be quite educational: After seeing so many images, issues, and ConvNet predictions you start to develop a really good model of the failure modes.

> My error turned out to be 5.1%, compared to GoogLeNet error of 6.8%. Still a bit of a gap to close (and more).

![](https://karpathy.github.io/assets/ilsvrc3.png)

Representative example of practical frustrations of labeling ILSVRC classes. Aww, a cute dog! Would you like to spend 5 minutes scrolling through 120 breeds of dog to guess what species it is?

#### Analysis of errors

We inspected both human and GoogLeNet errors to gain an understanding of common error types and how they compare. The analysis and insights below were derived specifically from GoogLeNet predictions, but I suspect that many of the same errors may be present in other methods. Let me copy paste the analysis from our [ILSVRC paper](http://arxiv.org/abs/1409.0575):

**Types of error that both GoogLeNet human are susceptible to:**

1. **Multiple objects.** Both GoogLeNet and humans struggle with images that contain multiple ILSVRC classes (usually many more than five), with little indication of which object is the focus of the image. This error is only present in the Classification setting, since every image is constrained to have exactly one correct label. In total, we attribute 24 (24%) of GoogLeNet errors and 12 (16%) of human errors to this category. It is worth noting that humans can have a slight advantage in this error type, since it can sometimes be easy to identify the most salient object in the image.
2. **Incorrect annotations.** We found that approximately 5 out of 1500 images (0.3%) were incorrectly annotated in the ground truth. This introduces an approximately equal number of errors for both humans and GoogLeNet.

**Types of error that GoogLeNet is more susceptible to than human:**

1. **Object small or thin.** GoogLeNet struggles with recognizing objects that are very small or thin in the image, even if that object is the only object present. Examples of this include an image of a standing person wearing sunglasses, a person holding a quill in their hand, or a small ant on a stem of a flower. We estimate that approximately 22 (21%) of GoogLeNet errors fall into this category, while none of the human errors do. In other words, in our sample of images, no image was mislabeled by a human because they were unable to identify a very small or thin object. This discrepancy can be attributed to the fact that a human can very effectively leverage context and affordances to accurately infer the identity of small objects (for example, a few barely visible feathers near person's hand as very likely belonging to a mostly occluded quill).
2. **Image filters.** Many people enhance their photos with filters that distort the contrast and color distributions of the image. We found that 13 (13%) of the images that GoogLeNet incorrectly classified contained a filter. Thus, we posit that GoogLeNet is not very robust to these distortions. In comparison, only one image among the human errors contained a filter, but we do not attribute the source of the error to the filter.
3. **Abstract representations.** We found that GoogLeNet struggles with images that depict objects of interest in an abstract form, such as 3D-rendered images, paintings, sketches, plush toys, or statues. An example is the abstract shape of a bow drawn with a light source in night photography, a 3D-rendered robotic scorpion, or a shadow on the ground, of a child on a swing. We attribute approximately 6 (6%) of GoogLeNet errors to this type of error and believe that humans are significantly more robust, with no such errors seen in our sample.
4. **Miscellaneous sources.** Additional sources of error that occur relatively infrequently include extreme closeups of parts of an object, unconventional viewpoints such as a rotated image, images that can significantly benefit from the ability to read text (e.g. a featureless container identifying itself as " *face powder* "), objects with heavy occlusions, and images that depict a collage of multiple images. In general, we found that humans are more robust to all of these types of error.
![](https://karpathy.github.io/assets/ilsvrc2.png)

Representative validation images that highlight common sources of error. For each image, we display the ground truth in blue, and top 5 predictions from GoogLeNet follow (red = wrong, green = right). GoogLeNet predictions on the validation set images were graciously provided by members of the GoogLeNet team. From left to right: Images that contain multiple objects, images of extreme closeups and uncharacteristic views, images with filters, images that significantly benefit from the ability to read text, images that contain very small and thin objects, images with abstract representations, and example of a fine-grained image that GoogLeNet correctly identifies but a human would have significant difficulty with.

**Types of error that human is more susceptible to than GoogLeNet:**

1. **Fine-grained recognition.** We found that humans are noticeably worse at fine-grained recognition (e.g. dogs, monkeys, snakes, birds), even when they are in clear view. To understand the difficulty, consider that there are more than 120 species of dogs in the dataset. We estimate that 28 (37%) of the human errors fall into this category, while only 7 (7%) of GoogLeNet erros do.
2. **Class unawareness.** The annotator may sometimes be unaware of the ground truth class present as a label option. When pointed out as an ILSVRC class, it is usually clear that the label applies to the image. These errors get progressively less frequent as the annotator becomes more familiar with ILSVRC classes. Approximately 18 (24%) of the human errors fall into this category.
3. **Insufficient training data.** Recall that the annotator is only presented with 13 examples of a class under every category name. However, 13 images are not always enough to adequately convey the allowed class variations. For example, a brown dog can be incorrectly dismissed as a " *Kelpie* " if all examples of a " *Kelpie* " feature a dog with black coat. However, if more than 13 images were listed it would have become clear that a " *Kelpie* " may have a brown coat. Approximately 4 (5%) of human errors fall into this category.

#### Conclusions

We investigated the performance of trained human annotators on a sample of up to 1500 ILSVRC test set images. Our results indicate that a trained human annotator is capable of outperforming the best model (GoogLeNet) by approximately 1.7% (p = 0.022).

We expect that some sources of error may be relatively easily eliminated (e.g. robustness to filters, rotations, collages, effectively reasoning over multiple scales), while others may prove more elusive (e.g. identifying abstract representations of objects). On the hand, a large majority of human errors come from fine-grained categories and class unawareness. We expect that the former can be significantly reduced with fine-grained expert annotators, while the latter could be reduced with more practice and greater familiarity with ILSVRC classes.

It is clear that humans will soon only be able to outperform state of the art image classification models by use of significant effort, expertise, and time. One interesting follow-up question for future investigation is how computer-level accuracy compares with human-level accuracy on more complex image understanding tasks.

> "It is clear that humans will soon only be able to outperform state of the art image classification models by use of significant effort, expertise, and time."

As for my personal take-away from this week-long exercise, I have to say that, qualitatively, I was very impressed with the ConvNet performance. Unless the image exhibits some irregularity or tricky parts, the ConvNet confidently and robustly predicts the correct label. If you're feeling adventurous, try out [the labeling interface](http://cs.stanford.edu/people/karpathy/ilsvrc/) for yourself and draw your own conclusions. I can promise that you'll gain interesting qualitative insights into where state-of-the-art Computer Vision works, where it fails, and how.

EDIT: additional discussions:

- [Pierre's Google+](https://plus.google.com/u/0/+PierreSermanet/posts/6wZYMuXo8PU)
- [Reddit /r/MachineLearning](http://www.reddit.com/r/MachineLearning/comments/2fg0va/what_i_learned_from_competing_against_a_convnet/)

UPDATE:

- [ImageNet workshop page](http://image-net.org/challenges/LSVRC/2014/eccv2014) now has links to many of the teams' slides and videos.
- [GoogLeNet paper](http://arxiv.org/abs/1409.4842) on arXiv describes the details of their architecutre.

UPDATE2 (14 Feb 2015):

There have now been several reported results that surpass my 5.1% error on ImageNet. I'm astonished to see such rapid progress. At the same time, I think we should keep in mind the following:

> Human accuracy is not a point. It lives on a tradeoff curve.

We trade off human effort and expertise with the error rate: I am one point on that curve with 5.1%. My labmates with almost no training and less patience are another point, with even up to 15% error. And based on some calculations that consider my exact error types and hypothesizing which ones may be easier to fix than others, it's not unreasonable to suggest that an ensemble of very dedicated expert human labelers might push this down to 3%, with about 2% being an optimistic error rate lower bound. I know it's not as exciting as having a single number, but it's the right way of thinking about it. See more details in my recent [Google+ post](https://plus.google.com/+AndrejKarpathy/posts/dwDNcBuWTWf).