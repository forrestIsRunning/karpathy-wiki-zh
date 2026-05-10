我在 Google 暑期实习的工作已经转化为一篇 CVPR 2014 Oral 论文，题为 **"Large-scale Video Classification with Convolutional Neural Networks"**（**[项目页面](http://cs.stanford.edu/people/karpathy/deepvideo/)**）。上周在 CVPR 的论文和口头报告中，政治正确、专业且精心构思的科学阐述是一回事，但我认为这个博客也是一个很好的媒介，可以更非正式和个人化地讲述这篇论文背后的故事，以及它如何融入一个更大的背景。

### 第一幕：Google Research 暑期实习 2011

![](https://karpathy.github.io/assets/megoogle.jpg)

2011 年在 Google 实习

这篇论文的线索始于 2011 年夏天，当时我接受了 Google Research 的暑期实习机会。我的项目涉及视频深度学习，作为一个当时只有几个人但后来发展为 [Google Brain](http://en.wikipedia.org/wiki/Google_Brain) 的优秀团队的一部分。

项目的目标是学习能够支持多种视频分类任务的时空特征。当然，问题在于视频是一个巨大的三维像素值块，如果你试图分类其中发生了什么物体/概念，它的原始形式是无用的。计算机视觉研究人员提出了[许多巧妙的方法](http://hal.archives-ouvertes.fr/inria-00439769/)在这些像素上计算手工设计的特征，将表示转换为对分类任务更直接有用的形式，但我们感兴趣的是用深度学习从原始数据中学习特征。

> "当时的深度学习 landscape 非常不同。"

值得注意的是，当时的深度学习 landscape 非常不同。每个人都主要对**无监督学习**感到兴奋：训练巨大的自编码器，吞噬所有的互联网数据，自动创建支持各种迁移学习任务的强大表示。这种雄心在很大程度上受到了以下因素的推动：

1. **人类学习**（人类是无监督学习的，所以我们的算法也应该如此（论点如此））
2. 学术界**并行的工作**，从 2006 年左右开始的深度学习复兴主要由具有显著无监督学习成分的算法组成（RBM、自编码器等）。
3. **实际考虑**：未标记的视频比标记数据更容易获得——如果我们不必担心标签，那不是很好吗？

大约在这个时候，我对视频变得特别感兴趣，因为我通过各种思想实验和神经科学论文说服自己，如果视觉领域的无监督学习要成功，它将涉及视频数据。以某种方式。我认为最好的机会可能是某种深度[慢特征分析](http://www.scholarpedia.org/article/Slow_feature_analysis)目标，但我最终工作的架构更类似于 CVPR 2011 论文 ["Learning hierarchical invariant spatio-temporal features for action recognition with independent subspace analysis"](http://cs.stanford.edu/~quocle/LeZouYeungNg11.pdf)。然而，在我们能够在 YouTube 的一块数据上扩大规模之前，夏天就结束了。

### 第二幕：斯坦福的无监督学习

那年秋天我离开了 Google，加入斯坦福大学攻读博士学位。我被在 Google 的项目所影响，热切地希望继续在视觉领域的无监督特征学习方面工作。

**图像。** 我的第一个 rotation 之一是跟随 Andrew Ng，他当时也对图像的无监督学习感兴趣。我与他的学生 Adam Coates 合作，他致力于用简单的、显式的方法（如 k-means）。NIPS 论文 [Emergence of Object-Selective Features in Unsupervised Feature Learning](http://cs.stanford.edu/people/karpathy/nips2012.pdf) 是我们努力的成果，但我并不完全相信这个公式有意义。该算法构建不变性的唯一线索是通过相似性：看起来相似的东西（在 L2 距离上）会聚集在一起，并在上一层中成为不变量。我想，仅此而已是不可能的。

![](https://karpathy.github.io/assets/nips2012.jpeg)

NIPS 2012 论文：通过将相似图像块链接成不变量来学习特征。

> "我无法看出仅基于图像的无监督学习如何能够工作。"

更一般地说，我无法看出仅基于图像的无监督学习如何能够工作。对于一个无监督算法来说，一块包含人脸的像素图像块与一块包含一些奇怪边缘/角落/草/树噪声的图像块是完全一样的。算法不应该担心后者，但它应该付出*额外的*努力去关注前者。但如果你只有十亿个图像块，你永远不会知道这一点！这一切归结为这个问题：如果你只有像素，没有别的，那么一张人脸的图像与一丛随机的灌木、或者房间天花板角落的图像有什么区别？我会回到这个问题上。

**3D。** 此时是我下一个 rotation 的时候了。我对处理像素感到沮丧，并开始思考另一种无监督学习的方法。在那之前一直潜伏在我脑海中的一些想法围绕着这样一个事实：我们生活并感知一个三维世界。也许图像和视频太难了。如果我们的无监督学习算法推理的是三维结构和布局，而不是二维的亮度网格，那不是更自然吗？我觉得人类在学习方面的优势在于能够从立体视觉和运动结构中获取所有这些信息（还有主动学习）。当我们把像素网格扔给算法，却期望有趣的事情发生时，我们是不是没有给算法一个公平的机会？

> "我们是不是没有给算法一个公平的机会？"

也大约在这个时候，Kinect 问世了，所以我想我会尝试一下 3D。我先在图形学方向与 [Vladlen Koltun](http://vladlen.info/) 轮转，后来夏天又与 [Fei-Fei](http://vision.stanford.edu/feifeili/) 轮转。我花了大量时间与 Kinect、3D 数据、Kinect Fusion、点云等打交道。我最终发现从 3D 数据学习面临四个挑战：

1. 没有明显/干净的方法将神经网络接入 3D 数据。
2. 推理被遮挡的空间与空白空间之间的区别是一个巨大的痛苦。
3. 大规模收集数据非常困难。神经网络热爱数据，而我却在摆弄大约 100 个场景的数据集，毫无办法知道这如何能够规模化。
4. 我处理的是完全静态的 3D 环境。没有运动，没有人，没有乐趣。

我最终在我的 3D 网格中做了一点无监督物体发现，并将其发表在相关度最高的机器人会议上（[Object Discovery in 3D scenes via Shape Analysis](http://cs.stanford.edu/people/karpathy/discovery/)）。我很高兴我找到了一种非常简单、高效且惊人地有效的在 3D 网格上计算物体性的方法，但这并不是我最初想做的事情。我在最后一个 rotation 中与 Sebastian Thrun 一起工作，对这个项目做了一些跟进，但我仍然感到不满和未完成。没有关于大脑的东西，没有可以学习的大型数据集，即使一切正常，它也只会适用于静态、无聊的场景。

![](https://karpathy.github.io/assets/objectdiscovery.jpeg)

ICRA 2013 论文：高亮的网格部分是发现的物体。

这对我来说是博士期间的一个低谷。我一直在思考让无监督特征学习工作的方法，但不断遇到障碍——既是实践上的，更令人担忧的是，哲学上的。我开始有点 burnout 了。

### 第三幕：计算机视觉颠倒

大约在这个时候，我加入了 Fei-Fei 的实验室，寻找与计算机视觉相关的研究方向。我希望我的工作涉及深度学习和特征学习的元素，但当时深度学习在计算机视觉中并不是一个热门话题。许多人对这个尝试持怀疑态度：深度学习论文很难被计算机视觉会议接收（例如，著名的 [Yann LeCun 致 CVPR AC 的公开信](https://plus.google.com/+YannLeCunPhD/posts/gurGyczzsJ7)）。另一个问题是我感到有点卡住了，不确定如何继续。

**AlexNet。** 大约在这个时候，一篇将改变我的研究方向、也将改变计算机视觉方向的论文发表了。我指的是 ["ImageNet Classification with Deep Convolutional Neural Networks"](http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf)，其中卷积神经网络（CNN）在 ImageNet 分类挑战赛中显著优于当时的最先进方法。这篇论文描述的 CNN 架构后来被称为 *"AlexNet"*，以论文的第一作者 [Alex Krizhevsky](http://www.cs.toronto.edu/~kriz/) 命名。ConvNet 已经成熟，从仅仅一年前还在处理 MNIST/CIFAR-10 这样的玩具数据集，突然跃进到运行在大图像上，并击败了已开发多年的方法。我没有预料到如此巨大的飞跃，我认为大多数社区也没有。

![](https://karpathy.github.io/assets/zeilercnnfeatures.jpeg)

学习到的 CNN 特征。可视化来自 Zeiler 和 Fergus 2013 年的一篇漂亮论文，[Visualizing and Understanding Convolutional Networks](http://www.matthewzeiler.com/pubs/arxive2013/arxive2013.pdf)。在网络深处，特征变得更加扩展和复杂。

**迁移学习。** AlexNet 令人印象深刻的性能本身就很有趣，但随之而来的第二个违反直觉的发现是，ImageNet 预训练的表示在迁移学习到其他数据集的任务中被证明极其强大。突然间，人们开始使用 ImageNet 预训练的 CNN，切除顶部的分类器层，将紧邻的前一层视为固定特征提取器，并在许多不同数据集上击败最先进的方法（参见 [DeCAF](http://arxiv.org/abs/1310.1531)、[Overfeat](http://arxiv.org/abs/1312.6229) 和 [Razavian et al.](http://arxiv.org/abs/1403.6382)）。我仍然觉得这相当令人惊讶。在某个平行宇宙中，我可以想象一个 CNN 在 ImageNet 上表现很好，但不一定能迁移到雕塑、鸟类和其他东西的奇怪数据集上，而我点头表示这是意料之中的。但这似乎不是我们所生活的宇宙。

![](https://karpathy.github.io/assets/cnntsne.jpeg)

一张 6000x6000 图像的小裁剪，展示了 CNN 如何排列视觉世界（使用 t-SNE）。在这里找到完整图像：[链接](http://cs.stanford.edu/people/karpathy/cnnembed/)。

**完全监督。** 这里需要做出的一个关键观察是，AlexNet 是在（有标签的）[ImageNet 挑战赛](http://www.image-net.org/challenges/LSVRC/2014/)数据集上的完全监督体制下训练的。没有任何无监督成分。那无监督学习该何去何从？无监督学习的主要目的是从未标记数据中学习强大的表示，然后可以在标签不多数据集上的迁移学习环境中使用。但我们看到的情况是，在大型监督数据集上的训练成功地填补了无监督学习的主要预期角色。这表明了一条通往强大、通用的表示的替代路线，它指向完全相反的方向：我们也许不应该在无标记数据上做无监督学习，而应该在所有我们能得到的监督数据上同时进行训练，使用多任务目标函数。

> "……在巨大的监督数据集上训练正在成功地填补无监督学习的主要预期角色。"

这让我回到了我上面的观点：如果你只有像素，一张人脸的图像与一个随机角落或道路的一部分或一棵树的图像有什么区别？我在这个问题上挣扎了很久，而我慢慢收敛到的讽刺性答案是：没有区别。在没有标签的情况下，没有区别。所以，除非我们希望我们的算法为人脸（以及我们非常关心的东西）开发强大的特征，同时也为大量的背景垃圾开发同样强大的特征，我们可能不得不付出标签的代价。

### 第四幕：Google Research 暑期实习 2013

当我第二次进入 Google 的那个夏天， landscape 与我 2011 年所见已经截然不同。两年前我离开时，正在为婴儿期的 Google Brain 实现用于学习时空（视频）特征的无监督学习算法。一切都带着研究的气息，我们仔细思考损失函数、算法等。当我回来时，我发现人们戴着工程师的帽子忙碌着，使用青春期的 Google Brain 在许多数据集上获得了巨大的成果，使用的是 1980 年代风格的全监督神经网络（类似于 AlexNet）。监督式的、普通的 feed-forward 神经网络成为了一把锤子，每个人都急于找到所有的钉子，摘取所有低垂的果实。这就是我开始第二个关于学习视频特征的项目时的氛围。配方更简单了。你有兴趣为 X 训练好的特征吗？

1. 获取 X 领域的大量标记数据
2. 用监督目标训练一个非常大的网络
3. ???
4. 收益

在我的情况下，第 4 步变成了 ["Large-scale Video Classification with Convolutional Neural Networks"](http://cs.stanford.edu/people/karpathy/deepvideo/)，其中我们训练了大型时空卷积神经网络。讽刺的是，我们选择使用的数据集（体育视频）结果对于学习丰富的时空特征来说有点太容易了，因为网络可以通过忽略大部分运动并主要依赖静态外观走得非常远（例如，如果你试图区分网球和游泳，你不需要关心细微的运动细节）。但我预计在未来几年会有显著的改进。（来自其他人，因为我不再从事视频工作了。）

![](https://karpathy.github.io/assets/sportspredict.jpeg)

时空 CNN 对视频进行体育预测。（蓝 = 真实标签，绿 = 预测正确，红 = 预测错误）

### 第五幕：向前看

两年前，我花费了大量的脑力，至少在概念上，试图破解无监督学习视觉世界的问题。我们将给算法提供大量的来自互联网的视觉数据（图像、视频、3D 或其他任何东西），它将自动发现能够支持像我们人类一样的丰富多样的任务的表示。

但当我回顾自己过去两年的研究、我的思想实验以及我在当前学术文献中看到的趋势时，我开始怀疑这个梦想可能永远无法实现——至少不是以我们最初意图的形式。大规模监督数据（即使标签很弱）正在成为许多最成功的深度学习应用的关键组成部分。事实上，我看到了完全逆转这一策略的迹象：我们可能不是在没有标签的情况下学习强大的特征，而是在巨大的多任务（甚至多模态）网络中从*所有*标签中学习它们，吞噬着我们能够获得的所有标签。这可能采取卷积网络的形式，其中来自多个不同数据集的梯度流过同一个网络，并更新共享参数。

> "我们可能不是在没有标签的情况下学习强大的特征，而是从*所有*标签中学习它们。"

*"但是等等，人类是无监督学习的——为什么要放弃？我们可能只是在概念上缺少了什么！"*，我听到过我的一些朋友这样争辩。不幸的是，这个前提可能是错误的：人类有在时间上连续的 RGBD 感知，并充分利用了主动学习、课程学习和强化学习，同时有各种预先布线的神经回路的帮助。想象一个（可怕的）实验，我们把一个幼儿放在显示器前，连续数月向他/她闪现随机的互联网图片。我们期望他们发展出同样的对视觉世界的理解吗？因为我们目前正试图让计算机做这样的事情。

人类和计算机实际可用的数据在其优势、劣势和类型上是根本不一致的。因此，直接进行比较是不公平的，在从人类学习中汲取灵感时应极其谨慎。也许有一天，当机器人技术发展到我们有大量具身机器人像我们一样与三维视觉世界互动的程度时，我会再次尝试无监督学习。我怀疑它将大量使用时间信息和强化学习。但在那之前，让我们收集一些数据，训练一些巨大的、全监督的、多任务的、多模态的网络并……"收益" : )

---

*English original below:*

My summer internship work at Google has turned into a CVPR 2014 Oral titled **"Large-scale Video Classification with Convolutional Neural Networks"** [(project page)](http://cs.stanford.edu/people/karpathy/deepvideo/). Politically correct, professional, and carefully crafted scientific exposition in the paper and during my oral presentation at CVPR last week is one thing, but I thought this blog might be a nice medium to also give a more informal and personal account of the story behind the paper and how it fits into a larger context.

### Act I: Google Research Summer Internship 2011

![](https://karpathy.github.io/assets/megoogle.jpg)

Hanging out at Google in 2011

The thread of this paper begins in Summer of 2011, when I accepted a summer internship offer from Google Research. My project involved Deep Learning for videos, as part of a great team that was at the time only a few people but would later grow to become [Google Brain](http://en.wikipedia.org/wiki/Google_Brain).

The goal of the project was to learn spatio-temporal features that could support a variety of video classification tasks. The problem, of course, is that videos are a giant 3-dimensional block of pixel values which is useless in its raw form if you're trying to classify what objects/concepts occur within. Computer Vision researchers have come up with [many ingenious ways](http://hal.archives-ouvertes.fr/inria-00439769/) of computing hand-crafted features over these pixels to transform the representation into one that is more directly useful to a classification task, but we were interested in learning features from raw data with Deep Learning.

> " Deep Learning landscape was very different at that time. "

It's interesting to note that the Deep Learning landscape was very different at that time. Everyone was excited primarily about **Unsupervised Learning**: The idea of training enormous autoencoders that gobble up all of internet data and automagically create powerful representations that support a large variety of transfer learning tasks. A lot of this ambition was motivated by:

1. **Human learning** (people learn unsupervised, and so should our algorithms (the argument goes))
2. Parallel **work in academia**, where resurgence of Deep Learning methods starting around 2006 has largely consisted of algorithms with a significant unsupervised learning component (RBMs, autoencoders, etc.).
3. **Practical considerations**: unlabeled videos are much easier to obtain than labeled data - wouldn't it be nice if we didn't have to worry about labels?

Around this time I became particularly interested in videos because I convinced myself through various thought experiments and neuroscience papers that if unsupervised learning in visual domain was to ever work, it would involve video data. Somehow. I thought the best shot might be some kind of Deep, [Slow Feature Analysis](http://www.scholarpedia.org/article/Slow_feature_analysis) objective, but I ended up working on architectures more similar to CVPR 2011 ["Learning hierarchical invariant spatio-temporal features for action recognition with independent subspace analysis"](http://cs.stanford.edu/~quocle/LeZouYeungNg11.pdf). However, the summer was over before we could get something interesting scaled over a chunk of YouTube.

### Act II: Unsupervised Learnings at Stanford

I left Google that fall and joined Stanford as a PhD student. I was swayed by my project at Google and felt eager to continue working on Unsupervised Feature Learning in visual domains.

**Images.** One of my first rotations was with Andrew Ng, who was also at the time interested in Unsupervised Learning in images. I joined forces with his student Adam Coates who worked on doing so with simple, explicit methods (e.g. k-means). The NIPS paper [Emergence of Object-Selective Features in Unsupervised Feature Learning](http://cs.stanford.edu/people/karpathy/nips2012.pdf) was the result of our efforts, but I didn't fully believe that the formulation made sense. The algorithm's only cue for building invariance was through similarity: Things that looked similar (in L2 distance) would group together and become invariants in the layer above. That alone can't be right, I thought.

![](https://karpathy.github.io/assets/nips2012.jpeg)

NIPS 2012 paper: Learning Features by linking similar patches into invariants.

> " I couldn't see how Unsupervised Learning based solely on images could work. "

More generally, I couldn't see how Unsupervised Learning based solely on images could work. To an unsupervised algorithm, a patch of pixels with a face on it is exactly as exciting as a patch that contains some weird edge/corner/grass/tree noise stuff. The algorithm shouldn't worry about the latter but it should spent *extra* effort worrying about the former. But you would never know this if all you had was a billion patches! It all comes down to this question: if all you have are pixels and nothing else, what distinguishes images of a face, or objects from a random bush, or a corner in the ceilings of a room? I'll come back to this.

**3D.** At this point it was time for my next rotation. I felt frustrated by working with pixels and started thinking about another line of attack to unsupervised learning. A few ideas that have been dormant in my brain until then centered around the fact that we live and perceive a 3D world. Perhaps images and videos were too hard. Wouldn't it be more natural if our unsupervised learning algorithms reasoned about 3D structures and arrangements rather than 2D grids of brightness? I felt that humans had advantage in their access to all this information during learning from stereo and structure from motion (and also Active Learning). Were we not giving our algorithms a fair chance when we throw grids of pixels at them and expect something interesting to happen?

> " Were we not giving our algorithms a fair chance? "

This was also around the time when the Kinect came out, so I thought I'd give 3D a shot. I rotated with [Vladlen Koltun](http://vladlen.info/) in Graphics and later with [Fei-Fei](http://vision.stanford.edu/feifeili/) over the summer. I spent a lot of my time wrestling with Kinect, 3D data, Kinect Fusion, Point Clouds, etc. There were four challenges to learning from 3D data that I eventually discovered:

1. There is no obvious/clean way to plug a neural network into 3D data.
2. Reasoning about the difference between occluded / empty space is a huge pain.
3. It is very hard to collect data at scale. Neural nets love data and here I was playing around with datasets on order of 100 scenes, with no ideas about how this could be possibly scale.
4. I was working with fully static 3D environments. No movement, no people, no fun.

I ended up doing a bit of Unsupervised Object Discovery in my 3D meshes and publishing it at a robotics conference, where it was most relevant ([Object Discovery in 3D scenes via Shape Analysis](http://cs.stanford.edu/people/karpathy/discovery/)). I was happy that I found a very simple, efficient and surprisingly effective way of computing objectness over 3D meshes, but it wasn't what I set out to do. I followed up on the project a bit while working with Sebastian Thrun for my last rotation, but I remained unsatisfied and unfulfilled. There was no brain stuff, no huge datasets to learn from, and even if it all worked, it would work on static, boring scenes.

![](https://karpathy.github.io/assets/objectdiscovery.jpeg)

ICRA 2013 paper: Highlighted mesh parts are discovered objects.

This was a low point for me in my PhD. I kept thinking about ways of making unsupervised feature learning work, but kept coming across roadblocks– both practical but more worryingly, philosophical. I was getting a little burnt out.

### Act III: Computer Vision Upside Down

Around this time I joined Fei-Fei's lab and looked around for a research direction related to Computer Vision. I wanted my work to involve elements of deep learning and feature learning, but at this time deep learning was not a hot topic in Computer Vision. Many people were skeptical of the endeavor: Deep Learning papers had trouble getting accepted to Computer Vision conferences (see for example, famously [Yann LeCun's public letter to CVPR AC](https://plus.google.com/+YannLeCunPhD/posts/gurGyczzsJ7)). The other issue was that I felt a little stuck and unsure about how to proceed.

**AlexNets.** It was around this time that the paper that would change the course of my research, and also the course of Computer Vision came out. I'm referring to ["ImageNet Classification with Deep Convolutional Neural Networks"](http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf), in which a Convolutional Neural Network (CNN) significantly outperformed state of the art methods on the ImageNet Classification Challenge. The described CNN architecture has become known as the *"AlexNet"*, after the first author of the paper: [Alex Krizhevsky](http://www.cs.toronto.edu/~kriz/). ConvNets have come of age and leapfrogged from working on toy MNIST/CIFAR-10 datasets just a year ago, to suddenly running on large images and beating methods that have been developed for years. I did not expect such an astronomical leap and I think neither did most of the community.

![](https://karpathy.github.io/assets/zeilercnnfeatures.jpeg)

Learned CNN features. Visualization taken from a nice paper by Zeiler and Fergus 2013, [Visualizing and Understanding Convolutional Networks"](http://www.matthewzeiler.com/pubs/arxive2013/arxive2013.pdf). The features become more extended and complex deeper in the network.

**Transfer Learning.** The impressive performance of the AlexNet was interesting by itself, but the second unintuitive finding that followed was that the ImageNet-pretrained representation proved extremely potent in transfer learning tasks to other datasets. Suddenly, people were taking an ImageNet-pretrained CNN, chopping off the classifier layer on top, treating the layers immediately before as a fixed feature extractor and beating state of the art methods across many different datasets (see [DeCAF](http://arxiv.org/abs/1310.1531), [Overfeat](http://arxiv.org/abs/1312.6229), and [Razavian et al.](http://arxiv.org/abs/1403.6382)). I still find this rather astonishing. In some parallel universe, I can image a CNN that performs very well on ImageNet but doesn't necessarily transfer to strange datasets of sculptures, birds and other things, and I'm nodding along and saying that that's to be expected. But that seems to not be the universe we live in.

![](https://karpathy.github.io/assets/cnntsne.jpeg)

A small crop of a 6000x6000 image that shows how CNN arranges the visual world (with t-SNE). Find full images [here](http://cs.stanford.edu/people/karpathy/cnnembed/).

**Fully Supervised.** A crucial observation to make here is that AlexNet was trained in a fully supervised regime on the (labeled) [ImageNet challenge](http://www.image-net.org/challenges/LSVRC/2014/) dataset. There are no unsupervised components to be found. Where does that leave us with unsupervised learning? The main purpose of unsupervised learning was to learn powerful representations from unlabeled data, which could then be used in transfer learning settings on datasets that don't have that many labels. But what we're seeing instead is that training on huge, supervised datasets is successfully filling the main intended role of unsupervised learning. This suggests an alternative route to powerful, generic representations that points in the complete opposite direction: Instead of doing unsupervised learning on unlabeled data, perhaps we should train on all the supervised data we have, at the same time, with multi-task objective functions.

> "… training on huge, supervised datasets is successfully filling the main intended role of unsupervised learning."

This brings me back to my point made above: if all you have is pixels, what is the difference between an image of a face and an image of a random corner or a part of a road, or a tree? I struggled with this question for a long time and the ironic answer I'm slowly converging on is: nothing. In absence of labels, there is no difference. So unless we want our algorithms to develop powerful features for faces (and things we care about a lot) alongside powerful features for a sea of background garbage, we may have to pay in labels.

### Act IV: Google Research Summer Internship 2013

When I entered Google the second time this summer, the landscape was very different than what I had seen in 2011. I left 2 years ago implementing unsupervised learning algorithms for learning spatio-temporal (video) features in baby Google Brain. Everything had a researchy feel and we were thinking carefully about loss functions, algorithms, etc. When I came back, I found people buzzing around with their engineer hats on, using adolescent Google Brain to obtain great results across many datasets with huge, 1980-style, fully supervised neural nets (similar to the AlexNet). Supervised, vanilla feed-forward Neural Nets became a hammer and everyone was eager to find all the nails and pick all the low-hanging fruit. This is the atmosphere that surrounded me when I started my second project on learning video features. The recipe was simpler. Are you interested in training nice features for X?

1. Get a large amount of labeled data in X domain
2. Train a very large network with supervised objective
3. ???
4. Profit

In my case, number 4 turned out to be ["Large-scale Video Classification with Convolutional Neural Networks"](http://cs.stanford.edu/people/karpathy/deepvideo/), in which we trained large Spatio-Temporal Convolutional Neural Networks. Ironically, the dataset we chose to use (Sports videos) turned out to be a little too easy to learn rich, spatio-temporal features since the network could get very far ignoring much of the motion and relying mostly on static appearances (e.g. if you're trying to tell difference between tennis and swimming, you need not be concerned with minute movement details). But I expect to see considerable improvements in the coming years. (From others, as I am no longer working on videos.)

![](https://karpathy.github.io/assets/sportspredict.jpeg)

Spatio-Temporal CNN predicting Sports on videos. (Blue = ground truth, Green = correct prediction, Red = incorrect)

### Act V: Forward

Two years ago, I spent a lot of my mental efforts trying to, at least conceptually, crack the problem of learning about the visual world unsupervised. We were going to feed an algorithm with lots and lots of visual data from the internet (images, videos, 3D or whatever else), and it would automatically discover representations that would support a variety of tasks as rich as those that we humans are capable of.

But as I reflect on the last two years of my own research, my thought experiments and the trends I'm seeing emerge in current academic literature, I am beginning to suspect that this dream may never be fulfilled - at least in the form we originally intended. Large-scale supervised data (even if weakly labeled) is turning out to be a critical component of many of the most successful applications of Deep Learning. In fact, I'm seeing indications of reversal of the strategy altogether: Instead of learning powerful features with no labels, we might end up learning them from ALL the labels in huge, multi-task (and even multi-modal) networks, gobbling up as many labels as we can get our hands on. This could take form of a Convolutional Network where gradients from multiple distinct datasets flow through the same network and update shared parameters.

> " Instead of learning powerful features with no labels, we might end up learning them from ALL the labels "

*"But wait, humans learn unsupervised - why give up? We might just be missing something conceptually!"*, I've heard some of my friends argue. The premise may, unfortunately be false: humans have temporally contiguous RGBD perception and take heavy advantage of Active Learning, Curriculum Learning, and Reinforcement Learning, with help from various pre-wired neural circuits. Imagine a (gruesome) experiment in which we'd sit a toddler in front of a monitor and flash random internet images at him/her for months. Would we expect them to develop the same understanding of the visual world? Because that's what we're currently trying to get working with computers.

The strengths, weaknesses and types of data practically available to humans and computers are fundamentally misaligned. Thus, it is unfair to draw direct comparisons and extreme caution should be taken when drawing inspiration from human learning. Perhaps one day when robotics advances to a point where we have masses of embodied robots interacting with the 3-dimensional visual world like we do, I will give unsupervised learning another shot. I suspect it will feature heavy use of temporal information and reinforcement learning. But until then, lets collect some data, train some huge, fully-supervised, multi-task, multi-modal nets and… "profit":)