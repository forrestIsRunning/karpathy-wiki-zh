### CIFAR-10

> 注：这篇文章来自2011年，部分内容可能略显过时。

**统计数据**。CIFAR-10 包含 50,000 张训练图像，全部属于 10 个类别之一（左侧展示）。测试集包含来自相同类别的 10,000 张新图像，任务是将每张图像分类到其所属类别。当时的最先进水平约为 80% 的分类准确率（使用 4000 个中心点），由 [Adam Coates 等人 (PDF)](http://ai.stanford.edu/~acoates/papers/coatesleeng_aistats_2011.pdf) 实现。该论文通过白化处理、k-means 学习大量中心点，然后使用 soft 激活函数作为特征来达到这一准确率。

**最先进水平的性能**。顺便提一下，用他们的方法运行 1600 个中心点可以得到 77% 的分类准确率。如果将聚类设为随机，准确率会降到 70%；如果将聚类设为训练集中的随机图像块，准确率会上升到 74%。看起来 k-means 的全部意义就是让聚类中心很好地分布在数据周围。我猜测 70% 的随机聚类性能可能是因为许多聚类中心距离数据流形相对太远而从未被激活——效果就好像你一开始就只有少得多的聚类中心一样。

**人类准确率**。上周末我想看看人类在这个数据集上能达到什么样的分类准确率。我写了一个快速的 MATLAB 代码来提供操作界面。它一次显示一张图像，让我按 0-9 键来表示我认为的类别。我在 400 张图像上的分类准确率最终约为 **94%**。为什么不是 100%？因为有些图像实在太不公平了！下面是一些来自 CIFAR-10 的有问题的图像：![](https://karpathy.github.io/assets/cifar_weirdimages.png)

> CIFAR-10 的人类准确率约为 94%

### 观察

从这次练习中我得出了一些观察：

- 这个数据集中同一类别内的物体可能极其多样。例如，"鸟"类别包含许多不同类型的鸟（既有大鸟也有小鸟）。不仅有多种类型的鸟，它们还以多种可能的放大倍数、所有可能的角度和所有可能的姿态出现。有时只显示了鸟的一部分。姿态问题在狗/猫类别中更加严重，因为这些动物有许多许多种不同的姿态，有时只显示头部，或者身体左侧等等。
- 我的分类方法感觉奇怪地二元化。有时你可以清楚地看到动物或物体，并基于高度信息量的独特部分进行分类（例如，你找到了猫的耳朵）。其他时候，我的识别纯粹基于上下文和图像中的整体线索，比如颜色。
- CIFAR-10 数据集太小，无法恰当地包含测试集所要求的所有示例。我至少基于多种可视化训练集中最近邻图像的方法得出这个结论。
- 我不太明白 Adam Coates 等人是如何用他们的方法在这一数据集上表现如此之好（80%）的。我的猜测是它的工作方式如下：眯着眼睛看图像，你几乎总能将类别缩小到大约 2 或 3 个。最终的区分可能来自于找到非常好的特定信息块（比如某种毛皮的斑块、尖耳朵部分等）。k-means 字典一定捕捉到了这些情况，而 SVM 很可能利用了它们。
- 我从这次练习中得到的印象是，超过 80% 将很困难，但我怀疑可能可以提高 85-90% 的范围，具体取决于我对训练数据不足的判断有多错误。（**2015 年更新**：显然这个预测大错特错，现在的最高水平已达到 95%，如这个 [Kaggle 竞赛排行榜](https://www.kaggle.com/c/cifar-10/leaderboard) 所示。我印象深刻！）

我鼓励大家亲自尝试（见上面的代码），这非常有趣！我很难准确地表达我学到了什么，但总体来说，我觉得我对图像分类任务有了更直观的理解，对眼前问题的难度也有了更多的认识。

最后，这是我的调试界面示例：![](https://karpathy.github.io/assets/cifar_predict.jpg)

生成这些结果的 MATLAB 代码可以在这里找到：[链接](http://cs.stanford.edu/people/karpathy/cifar10inspect.zip)

---

*English original below:*

### CIFAR-10

> Note, this post is from 2011 and slightly outdated in some places.

![](https://karpathy.github.io/assets/cifar_preview.png)

**Statistics**. CIFAR-10 consists of 50,000 training images, all of them in 1 of 10 categories (displayed left). The test set consists of 10,000 novel images from the same categories, and the task is to classify each to its category. The state of the art is currently at about 80% classification accuracy (4000 centroids), achieved by [Adam Coates et al. (PDF)](http://ai.stanford.edu/~acoates/papers/coatesleeng_aistats_2011.pdf). This paper achieved the accuracy by using whitening, k-means to learn many centroids, and then using a soft activation function as features.

**State of the Art performance.** By the way, running their method with 1600 centroids gives 77% classification accuracy. If you set the clusters to be random the accuracy becomes 70%, and if you set the clusters to be random patches from the training set, the accuracy goes up to 74%. It seems like the whole purpose of k-means is to nicely spread out the clusters around the data. I'm guessing that the 70% random clusters performance might be because many of the clusters are relatively too far away from data manifolds, and never become activated – it's as if you had much fewer clusters to begin with.

**Human Accuracy.** Over the weekend I wanted to see what kind of classification accuracy a human would achieve on this dataset. I set out to write some quick MATLAB code that would provide the interface to do this. It showed one image at a time and allowed me to press a key from 0-9 indicating my belief about its class category. My classification accuracy ended up at about **94%** on 400 images. Why not 100%? Because some images are really unfair! To give you an idea, here are some questionable images from CIFAR-10: ![](https://karpathy.github.io/assets/cifar_weirdimages.png)

> CIFAR-10 human accuracy is approximately 94%

### Observations

A few observations I derived from this exercise:

- The objects within classes in this dataset can be extremely varied. For example the "bird" class contains many different types of bird (both big birds and small). Not only are there many types of bird, but the occur at many possible magnifications, all possible angles and all possible poses. Sometimes only parts of the bird are shown. The poses problem is even worse for the dog/cat category, because these animals occur at many many different types of poses, and sometimes only the head is shown. Or left part of the body, etc.
- My classification method felt strangely dichotomous. Sometimes you can clearly see the animal or object and classify it based very highly-informative distinct parts (for example, you find ears of a cat). Other times, my recognition was purely based on context and the overall cues in the image such as the colors.
- The CIFAR-10 dataset is too small to properly contain examples of everything that it is asking for in the test set. I base this conclusion at least on my multiple ways of visualizing the nearest image in the training set.
- I don't quite understand how Adam Coates et al. perform so well on this dataset (80%) with their method. My guess is that it works along the following lines: looking at the image squinting your eyes you can almost always narrow down the category to about 2 or 3. The final disambiguation probably comes from finding very good specific informative patches (like a patch of some kind of fur, or pointy ear part, etc.). The k-means dictionary must be catching these cases and the SVM likely picks up on them.
- My impression from this exercise is that it will be hard to go above 80%, but I suspect improvements might be possible up to range of about 85-90%, depending on how wrong I am about the lack of training data. (**2015 update**: Obviously this prediction was way off, with state of the art now in 95%, as seen in this [Kaggle competition leaderboard](https://www.kaggle.com/c/cifar-10/leaderboard). I'm impressed!)

I encourage people to try this for themselves (see my code, above), as it is very interesting and fun! I have trouble exactly articulating what I learned, but overall I feel like I gained more intuition for image classification tasks and more appreciation for the difficulty of the problem at hand.

Finally, here is an example of my debugging interface: ![](https://karpathy.github.io/assets/cifar_predict.jpg)

The Matlab code used to generate these results can be found [here](http://cs.stanford.edu/people/karpathy/cifar10inspect.zip)