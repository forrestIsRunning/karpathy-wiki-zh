![](https://karpathy.github.io/assets/obamafunny.jpg) 上面的图片很有趣。

但对我来说，它也是那些让我对人工智能和计算机视觉的前景感到沮丧的例证之一。要让一台计算机像你我一样理解这张图像，需要做到什么程度？我请你明确地思考一下，要让这一切变得合理，需要哪些知识块各就各位。以下是我简要的尝试：

- 你识别出这是一群人的图像，并理解他们在走廊里
- 你识别出场中有 3 面镜子，所以其中一些人是来自不同视角的"虚拟"复制品
- 你从构成奥巴马面部的几个像素中识别出他。他穿着西装、周围有其他穿西装的人也有助于识别
- 你识别出有一个人站在秤上，尽管秤只占了很少的白色像素，并且与背景融为一体。但是，你利用了这个人的姿态以及人与物体互动的知识来搞清楚这一点
- 你识别出奥巴马的脚刚好稍微放在了秤上。注意我使用的语言：这是基于场景的三维结构，而不是腿在图像的二维坐标系中的位置
- 你了解物理原理：奥巴马倾斜压在秤上，对秤施加了力。秤测量施加在它上面的力，这就是它的工作原理 => 它会高估站在秤上的人的体重
- 正在称重的人没有意识到奥巴马在这样做。你推导出这一点，因为你了解他的姿态，你理解一个人的视野是有限的，并且你理解他不太可能感觉到奥巴马脚的轻微推动
- 你理解人们对自己的体重很在意。你也理解他正在读取秤上的读数，并且不久之后，被高估的体重会让他困惑，因为它很可能远远高于他的预期。换句话说，你推理了这张照片拍摄后几秒钟内即将发生的事件的含义，特别是关于人们的想法以及这些想法将如何在他们脑海中展开。你还推理了哪些信息是人们可以获得的
- 后面有些人觉得这个人即将到来的困惑很有趣。换句话说，你在推理人们的心理状态，以及他们对另一个人心理状态的看法。这已经到了可怕的元认知层面
- 最后，这里的"肇事者"是总统这一事实可能让它更加有趣。你根据人们的地位和身份，理解哪些行为更可能或更不可能被不同的人采取

我可以继续下去，但关键点是，在你看到这张照片并大笑的那半秒钟里，你已经使用了**大量的**信息。关于场景三维结构的信息、令人困惑的视觉元素（如镜子）、人物的身份、可供性以及人们如何与物体互动、物理原理（特定仪器如何工作、倾斜及其效果）、人、他们对自己体重的不安倾向、你从站在秤上的人的角度推理了情况——他知道什么、他的意图是什么、他有哪些信息可用——而且你推理了人们对其他人的推理。你还思考了场景的动态，并猜测了接下来几秒钟内情况在视觉上会如何展开，在相关人员的思想中会如何展开，并且你推理了特定身份/地位的人采取某些行为的可能性有多大。不知何故，所有这些事情汇聚在一起，"理解"了这个场景。

令人难以置信的是，以上所有的推理都是从快速扫一眼一个由 R、G、B 值组成的二维数组中展开的。核心问题是，像素值只是巨大冰山的一角，而从先验知识中推导出整个冰山的形状和大小是我们面前最困难的任务。我们如何能开始编写一个能够像我一样推理场景的算法？暂时忘记能够将这一切整合起来的推理算法；我们如何开始收集能够支持这些推理的数据（例如，秤是如何工作的）？我们如何给计算机一个机会？

现在考虑一下，计算机视觉领域的最先进技术是在像 ImageNet（为整张图像分配 1-of-k 标签的任务）或 Pascal VOC 检测挑战赛（+ 包括边界框）这样的任务上进行测试的。还有相当多关于姿态估计、动作识别等方面的工作，但它们都是特定的、不连贯的，而且只成功了一半。我不想这么说，但考虑到我们面前的任务，考虑到我们如何能从这里到达那里，计算机视觉和人工智能的现状是可怜的。前方的道路漫长、不确定且不清晰。

我见过一些论点认为，我们只需要更多的数据——来自图像、视频，也许还有文本——并运行一些聪明的学习算法：也许是一个更好的目标函数，运行 SGD（随机梯度下降），也许调整步长，使用 Adagrad，或者在这里那里加一个 L1 正则化，一切就会自动浮现。如果我们再多几招就好了！但对我来说，像这样的例子说明，我们缺少拼图的许多关键部分，中心问题既在于如何获得正确形式的正确训练数据以支持这些推理，也在于如何做出这些推理本身。

进一步思考这个问题的复杂性和规模，一个似乎不可避免的结论是，我们可能还需要具身体验，而构建能够像我们一样解释场景的计算机的唯一方法是让它们接触我们所拥有的多年（结构化、时间连贯的）经验、与世界互动的能力，以及某种神奇地主动学习/推理架构——当我反过来思考它应该能够做什么时，我几乎无法想象。

无论如何，我们离目标还非常、非常遥远，这让我感到沮丧。前进的道路是什么？：( 也许我应该去做个创业公司。我有非常酷的关于移动本地社交 iPhone 应用的想法。

---

*English original below:*

![](https://karpathy.github.io/assets/obamafunny.jpg) The picture above is funny.

But for me it is also one of those examples that make me sad about the outlook for AI and for Computer Vision. What would it take for a computer to understand this image as you or I do? I challenge you to think explicitly of all the pieces of knowledge that have to fall in place for it to make sense. Here is my short attempt:

- You recognize it is an image of a bunch of people and you understand they are in a hallway
- You recognize that there are 3 mirrors in the scene so some of those people are "fake" replicas from different viewpoints.
- You recognize Obama from the few pixels that make up his face. It helps that he is in his suit and that he is surrounded by other people with suits.
- You recognize that there's a person standing on a scale, even though the scale occupies only very few white pixels that blend with the background. But, you've used the person's pose and knowledge of how people interact with objects to figure it out.
- You recognize that Obama has his foot positioned just slightly on top of the scale. Notice the language I'm using: It is in terms of the 3D structure of the scene, not the position of the leg in the 2D coordinate system of the image.
- You know how physics works: Obama is leaning in on the scale, which applies a force on it. Scale measures force that is applied on it, that's how it works => it will over-estimate the weight of the person standing on it.
- The person measuring his weight is not aware of Obama doing this. You derive this because you know his pose, you understand that the field of view of a person is finite, and you understand that he is not very likely to sense the slight push of Obama's foot.
- You understand that people are self-conscious about their weight. You also understand that he is reading off the scale measurement, and that shortly the over-estimated weight will confuse him because it will probably be much higher than what he expects. In other words, you reason about implications of the events that are about to unfold seconds after this photo was taken, and especially about the thoughts and how they will develop inside people's heads. You also reason about what pieces of information are available to people.
- There are people in the back who find the person's imminent confusion funny. In other words you are reasoning about state of mind of people, and their view of the state of mind of another person. That's getting frighteningly meta.
- Finally, the fact that the perpetrator here is the president makes it maybe even a little more funnier. You understand what actions are more or less likely to be undertaken by different people based on their status and identity.

I could go on, but the point here is that you've used a HUGE amount of information in that half second when you look at the picture and laugh. Information about the 3D structure of the scene, confounding visual elements like mirrors, identities of people, affordances and how people interact with objects, physics (how a particular instrument works, leaning and what that does), people, their tendency to be insecure about weight, you've reasoned about the situation from the point of view of the person on the scale, what he is aware of, what his intents are and what information is available to him, and you've reasoned about people reasoning about people. You've also thought about the dynamics of the scene and made guesses about how the situation will unfold in the next few seconds visually, how it will unfold in the thoughts of people involved, and you reasoned about how likely or unlikely it is for people of particular identity/status to carry out some action. Somehow all these things come together to "make sense" of the scene.

It is mind-boggling that all of the above inferences unfold from a brief glance at a 2D array of R,G,B values. The core issue is that the pixel values are just a tip of a huge iceberg and deriving the entire shape and size of the icerberg from prior knowledge is the most difficult task ahead of us. How can we even begin to go about writing an algorithm that can reason about the scene like I did? Forget for a moment the inference algorithm that is capable of putting all of this together; How do we even begin to gather data that can support these inferences (for example how a scale works)? How do we go about even giving the computer a chance?

Now consider that the state of the art techniques in Computer Vision are tested on things like Imagenet (task of assigning 1-of-k labels for entire images), or Pascal VOC detection challenge (+ include bounding boxes). There is also quite a bit of work on pose estimation, action recognition, etc., but it is all specific, disconnected, and only half works. I hate to say it but the state of CV and AI is pathetic when we consider the task ahead, and when we think about how we can ever go from here to there. The road ahead is long, uncertain and unclear.

I've seen some arguments that all we need is lots more data from images, video, maybe text and run some clever learning algorithm: maybe a better objective function, run SGD, maybe anneal the step size, use adagrad, or slap an L1 here and there and everything will just pop out. If we only had a few more tricks up our sleeves! But to me, examples like this illustrate that we are missing many crucial pieces of the puzzle and that a central problem will be as much about obtaining the right training data in the right form to support these inferences as it will be about making them.

Thinking about the complexity and scale of the problem further, a seemingly inescapable conclusion for me is that we may also need embodiment, and that the only way to build computers that can interpret scenes like we do is to allow them to get exposed to all the years of (structured, temporally coherent) experience we have, ability to interact with the world, and some magical active learning/inference architecture that I can barely even imagine when I think backwards about what it should be capable of.

In any case, we are very, very far and this depresses me. What is the way forward?:( Maybe I should just do a startup. I have a really cool idea for a mobile local social iPhone app.