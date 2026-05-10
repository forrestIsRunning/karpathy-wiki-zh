我一直在寻找有趣的数据集来收集、分析和解读。而有什么数据集比自己收集/分析其他数据集的*元数据集*——我自己的活动——更好呢？我每天*真正*花多少时间在工作上？我大部分时间是怎么过的？什么让我高效？这些都是我希望能有答案的相对重要的问题。由于我喜欢基于数据的答案，而不是容易受确认偏差影响的个人轶事，所以我写了 [ulogme](https://github.com/karpathy/ulogme)。

> "我喜欢基于数据的答案，而不是容易受确认偏差影响的个人轶事"

我现在已经记录了自己的电脑使用数据将近 **3 个月**。在这篇文章中，我将重点介绍这个项目的一些功能、我目前能得出的一些见解，以及我希望下一步能走向何方。谁知道呢，也许读完这篇文章你也会想成为用户 : )

### 已有的工具

追踪和可视化你的电脑活动这个想法并不新鲜。它在[量化自我](http://en.wikipedia.org/wiki/Quantified_Self)圈子中已经以各种形式和形态存在了多年，并且已经存在几个试图满足这一需求的程序。其中比较知名的有 [RescueTime](https://www.rescuetime.com/) 和 [Toggl](https://www.toggl.com/)，但还有几十到几百个相当糟糕的仿制品。在所有这些中，我找不到任何一个能满足几个非常简单的基本要求：

- 用户界面必须是**基于 Web 的**，因为现在是 2014 年了
- 一切必须是**开源的**且**免费的**
- 数据绝不能离开**本地机器**（不要云端的那些花里胡哨——太私密了！）
- 必须易于**定制**并且看起来**漂亮**

根本不存在这样的东西（实际上差得远），所以我决定自己实现一个解决方案。

### ulogme 快速浏览：单日视图

ulogme 小而简单：有两个*后端*组件：一个记录活动的跟踪脚本和一个提供活动日志给*前端*（可视化页面）的小型本地 Web 服务器包装器。跟踪脚本目前记录活动窗口标题（每 2 秒一次频率）和键盘击键频率。

让我们快速浏览一些得到的可视化和功能。首先是**单日视图**。例如，看看我的 8 月 1 日。头部显示记录日期，还有一个空间可以为每天写一段简短的"博客"记录：

![](https://karpathy.github.io/assets/ulogme_sv1.jpeg)

头部：日期信息、刷新按钮、切换日期的按钮，以及一个可编辑的当天"博客"记录。

现在我们开始进入正题。看起来那天我在办公室从上午 10 点待到了晚上 8 点。记住，我们全程记录了击键和窗口标题。下面是一天的击键分解：

![](https://karpathy.github.io/assets/ulogme_sv2.jpeg)

当天的击键统计数据。

我们看到那天我大部分时间在 Sublime Text 2（我用它写 Python/JS/C++）和 Gmail 中编码——看起来我写了不少邮件！接下来，ulogme 展示了我喜欢称之为*当天的条形码*的东西。这是当天所有窗口的分解：

![](https://karpathy.github.io/assets/ulogme_sv3.jpeg)

当天的条形码。悬停在任何一个条上会显示确切的窗口标题。

这个视图有点密集，让我逐一解释：

- **备注**功能（顶部）允许我为一天中的任何时间输入任意备注。注意我还写了一个（可选的）功能，查找关于咖啡的备注并根据咖啡的*实际*半衰期计算我的咖啡因水平。我很好奇咖啡因对我的生产力有什么影响！
- 我将窗口分组为*显示组***条形码**，其中第一组涉及娱乐（Gmail/Chrome/在 Sublime Text 2 中打开的非代码文件——如用于写博客的 *.markdown*），第二组涉及工作（Matlab/IPython Notebook、.js/.css/.cpp/.h/.py 文件，或打开的 PDF 文件（论文））。看起来我大约有一半的时间花在工作上。
- **编码持续时段**是一个巧妙的功能，它尝试识别连续的编码活动，并与我的生产力有合理的相关性。它寻找构成工作的活动窗口（我在设置中定义），然后寻找高于某个击键频率阈值的连续击键。这表示我处于*编码状态*，如果我切换到非工作标题的窗口，或者如果我停止写代码，持续时段会逐渐中断。这里看到的最长的一个是 22 分钟，当我悬停在那时活动标题上时，我看到是我在给 *ulogme* 添加功能。我见过最长的是一个实验室伙伴测试用户，有一个激烈的 50 分钟编码持续时段。

最后，ulogme 显示了当天占据我时间的标题的最终分解：

![](https://karpathy.github.io/assets/ulogme_sv4.jpeg)

活动窗口标题的最终分解。

这很有趣，看起来我实际上只花了 10% 的时间在 Gmail 上。所以即使我写了很多，也只是几封快速发出的邮件和聊天信息。

### ulogme 快速浏览：全局概览

一天的见解很有趣，但当放在大量日期的背景下时，一切就变得更有意义了。你可能注意到了头部的*"概览"*链接；点击它会带你到 ulogme 的概览页面，它将所有日期的统计数据汇总在一起。我现在已经记录了将近 3 个月的活动。以下是整个期间的可视化数据（附有一些叠加注释）：

![](https://karpathy.github.io/assets/ulogme_mv1.jpeg)

三个月内每天花在各种应用程序上的总时间。顶部的标题是可点击的，可以打开/关闭任何一个标题的可视化。

太棒了。有许多有趣的事情值得注意：

- 注意 6 月 6 日 NIPS 论文截止日期前的**截止日期模式**。我当时大部分时间在疯狂地写 LaTeX : )
- 截止日期后不久，你可以看到活动量的下降。这是因为我当时主要在我的笔记本电脑上准备 CVPR 会议的材料，我需要在上面做演讲。这指向了 *ulogme* 的一个问题——目前没有跨机器的同步。
- 注意几个周日的下降——显然周日是我的休息日 : )
- 是我产生了幻觉，还是在休息之后活动量有相当显著的跃升（注意 CVPR 和假期之后的高条）。这需要更多数据，但如果假期实际上让我更有效率，那将会很有趣。不过，我们需要衡量的不仅仅是花在电脑上的时间。
- 当我关闭所有非工作标题时，可视化（未展示）显示，我*实际上*花在工作上的时间少得令人沮丧。很多天我早上来实验室，晚上很晚才离开直接去睡觉，但即使是这些天，实际编码时间加起来也只有大约 5-6 小时。一开始我非常惊讶，去查找了 bug，但仔细检查后发现这是真的——有短途通勤、午餐、晚餐、随机读书会、会议、随机的在网上摸鱼、Gmail 等等等等……时间累积得很快！看到这样量化的结果令人沮丧。

接下来，ulogme 给出了击键次数和花在每个窗口上的时间的很好分解，覆盖所有时间：

![](https://karpathy.github.io/assets/ulogme_mv2.jpeg)

全部三个月内每个窗口的击键和时间汇总。

这有点不完整，因为我有时在笔记本电脑上编码，但它仍然描绘了一幅有趣的画面。看起来我花了很多桌面时间在 Matlab 上，但似乎在 Chrome 上消磨和浏览互联网上花的时间最多。太棒了。

**写一篇论文需要什么。** 有趣的是，我在 LaTeX 上的总时间是 **35** 小时——这就是写一篇论文需要的时间！此外，我在 LaTeX 编辑器中按下了 **225,149** 次键，而我的论文 `.tex` 文件上的 `$ wc -l` 显示它有 **40,192** 个字符。其中一些是模板代码，但至少大约来说，这意味着最终论文中的每个字符需要输入约 **5.6** 个字符！

> 写一篇 40,192 个字符的 NIPS 论文需要 35 小时和 225,149 次击键（即每输出一个最终字符，需要输入 5.6 个字符。）

最后的可视化太长了无法完整粘贴在这里，但我会展示一个片段：

![](https://karpathy.github.io/assets/ulogme_mv3.jpeg)

每天的可视化击键频率，顶部和右侧有边际总和。

这个可视化似乎表明我大部分工作在上午 10 点到晚上 8 点之间完成，一个高效的一天大约是 50,000 次击键。你还可以看到我在 NIPS 后的一段休整期，击键活动明显减少。

最后，ulogme 告诉我，在过去 3 个月里，我在 **83** 天内总共按下了 **1,608,943** 次键，平均每天约 **19,384** 次。

### 展望未来

展望未来，我希望将 ulogme 打造成一个漂亮的开源个人项目。代码全部在 [Github](https://github.com/karpathy/ulogme) 上以 *MIT License* 提供，欢迎任何人尝试（如果你用的是 Ubuntu 或 OSX——Windows 不支持，并且你使用的是现代浏览器）。

如果你觉得特别有冒险精神，我热烈欢迎针对新功能或 bug 修复的 pull request。代码库是 Python 和 Javascript 的混合，我使用 [d3.js](http://d3js.org/) 进行所有可视化。项目还处于相当早期的阶段，代码不是我写过的最漂亮的，但我已经开始进行相当大规模的重构工作，以使上手过程更容易。

长期来看，我希望 ulogme 代码库将演变成一组精美的模块化*数据视图插件*，可以按需在用户界面中进行定制、堆叠和组合。

总之，我觉得仅仅通过可视化数据，我就对自己的工作习惯获得了很多见解，但在分析方面还有很多工作要做。这里的圣杯尚未实现：我生产力的相关因素是什么？睡得多有帮助吗？喝咖啡有帮助吗？度假或休息有任何帮助吗？所有这些问题都有答案，我迫不及待地想在数据中找到它们。

---

*English original below:*

I'm always on a lookout for interesting datasets to collect, analyze and interpret. And what better dataset to collect/analyze than the *meta-dataset* of my own activity collecting/analyzing other datasets? How much time do I *\*really* spend working per day? How do I spend most of that time? What makes me productive? These are all relatively important questions that I'd like answers to, and since I prefer my answers based on data and not confirmation-bias-susceptible personal anecdotes, I wrote [ulogme](https://github.com/karpathy/ulogme).

> "I prefer my answers based on data, not confirmation-bias-susceptible personal anecdotes"

I've now collected my computer usage data over a period of almost **3 months**. In this post I'll highlight some of the features of the project, some of the insights I was able to derive so far and some thoughts about where I hope I can take it next. And who knows, maybe by the end of the post you'll want to become a user yourself:)

### What's out there already

The idea of tracking and visualizing your computer activity is not at all new. It has been around in various shapes and forms in [Quantified Self](http://en.wikipedia.org/wiki/Quantified_Self) circles and several programs already exist that try to fill this need. Among the few better known ones are [RescueTime](https://www.rescuetime.com/) and [Toggl](https://www.toggl.com/), but there are literally tens to hundreds of other quite terrible copies. Among all of these, I couldn't find anything that satisfies a few very simple, basic requirements:

- The user interface must be **web-based** because it's 2014
- Everything must be **open source** and **free**
- The data must never leave the **local machine** (No cloud mambo jambo - too personal!)
- It must be easily **customizable** and look **pretty**

Nothing like this (by far, actually) exists, so I set out to implement my own solution.

### Brief Tour of ulogme: Single Day View

ulogme is small and simple: There are two *backend* components: a tracking script that records activity and a small local web server wrapper that serves the activity logs to the *frontend* (visualization pages). The tracking script currently records active window titles (at frequency of once every 2 seconds) and keystroke typing frequency.

Lets go through a brief overview of some of the resulting visualizations and features. First there is the **single day view**. Lets look at my August 1st, for example. The header tells us the day of the recording and there is space for a short "blog" post that can be written up for each day:

![](https://karpathy.github.io/assets/ulogme_sv1.jpeg)

Header: day information, refresh button, buttons for going between days, and a little editable "blog" post for the day.

Now we start to get to the meat. It looks like I was in the office from 10AM to 8PM on this day. Now, remember that we record keystrokes and window titles throughout. What follows is the keystroke breakdown for the day:

![](https://karpathy.github.io/assets/ulogme_sv2.jpeg)

Keystroke statistics for the day.

We see that I spent most of the day coding in Sublime Text 2 (which I use to write Python/JS/C++) and Gmail - Looks like I wrote quite a bit of email! Next, ulogme shows the *barcode of the day*, as I like to call it. This is a breakdown of all the windows on that day:

![](https://karpathy.github.io/assets/ulogme_sv3.jpeg)

Barcode of the day. Mousing over any of these strips reveals the exact window title.

This view is a little dense so let me unpack it one by one:

- The **Notes** feature (on top) allows me to enter arbitrary notes for any time of day. Notice I also wrote an (optional) feature that looks for notes about coffee and calculates my levels of caffeine based on *actual* half-life of coffee. I am curious what caffeine does to my productivity!
- I group my windows into *display groups* **barcodes**, where the first group involves fun (Gmail/Chrome/Non-coding files opened in Sublime Text 2 - such as *.markdown* for blogging) and the second the group involves work (Matlab/Ipython Notebook with.js/.css/.cpp/.h/.py files, or PDF files opened (papers)). Looks like I spent roughly half of the day on work.
- **Hacking Streak** is a nifty feature that tries to identify contiguous hacking activity and correlates reasonably with my productivity. It looks for active windows that constitute work (I define this in settings) and then for continuous keystrokes above some typing frequency threshold. This indicates that I'm in a state of *hacking*, and the streak gets gradually interrupted if I switch windows to non-working titles, or if I stop writing code. The longest one visible here was 22 minutes and when I hover over the active title at that time, I see that it was me adding a feature to *ulogme*. The longest I've seen anyone get is a lab mate beta tester friend with an intense 50-minute hacking streak.

In the end, ulogme shows the final breakdown of titles that occupied me on this day:

![](https://karpathy.github.io/assets/ulogme_sv4.jpeg)

The final breakdown of active window titles.

That's interesting, it looks like I actually only spent 10% of my day in Gmail. So even though I wrote a lot, it was just a few emails and chats I quickly sent out.

### Brief Tour of ulogme: Global Overview

Insights for one day are interesting, but everything becomes signficantly more meaningful when it is put in context of a large number of days. Perhaps you noticed the *"Overview"* link on the header; Clicking this takes you to the overview page of ulogme that takes the statistics for all days and puts them together. I recorded my activity for almost 3 months now. Here is the delicious data visualized for the entire period (with some overlayed annotations):

![](https://karpathy.github.io/assets/ulogme_mv1.jpeg)

Total amount of time per day spent in various applications over a period of three months. The titles on top are clickable and toggle on/off the visualization of any one of the titles.

SO AWESOME. There are many fun things to note:

- Note the **deadline mode** right before NIPS paper deadline on June 6th. I was frantically writing Latex for the most part:)
- Right after the deadline, you see a dip in activity. This is because I was mostly on my laptop preparing things for the CVPR conference where I had to give a talk. This points to one issue with *ulogme* - there is no syncing across machines right now.
- Notice a few dips on Sundays – apparently Sundays are my rest days:)
- Am I just hallucinating this, or is there a fairly significant jump in activity right after breaks (note very high bars right after CVPR and vacation.) This needs more data but it would be interesting if vacations actually made me more productive. We'd have to measure more than just time spent on computer, though.
- When I toggle off all non-working titles, the visualizaiton (not shown) reveals that I only spend somewhat depressingly little time *actually* working. Many days I come into lab in the morning and leave late at night to go straight to sleep, but even these days sometimes add up to only roughly 5-6 hours of actual coding. I was very surprised about this initially and went looking for bugs, but it is true upon closer inspection - there is a short commute, lunch, dinner, random reading groups, meetings, random slacking off on the internet, gmail, etc etc… it all builds up quite quickly! Depressing to see that quantified.

Next, ulogme gives me nice breakdown for both keystrokes and time spent in every window, across all time:

![](https://karpathy.github.io/assets/ulogme_mv2.jpeg)

Summary of keys and time per window across all 3 months.

This is a little incomplete because I do some hacking on my laptop, but it paints an interesting picture nonetheless. It looks like I spent a good chunk of desktop time in Matlab, but seemingly I spend the most amount of time in Chrome screwing around and browsing the internet. Great.

**What it takes to write a paper.** Note that, interestingly, my total time for Latex is **35** hours - this is how long it takes to write a paper! Additionally, I pressed **225,149** keys in my Latex editor and the `$ wc -l` on my paper `.tex` file reveals that it has **40,192** characters. Some of it is template code but, at least approximately, this means that it takes about **5.6** characters for every one character in the final paper!

> It takes 35 hours and 225,149 keys to write a 40,192-character NIPS paper (i.e. 5.6 characters must be typed for every one final character.)

The final visualization is too long to paste here entirely, but I will show a snippet:

![](https://karpathy.github.io/assets/ulogme_mv3.jpeg)

Keystroke frequencies visualized for every day, along with the marginal sums on top and right.

This visualization seems to suggest that I do most of my work between 10AM and 8PM, and a very productive day is about 50,000 keystrokes. You can also see a bit of my post-NIPS refactory period with much lower keystroke activity.

In the end, ulogme tells me that over the last 3 months I've pressed a total of **1,608,943** keys over **83** days, or approximately **19,384** per day.

### Going forward

Going forward, I'm hoping to make ulogme into a nice, open-sourced pet project. The code is all available on [Github](https://github.com/karpathy/ulogme) under *MIT License* and anyone is welcome try it out (if you're on Ubuntu or OSX - Windows is not supported, and if you're using a modern browser).

And if you're feeling extra adventurous, I warmly welcome pull requests for new features or bug fixes. The code base is a mix of Python, Javascript and I use [d3.js](http://d3js.org/) for all visualizations. The project is in fairly early stages and the code is not among the nicest I've produced, but I've started fairly major refactoring efforts to make the onboarding process easier.

In longer term, I'm hoping that ulogme codebase will evolve to become beautifully modular set of *data view plugins* that could be customized, stacked up and composed in the user interface as desired.

Im summary, I feel I've gained quite a few insights into my own work habits by just visualizating the data, but there is much more work to be done on the analysis side as well. The holy grail here is still not implemented: What are the correlated of my productivity? Does sleeping more help? Does drinking coffee help? Do vacations or breaks help at all? All of these questions have answers and I can't wait to find them, in the data.