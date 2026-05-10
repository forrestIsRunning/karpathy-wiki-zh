你可能听说过卷积网络（Convolutional Networks）在实践中非常有效，适用于广泛的视觉识别问题。你可能也读到过声称接近*"人类水平性能"*的文章和论文。这有很多注意事项（例如看我关于[人类准确率不是一个点，它存在于一个权衡曲线](https://plus.google.com/+AndrejKarpathy/posts/dwDNcBuWTWf)的 G+ 帖子），但这不是本文的重点。我确实认为这些系统现在在许多视觉识别任务上表现非常出色，尤其是那些可以表述为简单分类的任务。

然而，第二组看似令人费解的结果出现了，带来了一个明显的矛盾。我指的是有几个人注意到，可以将一张最先进的卷积网络认为是某个类别（例如"熊猫"）的图像，以人类眼睛几乎无法察觉的方式改变它，使得卷积网络突然将该图像分类为任何其他选择的类别（例如"长臂猿"）。我们说我们*打破*或*愚弄*了 ConvNet。请看下图：

来自 Goodfellow 等人的论文 [Explaining and Harnessing Adversarial Examples](http://arxiv.org/abs/1412.6572) 的图片。

这个话题最近引起了关注，始于去年 Szegedy 等人的 [Intriguing properties of neural networks](http://arxiv.org/abs/1312.6199)。他们有一组非常相似的图像：

取一张正确分类的图像（两列中的左图），添加一个微小的扰动（中间），用得到的图像（右图）来愚弄 ConvNet。

随后，一组非常相关的结果来自 Nguyen 等人的 [Deep Neural Networks are Easily Fooled: High Confidence Predictions for Unrecognizable Images](http://arxiv.org/abs/1412.1897)。他们不是从正确分类的图像开始并愚弄 ConvNet，而是有更多从噪声开始的相同过程的例子（从而让 ConvNet 自信地将无法理解的噪声模式分类为某个类别），或者进化出新的看起来滑稽的图像，ConvNet 对其过于确信：

这些图像被卷积网络以 >99.6% 的置信度分类为所示类别。

我应快速指出，这些结果对计算机视觉来说并非全新，有些人甚至在更早的特征（如 HOG 特征）上也观察到了同样的问题。详见 [Exploring the Representation Capabilities of the HOG Descriptor](http://ieeexplore.ieee.org/xpl/articleDetails.jsp?tp=&arnumber=6130416&contentType=Conference+Publications&queryText%3Dexploring+representation+capabilities+of+HOG)。

结论似乎是，我们可以通过添加微小的、不可察觉的噪声模式，将任何任意图像分类为我们想要的任何类别。更糟的是，研究发现相当一部分愚弄图像可以在不同的卷积网络之间**泛化**，所以这不是新图像的某种脆弱性质或模型的某种过拟合特性。引入的噪声类型似乎有某种更普遍的属性，可以愚弄许多其他模型。从某种意义上说，谈论*愚弄子空间*比谈论*愚弄图像*要准确得多。后者错误地使它们看起来像是超高维图像空间中的微小点，类似于实数轴上的有理数，而实际上它们更像是完整的区间。当然，这项工作引发了安全担忧，因为对手可以在自己的电脑上生成任何类别的愚弄图像，并怀着恶意将其上传到某个服务，有一定概率会愚弄服务器端的模型（例如绕过不当内容过滤器）。

> 发生了什么？

这些结果既有趣又令人担忧，但也导致外行人的大量困惑。整篇文章最重要的一点如下：

**这些结果并非图像或 ConvNet 所特有，也不是深度学习中的"缺陷"**。很多这些结果是在图像上运行的 ConvNet 上报告的，因为图片看起来有趣，而且 ConvNet 是最先进的，但实际上核心缺陷延伸到许多其他领域（例如语音识别系统），最重要的是，也延伸到简单的、浅层的、老式的线性分类器（Softmax 分类器或线性支持向量机等）。这在 Goodfellow 等人的 [Explaining and Harnessing Adversarial Examples](http://arxiv.org/abs/1412.6572) 中被指出并阐明。我们将进行与该论文中非常相似的几个实验，并看到实际上正是这种*线性*本质导致了问题。正因为深度学习模型使用线性函数来构建架构，它们继承了这一缺陷。但深度学习本身并不是问题的原因。事实上，深度学习为解决方案提供了切实的希望，因为我们可以利用组合函数的灵活性来设计更鲁棒的架构或目标函数。

### 愚弄方法如何工作

ConvNet 表达了从像素值到类别得分的一个可微函数。例如，一个 ConvNet 可能接收一张 227x227 的图像，通过一个复杂的函数（由数百万参数参数化）将这约 10 万个数字转换为 1000 个数字，我们将其解释为 1000 个类别的置信度（例如 ImageNet 的类别）。

这个 ConvNet 接收一张香蕉图像，并应用一个函数将其转换为类别得分（这里显示了 4 个类别）。该函数包括几轮卷积（其中滤波器条目是参数）和几个矩阵乘法（其中矩阵元素是参数）。一个典型的 ConvNet 可能有约 1 亿个参数。

我们通过重复采样数据、计算参数梯度和执行参数更新的过程来训练 ConvNet。也就是说，假设我们向 ConvNet 输入一张香蕉图像，并计算 ConvNet 分配给这张图像的 1000 个类别的得分。然后我们对模型中的每一个参数问以下问题：

> 正常的 ConvNet 训练："当我微调这个参数时，正确类别的得分会发生什么变化？"

当然，这种*微调影响*就是梯度。例如，ConvNet 某层某个滤波器中的某个参数可能会得到 -3.0 的梯度。这意味着将该参数略微增加（例如 0.0001）会对香蕉得分产生*负面*影响（由于负号）；在这种情况下，我们预计香蕉得分会*下降*大约 0.0003。通常我们取这个梯度并用它来执行**参数更新**，将模型中的每个参数向*正确*方向微调一点点，以提高香蕉得分。这些参数更新协同工作，略微提高那张香蕉图像的香蕉类别得分。然后我们在训练数据的所有图像上反复重复这个过程。

注意这里的工作方式：我们固定输入图像，微调模型参数以提高我们想要的任何类别的得分。事实证明，我们可以很容易地将这个过程反过来，创建愚弄图像。（实际上，完全不需要对 ConvNet 代码库做任何更改。）也就是说，我们将固定模型参数，而是计算输入图像中所有像素相对于我们可能想要的任何类别的梯度。例如，我们可以问：

> 创建愚弄图像："当我微调这个像素时，（你想要的任何类别的）得分会发生什么变化？"

我们像以前一样用反向传播计算梯度，然后执行**图像更新**而不是参数更新，最终结果是我们提高任何我们想要的类别的得分。例如，我们可以拿香蕉图像，根据该图像相对于猫类别的梯度来微调每个像素。这会使图像发生微小变化，但*猫*的得分会增加。有些违反直觉的是，事实证明你不需要对图像改变太多，就能将图像从被正确分类为香蕉，切换为被分类为其他任何东西（例如猫）。

简而言之，要创建愚弄图像，我们从任何我们想要的图像开始（一张真实的图像，甚至一个噪声模式），然后用反向传播计算图像像素相对于任何类别得分的梯度，并沿着它推进。我们可以重复这个过程几次，但不必如此。你可以将这里的反向传播解释为使用动态规划来计算对输入最具破坏性的局部扰动。注意，如果你能访问 ConvNet 的参数，这个过程非常高效且几乎不花时间（反向传播很快），但即使你不能访问参数，只能访问最终的类别得分，也可以做到。在这种情况下，可以用数值方法计算数据梯度，或使用其他局部随机搜索策略等。注意，由于后一种方法，甚至不可微分类器（例如随机森林）也不安全（但我还没看到有人用实验证实这一点）。

### 在 ImageNet 上愚弄线性分类器

正如我之前提到的（以及在 [Goodfellow 等人](http://arxiv.org/abs/1412.6572)中更详细描述的），正是线性函数的使用使我们的模型容易受到攻击。当然，ConvNet 并不表达从图像到类别得分的线性函数；它们是一个复杂的深度学习模型，表达高度非线性的函数。然而，构成 ConvNet 的组件*是*线性的：滤波器与其输入的卷积是线性操作，矩阵乘法也是线性函数。

所以这里有一个有趣的实验。让我们忘掉 ConvNet——就核心缺陷而言，它们是分散注意力的过度杀伤。相反，让我们愚弄一个线性分类器，并继续在图像上打破模型的主题，因为它们看起来有趣。

以下是设置：

- 获取 ImageNet 中的 120 万张图像
- 将它们调整为 64x64（全尺寸图像训练时间更长）
- 使用 [Caffe](http://caffe.berkeleyvision.org/) 训练一个线性分类器（例如 Softmax）。换句话说，我们直接从数据通过一个全连接层到达分类器。

*题外话：技术有趣的部分。* 实际操作中的有趣之处在于，标准的 AlexNet 式 ConvNet 超参数当然完全不适用。例如，通常你会使用 0.0005 左右的正则化和 0.01 的学习率，以及从标准差 0.01 的高斯分布中采样的初始化。如果你以前在这种高维输入上训练过线性分类器，你会知道学习率可能需要低得多，regularization 大得多，0.01 标准差的初始化可能不适用。确实，用默认超参数开始 Caffe 训练会得到约 80 的起始损失，这立即告诉你初始化完全不正常（初始 ImageNet 损失应该大约是 7.0，即 -log(1/1000)）。我将高斯初始化的标准差降到 0.0001，得到了合理的起始损失。但随后损失立即爆炸，这告诉学习率太高了——我不得不一直降到约 1e-7。最后，使用 0.0005 的权重衰减对于 12K 输入来说几乎可以忽略——我不得不将其提高到 100 才开始得到看起来不太过拟合的合理权重。做一个神经网络实践者很有趣。

图像像素上的线性分类器意味着每个类别得分被计算为所有图像像素（拉伸为大列向量）与一个可学习的权重向量之间的点积，每个类别一个权重向量。输入图像尺寸为 64x64x3 和 1000 个 ImageNet 类别，因此我们有 64x64x3x1000 = 1230 万个权重，以及 1000 个偏置。在 K40 GPU 上在 ImageNet 上训练这些参数只需要几十分钟。然后我们可以通过将学习到的权重重塑为图像来可视化它们：

几个 ImageNet 类别的示例线性分类器。每个类别的得分通过可视化权重与图像之间的点积计算。因此，权重可以被视为模板：图像显示了分类器在寻找什么。例如，青苹果是绿色的，所以线性分类器在所有空间位置上，在绿色通道中有正权重，在蓝色和红色通道中有负权重。因此，它有效地统计了中间绿色东西的数量。你也可以查看所有 ImageNet 类别的[学习模板](http://cs.stanford.edu/people/karpathy/linear_imagenet/)。

顺便提一下，我以前没见过任何人报告 ImageNet 上的线性分类准确率，但结果显示在 ImageNet 上大约是 3.0% 的 top-1 准确率（和大约 10% 的 top-5）。我没有做完全彻底的超参数搜索，但做了几轮手动二分搜索。

现在我们训练好了模型参数，可以开始生成愚弄图像了。在线性分类器的情况下，这变得非常简单，不需要反向传播。这是因为当你的得分函数是点积 $s = w^Tx$ 时，图像 $x$ 上的梯度就是 $\nabla_x s = w$。也就是说，我们拿一张要开始的图像，如果想愚弄模型使其认为它是某个其他类别（例如金鱼），我们必须取对应于目标类别的权重，并将这些权重的一部分加到图像上：

愚弄线性分类器：起始图像（左）被分类为狐。这是错误的，但你能对线性分类器期望什么呢？然而，如果我们向图像添加一小部分"金鱼"权重（上行中间），分类器突然确信它看到的是金鱼，置信度很高。我们也可以改为使用校车模板来扭曲它。类似的图可以在 [Goodfellow 等人](http://arxiv.org/abs/1412.6572)的图 2 中找到。

我们也可以从随机噪声开始达到同样的效果：

同样的过程，但从随机图像开始。

当然，这些例子不如使用 ConvNet 的那些有冲击力，因为 ConvNet 提供了最先进的性能，而线性分类器勉强达到 3% 的准确率，但这说明了即使是简单的、浅层的函数，仍然可以以难以察觉的方式操纵输入并获得几乎任意结果。

**正则化。** 有一个关于正则化强度的微妙评论。在我上面的实验中，增加正则化强度得到了更漂亮、更平滑和更分散的权重，但在验证数据上的泛化能力比一些最佳分类器（表现出更多噪声模式）更差。例如，我展示的漂亮平滑模板只达到了 1.6% 的准确率。达到 3.0% 准确率的最佳模型有更噪声的权重。具有非常低正则化的另一个模型达到 2.8%，其愚弄图像几乎无法区分，却产生了 100% 的错误类别置信度。具体来说：

- 高正则化产生更平滑的模板，但最终性能开始下降。然而，它对愚弄更具抵抗性。（愚弄图像看起来与原始图像有明显不同）
- 低正则化产生更多噪声的模板，但似乎比全平滑模板效果更好。它对愚弄的抵抗性较差。

直观地说，更高的正则化导致更小的权重，这意味着必须更显著地改变图像才能将得分改变一定量。这个结论是否以及如何转化到更深的模型上并不明显。

较低正则化（导致更噪声的类别权重）的线性分类器更容易被愚弄（上）。较高正则化产生更分散的滤波器，更难被愚弄（下）。也就是说，更难达到非常自信的错误答案（然而，权重如此之小，也很难达到非常自信的正确答案）。要将标签翻转为错误类别，需要更明显的视觉扰动。有点矛盾的是，具有噪声权重的模型（上）在验证数据上表现更好（2.6% vs. 1.4% 准确率）。

### 玩具示例

我们可以通过将问题压缩为展示该问题的最小玩具示例来更详细地理解这个过程。假设我们训练一个二分类逻辑回归，其中我们将类别 1 的概率定义为 $P(y = 1 \mid x; w,b) = \sigma(w^Tx + b)$，其中 $\sigma(z) = 1/(1+e^{-z})$ 是 sigmoid 函数。因此，这个分类器判定输入类别为 1 的条件是 $s > 0$。进一步假设我们有如下设置：

```
x = [2, -1, 3, -2, 2, 2, 1, -4, 5, 1] // 输入
w = [-1, -1, 1, -1, 1, -1, 1, 1, -1, 1] // 权重向量
```

点积结果为 -3。因此，类别 1 的概率为 `1/(1+e^(-(-3))) = 0.0474`。换句话说，分类器有 95% 的把握认为这是类别 0。现在我们试图愚弄分类器。也就是说，我们想找到一个微小的变化，使得得分大大提高。由于得分通过点积计算，稍加思考就清楚应该做什么：在每个权重为正的维度上，我们想稍微增加输入；相反，在每个权重为负的维度上，我们想稍微降低输入。换句话说，对抗性的 `xad` 可能是：

```
xad = [1.5, -1.5, 3.5, -2.5, 2.5, 1.5, 1.5, -3.5, 4.5, 1.5]
```

再次计算点积，我们看到得分突然变成了 2。这并不奇怪：有 10 个维度，我们在每个维度上将输入调整了 0.5，使得我们在每个维度上*获得* 0.5，总共增加了 5 分，从 -3 提高到 2。现在类别 1 的概率是 `1/(1+e^(-2)) = 0.88`。也就是说，我们将原始 `x` 调整了一小点，就将类别 1 的概率从 5% 提高到了 88%！而且，注意在这个例子中输入只有 10 个维度，但图像可能有成千上万个维度，所以你可以在所有维度上做微小的改变，它们以精确的最坏方式累加，使任何你想要的类别的得分爆炸。

### 结论

更多相关的实验可以在 Goodfellow 等人的 [Explaining and Harnessing Adversarial Examples](http://arxiv.org/abs/1412.6572) 中找到。这篇论文是关于此主题的必读材料。它是第一个阐明和指出线性函数缺陷的论文，并更一般地论证了易于训练的模型（例如使用线性函数的模型）与抵抗对抗性扰动的模型之间存在张力。

作为本文的结束语，要点是 ConvNet 在实践中仍然工作得很好。不幸的是，它们的能力似乎相对局限于数据流形附近包含自然图像和分布的小区域，而一旦我们通过反向传播计算的噪声模式人为地将图像推离这个流形，我们就会进入图像空间中一切皆不可预测的区域，网络中的线性函数在那里诱导出大的愚弄输入子空间。

乐观地看，人们可能希望 ConvNet 在训练数据之外的区域产生全模糊的概率，但普通的目标函数（例如平均交叉熵损失）中没有部分明确强制这一约束。确实，这些空间区域中的类别得分似乎到处都是，更糟的是，通过引入背景类并在训练期间迭代添加愚弄图像作为新的*背景*类来修补这个问题的直接尝试，在缓解问题上并不有效。

要解决这个问题，我们需要改变我们的目标函数、前向函数形式，甚至优化模型的方式。但据我所知，我们还没有找到很好的候选方案。未完待续。

#### 延伸阅读

- Ian Goodfellow 在 [RE.WORK 深度学习峰会 2015](https://www.youtube.com/watch?v=Pq4A2mPCB0Y) 上就此工作做了演讲
- 你可以在 [CS231n 作业 #3 IPython Notebook](http://cs231n.github.io/assignment3/) 中愚弄 ConvNet
- 本次实验的 [IPython Notebook](http://cs.stanford.edu/people/karpathy/break_linear_classifier.ipynb)。还有我的 [Caffe 线性分类器](http://cs.stanford.edu/people/karpathy/caffe_linear_imagenet.zip) 配置文件

---

*English original below:*

You've probably heard that Convolutional Networks work very well in practice and across a wide range of visual recognition problems. You may have also read articles and papers that claim to reach a near *"human-level performance"*. There are all kinds of caveats to that (e.g. see my G+ post on [Human Accuracy is not a point, it lives on a tradeoff curve](https://plus.google.com/+AndrejKarpathy/posts/dwDNcBuWTWf)), but that is not the point of this post. I do think that these systems now work extremely well across many visual recognition tasks, especially ones that can be posed as simple classification.

Yet, a second group of seemingly baffling results has emerged that brings up an apparent contradiction. I'm referring to several people who have noticed that it is possible to take an image that a state-of-the-art Convolutional Network thinks is one class (e.g. "panda"), and it is possible to change it almost imperceptibly to the human eye in such a way that the Convolutional Network suddenly classifies the image as any other class of choice (e.g. "gibbon"). We say that we *break*, or *fool* ConvNets. See the image below for an illustration:

![](https://karpathy.github.io/assets/break/breakconv.png)

Figure from [Explaining and Harnessing Adversarial Examples](http://arxiv.org/abs/1412.6572) by Goodfellow et al.

This topic has recently gained attention starting with [Intriguing properties of neural networks](http://arxiv.org/abs/1312.6199) by Szegedy et al. last year. They had a very similar set of images:

![](https://karpathy.github.io/assets/break/szegedy.jpeg)

Take a correctly classified image (left image in both columns), and add a tiny distortion (middle) to fool the ConvNet with the resulting image (right).

And a set of very closely related results was later followed by [Deep Neural Networks are Easily Fooled: High Confidence Predictions for Unrecognizable Images](http://arxiv.org/abs/1412.1897) by Nguyen et al. Instead of starting with correctly-classified images and fooling the ConvNet, they had many more examples of performing the same process starting from noise (and hence making the ConvNet confidently classify an incomprehensible noise pattern as some class), or evolving new funny-looking images that the ConvNet is slightly too certain about:

![](https://karpathy.github.io/assets/break/break1.jpeg) ![](https://karpathy.github.io/assets/break/break2.jpeg)

These images are classified with >99.6% confidence as the shown class by a Convolutional Network.

I should make the point quickly that these results are not completely new to Computer Vision, and that some have observed the same problems even with our older features, e.g. HOG features. See [Exploring the Representation Capabilities of the HOG Descriptor](http://ieeexplore.ieee.org/xpl/articleDetails.jsp?tp=&arnumber=6130416&contentType=Conference+Publications&queryText%3Dexploring+representation+capabilities+of+HOG) for details.

The conclusion seems to be that we can take any arbitrary image and classify it as whatever class we want by adding tiny, imperceptible noise patterns. Worse, it was found that a reasonable fraction of fooling images **generalize** across different Convolutional Networks, so this isn't some kind of fragile property of the new image or some overfitting property of the model. There's something more general about the type of introduced noise that seems to fool many other models. In some sense, it is much more accurate to speak about *fooling subspaces* rather than *fooling images*. The latter erroneously makes them seem like tiny points in the super-high-dimensional image space, perhaps similar to rational numbers along the real numbers, when instead they are better thought of as entire intervals. Of course, this work raises security concerns because an adversary could conceivably generate a fooling image of any class on their own computer and upload it to some service with a malicious intent, with a non-zero probability of it fooling the server-side model (e.g. circumventing racy filters).

> What is going on?

These results are interesting and worrying, but they have also led to a good amount of confusion among laymen. The most important point of this entire post is the following:

**These results are not specific to images, ConvNets, and they are also not a "flaw" in Deep Learning**. A lot of these results were reported with ConvNets running on images because pictures are fun to look at and ConvNets are state-of-the-art, but in fact the core flaw extends to many other domains (e.g. speech recognition systems), and most importantly, also to simple, shallow, good old-fashioned Linear Classifiers (Softmax classifier, or Linear Support Vector Machines, etc.). This was pointed out and articulated in [Explaining and Harnessing Adversarial Examples](http://arxiv.org/abs/1412.6572) by Goodfellow et al. We'll carry out a few experiments very similar to the ones presented in this paper, and see that it is in fact this *linear* nature that is problematic. And because Deep Learning models use linear functions to build up the architecture, they inherit their flaw. However, Deep Learning by itself is not the cause of the issue. In fact, Deep Learning offers tangible hope for a solution, since we can use all the wiggle of composed functions to design more resistant architectures or objectives.

### How fooling methods work

ConvNets express a differentiable function from the pixel values to class scores. For example, a ConvNet might take a 227x227 image and transforms these ~100,000 numbers through a wiggly function (parameterized by several million parameters) to 1000 numbers that we interpret as the confidences for 1000 classes (e.g. the classes of ImageNet).

![](https://karpathy.github.io/assets/break/banana.jpeg)

This ConvNet takes the image of a banana and applies a function to it to transform it to class scores (here 4 classes are shown). The function consists of several rounds of convolutions where the filter entries are parameters, and a few matrix multiplications, where the elements of the matrices are parameters. A typical ConvNet might have ~100 million parameters.

We train a ConvNet with repeated process of sampling data, calculating the parameter gradients and performing a parameter update. That is, suppose we feed the ConvNet an image of a banana and compute the 1000 scores for the classes that the ConvNet assigns to this image. We then and ask the following question for every single parameter in the model:

> Normal ConvNet training: "What happens to the score of the correct class when I wiggle this parameter?"

This *wiggle influence*, of course, is just the gradient. For example, some parameter in some filter in some layer of the ConvNet might get the gradient of -3.0 computed during backpropagation. That means that increasing this parameter by a tiny amount, e.g. 0.0001, would have a *negative* influence on the banana score (due to the negative sign); In this case, we'd expect the banana score to *decrease* by approximately 0.0003. Normally we take this gradient and use it to perform a **parameter update**, which wiggles every parameter in the model a tiny amount in the *correct* direction, to increase the banana score. These parameter updates hence work in concert to slightly increase the score of the banana class for that one banana image (e.g. the banana score could go up from 30% to 34% or something). We then repeat this over and over on all images in the training data.

Notice how this worked: we held the input image fixed, and we wiggled the model parameters to increase the score of whatever class we wanted (e.g. banana class). It turns out that we can easily flip this process around to create fooling images. (In practice in fact, absolutely no changes to a ConvNet code base are required.) That is, we will hold the model parameters fixed, and instead we're computing the gradient of all pixels in the input image on any class we might desire. For example, we can ask:

> Creating fooling images: "What happens to the score of (whatever class you want) when I wiggle this pixel?"

We compute the gradient just as before with backpropagation, and then we can perform an **image update** instead of a parameter update, with the end result being that we increase the score of whatever class we want. E.g. we can take the banana image and wiggle every pixel according to the gradient of that image on the cat class. This would change the image a tiny amount, but the score of *cat* would now increase. Somewhat unintuitively, it turns out that you don't have to change the image too much to toggle the image from being classified correctly as a banana, to being classified as anything else (e.g. cat).

In short, to create a fooling image we start from whatever image we want (an actual image, or even a noise pattern), and then use backpropagation to compute the gradient of the image pixels on any class score, and nudge it along. We may, but do not have to, repeat the process a few times. You can interpret backpropagation in this setting as using dynamic programming to compute the most damaging local perturbation to the input. Note that this process is very efficient and takes negligible time if you have access to the parameters of the ConvNet (backprop is fast), but it is possible to do this even if you do not have access to the parameters but only to the class scores at the end. In this case, it is possible to compute the data gradient numerically, or to to use other local stochastic search strategies, etc. Note that due to the latter approach, even non-differentiable classifiers (e.g. Random Forests) are not safe (but I haven't seen anyone empirically confirm this yet).

### Fooling a Linear Classifier on ImageNet

As I mentioned before (and as described in more detail in [Goodfellow et al.](http://arxiv.org/abs/1412.6572)), it is the use of linear functions that makes our models susceptible for an attack. ConvNets, of course, do not express a linear function from images to class scores; They are a complex Deep Learning model that expresses a highly non-linear function. However, the components that make up a ConvNet *are* linear: Convolution of a filter with its input is a linear operation (we are sliding a filter through the input and computing dot products - a linear operation), and matrix multiplications are also a linear function.

So here's a fun experiment we'll do. Lets forget about ConvNets - they are a distracting overkill as far as the core flaw goes. Instead, lets fool a linear classifier and lets also keep with the theme of breaking models on images because they are fun to look at.

Here is the setup:

- Take 1.2 million images in ImageNet
- Resize them to 64x64 (full-sized images would train longer)
- use [Caffe](http://caffe.berkeleyvision.org/) to train a Linear Classifier (e.g. Softmax). In other words we're going straight from data to the classifier with a single fully-connected layer.

*Digression: Technical fun parts.* The fun part in actually doing this is that the standard AlexNetty ConvNet hyperparameters are of course completely inadequate. For example, normally you'd use weight decay of 0.0005 or so and learning rate of 0.01, and gaussian initialization drawn from a gaussian of 0.01 std. If you've trained linear classifiers before on this type of high-dimensional input (64x64x3 ~= 12K numbers), you'll know that your learning rate will probably have to be much lower, the regularization much larger, and initialization of 0.01 std will probably be inadequate. Indeed, starting Caffe training with default hyperparameters gives a starting loss of about 80, which right away tells you that the initialization is completely out of whack (initial ImageNet loss should be ballpark 7.0, which is -log(1/1000)). I scaled it down to 0.0001 std for Gaussian init which gives sensible starting loss. But then the loss right away explodes which tells you that the learning rate is way too high - I had to scale it all the way down to about 1e-7. Lastly, a weight decay of 0.0005 will give almost negligible regularization loss with 12K inputs - I had to scale it up to 100 to start getting reasonably-looking weights that aren't super-overfitted noise blobs. It's fun being a Neural Networks practitioner.

A linear classifier over image pixels implies that every class score is computed as a dot product between all the image pixels (stretched as a large column) and a learnable weight vector, one for each class. With input images of size 64x64x3 and 1000 ImageNet classes we therefore have 64x64x3x1000 = 12.3 million weights (beefy linear model!), and 1000 biases. Training these parameters on ImageNet with a K40 GPU takes only a few tens of minutes. We can then visualize each of the learned weights by reshaping them as images:

![](https://karpathy.github.io/assets/break/templates.jpeg)

Example linear classifiers for a few ImageNet classes. Each class' score is computed by taking a dot product between the visualized weights and the image. Hence, the weights can be thought of as a template: the images show what the classifier is looking for. For example, Granny Smith apples are green, so the linear classifier has positive weights in the green color channel and negative weights in blue and red channels, across all spatial positions. It is hence effectively counting the amount of green stuff in the middle. You can also see the learned [templates for all imagenet classes for fun.](http://cs.stanford.edu/people/karpathy/linear_imagenet/)

By the way, I haven't seen anyone report linear classification accuracy on ImageNet before, but it turns out to be about 3.0% top-1 accuracy (and about 10% top-5) on ImageNet. I haven't done a completely exhaustive hyperparameter sweep but I did a few rounds of manual binary search.

Now that we've trained the model parameters we can start to produce fooling images. This turns out to be quite trivial in the case of linear classifiers and no backpropagation is required. This is because when your score function is a dot product $s = w^Tx$, then the gradient on the image $x$ is simply $\nabla_x s = w$. That is, we take an image we would like to start out with, and then if we wanted to fool the model into thinking that it is some other class (e.g. goldfish), we have to take the weights corresponding to the desired class, and add some fraction of those weights to the image:

![](https://karpathy.github.io/assets/break/fool2.jpeg) ![](https://karpathy.github.io/assets/break/fool1.jpeg) ![](https://karpathy.github.io/assets/break/fish.jpeg)

Fooled linear classifier: The starting image (left) is classified as a kit fox. That's incorrect, but then what can you expect from a linear classifier? However, if we add a small amount "goldfish" weights to the image (top row, middle), suddenly the classifier is convinced that it's looking at one with high confidence. We can distort it with the school bus template instead if we wanted to. Similar figures (but on the MNIST digits dataset) can be seen in Figure 2 of [Goodfellow et al.](http://arxiv.org/abs/1412.6572)

We can also start from random noise and achieve the same effect:

Same process but starting with a random image.

Of course, these examples are not as impactful as the ones that use a ConvNet because the ConvNet gives state of the art performance while a linear classifier barely gets to 3% accuracy, but it illustrates the point that even with a simple, shallow function it is still possible to play around with the input in imperceptible ways and get almost arbitrary results.

**Regularization**. There is one subtle comment to make regarding regularization strength. In my experiments above, increasing the regularization strength gave nicer, smoother and more diffuse weights but generalized to validation data *worse* than some of my best classifiers that displayed more noisy patterns. For example, the nice and smooth templates I've shown only achieve 1.6% accuracy. My best model that achieves 3.0% accuracy has noisier weights (as seen in the middle column of the fooling images). Another model with very low regularization reaches 2.8% and its fooling images are virtually indistinguishable yet produce 100% confidences in the wrong class. In particular:

- High regularization gives smoother templates, but at some point starts to works worse. However, it is more resistant to fooling. (The fooling images look noticeably different from their original)
- Low regularization gives more noisy templates but seems to work better that all-smooth templates. It is less resistant to fooling.

Intuitively, it seems that higher regularization leads to smaller weights, which means that one must change the image more dramatically to change the score by some amount. It's not immediately obvious if and how this conclusion translates to deeper models.

![](https://karpathy.github.io/assets/break/rapeseed.jpeg) ![](https://karpathy.github.io/assets/break/rapeseed2.jpeg)

Linear classifier with lower regularization (which leads to more noisy class weights) is easier to fool (top). Higher regularization produces more diffuse filters and is harder to fool (bottom). That is, it's harder to achieve very confident wrong answers (however, with weights so small it is hard to achieve very confident correct answers too). To flip the label to a wrong class, more visually obvious perturbations are also needed. Somewhat paradoxically, the model with the noisy weights (top) works quite a bit better on validation data (2.6% vs. 1.4% accuracy).

### Toy Example

We can understand this process in even more detail by condensing the problem to the smallest toy example that displays the problem. Suppose we train a binary logistic regression, where we define the probability of class 1 as $P(y = 1 \mid x; w,b) = \sigma(w^Tx + b)$, where $\sigma(z) = 1/(1+e^{-z})$ is the sigmoid function that squashes the class 1 score $s = w^Tx+b$ into range between 0 and 1, where 0 is mapped to 0.5. This classifier hence decides that the class of the input is 1 if $s > 0$, or equivalently if the class 1 probability is more than 50% (i.e. $\sigma(s) > 0.5$). Suppose further that we had the following setup:

```javascript
x = [2, -1, 3, -2, 2, 2, 1, -4, 5, 1] // input
w = [-1, -1, 1, -1, 1, -1, 1, 1, -1, 1] // weight vector
```

If you do the dot product, you get `-3`. Hence, probability of class 1 is `1/(1+e^(-(-3))) = 0.0474`. In other words the classifier is 95% certain that this is example is class 0. We're now going to try to fool the classifier. That is, we want to find a tiny change to `x` in such a way that the score comes out much higher. Since the score is computed with a dot product (multiply corresponding elements in `x` and `w` then add it all up), with a little bit of thought it's clear what this change should be: In every dimension where the weight is positive, we want to slightly increase the input (to get slightly more score). Conversely, in every dimension where the weight is negative, we want the input to be slightly lower (again, to get slightly more score). In other words, an adversarial `xad` might be:

```javascript
// xad = x + 0.5w gives:
xad = [1.5, -1.5, 3.5, -2.5, 2.5, 1.5, 1.5, -3.5, 4.5, 1.5]
```

Doing the dot product again we see that suddenly the score becomes 2. This is not surprising: There are 10 dimensions and we've tweaked the input by 0.5 in every dimension in such a way that we *gain* 0.5 in each one, adding up to a total of 5 additional score, rising it from -3 to 2. Now when we look at probability of class 1 we get `1/(1+e^(-2)) = 0.88`. That is, we tweaked the original `x` by a small amount and we improved the class 1 probability from 5% to 88%! Moreover, notice that in this case the input only had 10 dimensions, but an image might consist of many tens of thousands of dimensions, so you can afford to make tiny changes across all of them that all add up in concert in exactly the worst way to blow up the score of any class you wish.

### Conclusions

Several other related experiments can be found in [Explaining and Harnessing Adversarial Examples](http://arxiv.org/abs/1412.6572) by Goodfellow et al. This paper is a required reading on this topic. It was the first to articulate and point out the linear functions flaw, and more generally argued that there is a tension between models that are easy to train (e.g. models that use linear functions) and models that resist adversarial perturbations.

As closing words for this post, the takeaway is that ConvNets still work very well in practice. Unfortunately, it seems that their competence is relatively limited to a small region around the data manifold that contains natural-looking images and distributions, and that once we artificially push images away from this manifold by computing noise patterns with backpropagation, we stumble into parts of image space where all bets are off, and where the linear functions in the network induce large subspaces of fooling inputs.

With wishful thinking, one might hope that ConvNets would produce all-diffuse probabilities in regions outside the training data, but there is no part in an ordinary objective (e.g. mean cross-entropy loss) that explicitly enforces this constraint. Indeed, it seems that the class scores in these regions of space are all over the place, and worse, a straight-forward attempt to patch this up by introducing a background class and iteratively adding fooling images as a new *background* class during training are not effective in mitigating the problem.

It seems that to fix this problem we need to change our objectives, our forward functional forms, or even the way we optimize our models. However, as far as I know we haven't found very good candidates for either. To be continued.

#### Further Reading

- Ian Goodfellow gave a talk on this work at the [RE.WORK Deep Learning Summit 2015](https://www.youtube.com/watch?v=Pq4A2mPCB0Y)
- You can fool ConvNets as part of [CS231n Assignment #3 IPython Notebook](http://cs231n.github.io/assignment3/).
- [IPython Notebook](http://cs.stanford.edu/people/karpathy/break_linear_classifier.ipynb) for this experiment. Also my [Caffe linear classifier](http://cs.stanford.edu/people/karpathy/caffe_linear_imagenet.zip) protos if you like.