### 量化 Hacker News

我觉得分析我最喜欢的有趣链接和信息来源之一 [Hacker News](https://news.ycombinator.com/) 上的活动会很有趣。我的数据来源是一个我八月份设置的脚本，它每隔一分钟下载一次 HN（首页和新故事页面）。我们会感兴趣的是：可视化故事在一天中如何被点赞；找出哪些域名/用户最受欢迎；哪些话题最热门；以及发布故事的最佳时间。我公开所有数据和代码（Python 数据收集脚本 + IPython Notebook 分析代码），以便你也可以进行类似的分析。

### 数据收集协议

我设置了非常简单的 Python 脚本，每隔一分钟抓取 HN 的**首页**和**新故事页面**。一天的数据从凌晨 4 点（PST）开始，到第二天凌晨 4 点结束。HTML 文件被压缩保存为 gzipped pickle 格式，一天的数据大约占用 10MB。我中途有几次关闭了机器几天，所以数据中存在一些空缺，但最终我们得到了从 8 月 22 日到 10 月 30 日期间的 47 天数据。

### 原始 HTML 数据解析

解析 Python 脚本使用 **BeautifulSoup** 将原始 HTML 转换为更结构化的 JSON。顺便说一句，这个脚本写起来可一点都不简单——HN 基于无格式表格，我不得不一路上发现许多奇怪的特殊情况。最后我写了一个 100 行的有史以来最丑陋的解析函数（真的，我都不好意思了），但它能工作，对某个快照中的单个故事输出如下内容：

```
{
'domain': u'play.google.com', 'title': u'Nexus 5', 
'url': u'https://play.google.com/store/devices/details?id=nexus_5_black_16gb', 
'num_comments': 42, 'rank': 1, 'points': 65, 
'user': u'sonier', 'minutes_ago': 39, 'id': u'6648519'
}
```

我们每分钟获得 60 条这样的条目（30 条来自首页，30 条来自新页面），这些都被保存到磁盘上。现在我们准备好拿出 IPython Notebook 来进行有料的分析了！

### 分析：详细分析

请访问 [渲染为 HTML 的 IPython Notebook](http://cs.stanford.edu/people/karpathy/hn_analysis.html) 查看分析内容：

[![](https://karpathy.github.io/assets/hn.jpg "hn")](http://cs.stanford.edu/people/karpathy/hn_analysis.html)

注意：我原本提供了完整数据集和 .ipynb IPython Notebook 源代码可供下载，但最近为了节省主机空间而将其下架了（抱歉）。

---

*English original below:*

### Quantifying Hacker News

I thought it would be fun to analyze the activity on one of my favorite sources of interesting links and information, [Hacker News](https://news.ycombinator.com/). My source of data is a script I've set up some time in August that downloads HN (the Front page and the New stories page) every minute. We will be interested in visualizing the stories as they get upvoted during the day, figuring out which domains/users are most popular, what topics are most popular, and the best time to post a story. I'm making all my data and code (Python data collection scripts + IPython Notebook for analysis) available in case you'd like to carry out a similar analysis.

### Data collection protocol

I set up a very simple python script that scrapes the HN **front page** and the **new stories page** every minute. A single day of data begins at 4am (PST) and ends at 4am the next day. The.html files are saved compressed as gzipped pickles and one day occupies roughly 10mb in this format. I had bring down my machine for a few days a few times so there are some gaps in the data, but in the end we get 47 days of data from period between August 22 and October 30.

### Raw HTML data parsing

The parsing Python script uses **BeautifulSoup** to convert the raw HTML into a more structured JSON. This script was by the way by no means simple to write – HN is based on unstructured tables and I had to discover many strange edge cases in its behavior along the way. At the end I ended up with a 100-line ugliest-parsing-function-ever (really, I'm not proud of it) but it works and outputs something like the following for a single story at a specific snapshot:

```
{
'domain': u'play.google.com', 'title': u'Nexus 5', 
'url': u'https://play.google.com/store/devices/details?id=nexus_5_black_16gb', 
'num_comments': 42, 'rank': 1, 'points': 65, 
'user': u'sonier', 'minutes_ago': 39, 'id': u'6648519'
}
```

We get 60 such entries every minute (30 for front page and 30 for new page) and these are again all saved to disk. We are now ready to bring out the IPython Notebook and get to the juicy analysis!

### The Analysis: Detailed analysis

Head over to the IPython Notebook [rendered as HTML](http://cs.stanford.edu/people/karpathy/hn_analysis.html) for the analysis:

[![](https://karpathy.github.io/assets/hn.jpg "hn")](http://cs.stanford.edu/people/karpathy/hn_analysis.html)

Note: I had the entire dataset and.ipynb Ipython Notebook source available for download but recently took it down to save space on my host (sorry).