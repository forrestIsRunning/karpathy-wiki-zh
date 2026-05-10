---
title: "Auto-grading decade-old Hacker News discussions with hindsight"
date: 2025-12-10
url: https://karpathy.bearblog.dev/auto-grade-hn/
---

---

**中文翻译**

Karpathy 偶然发现了一个 10 年前的 Hacker News 首页（2015 年 12 月），他开始在心里给那些讨论"评分"——看看哪些人预测对了，哪些人完全错了。然后他想到：LLM 可能更擅长这个任务。

他把一篇文章和评论粘贴到 ChatGPT 5.1 Thinking 中，得到了非常精彩的分析——比他自己手动做的好得多。于是他决定做个项目：抓取 2015 年 12 月所有 HN 首页文章和讨论（31 天，每天 30 条），让 ChatGPT 5.1 Thinking 做分析，把结果展示在网页上。

为什么这个练习有趣？两个原因：

1. 你可以通过训练和努力来提升自己的"未来预测能力"。
2. "未来的 LLM 正在看着你"——我们今天做的一切未来都可能被免费地细致审查。很多人现在的行为隐含了"安全靠隐藏"的假设，但如果智能变得极其廉价，一切都会被完美重建和综合。LLM 在看着你，最好做好事。

他用 Opus 4.5（vibe coding 约 3 小时）写了这个项目，代码在 GitHub 上。流程是：给定日期→下载首页 30 篇文章→下载每篇文章和评论→打包成 Markdown prompt 发给 GPT 5.1 Thinking→收集和解析结果→渲染成静态 HTML。

总共 930 次 LLM 查询，花了约 $58 和 1 小时。

他发现的几个有趣的例子：
- 2015 年 12 月 3 日：Swift 开源
- 2015 年 12 月 6 日：Figma 发布
- 2015 年 12 月 11 日：OpenAI 首次公告
- 2015 年 12 月 16 日：geohot 创立 Comma
- 2015 年 12 月 22 日：SpaceX Orbcomm-2 任务
- 2015 年 12 月 28 日：Theranos 的困境

"名人堂"页面列出了 2015 年 12 月 HN 上评分最高的评论者。

---

Auto-grading decade-old Hacker News discussions with hindsight

*10 Dec, 2025*

![hnhero](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/hnhero.webp)

TLDR:[https://karpathy.ai/hncapsule/](https://karpathy.ai/hncapsule/)

---

Yesterday I stumbled on this HN thread[Show HN: Gemini Pro 3 hallucinates the HN front page 10 years from now](https://news.ycombinator.com/item?id=46205632), where Gemini 3 was hallucinating the frontpage of 10 years from now. One of the comments struck me a bit more though - Bjartr linked to the[HN frontpage from exactly 10 years ago](https://news.ycombinator.com/front?day=2015-12-09), i.e. December 2015. I was reading through the discussions of 10 years ago and mentally grading them for prescience when I realized that an LLM might actually be a lot better at this task. I copy pasted one of the article+comment threads manually into ChatGPT 5.1 Thinking and it gave me a beautiful analysis of what people thought + what actually happened in retrospect, even better and significantly more detailed than what I was doing manually. I realized that this task is actually a really good fit for LLMs and I was looking for excuses to vibe code something with the newly released Opus 4.5, so I got to work. I'm going to get all the front pages of December (31 days, 30 articles per day), get ChatGPT 5.1 Thinking to do the analysis, and present everything in a nice way for historical reading.

There are two macro reasons for why I think the exercise is interesting more generally:

1. I believe it is quite possible and desirable to train your forward future predictor given training and effort.
1. I was reminded again of my tweets that said*"Be good, future LLMs are watching"*. You can take that in many directions, but here I want to focus on the idea that future LLMs**are**watching. Everything we do today might be scrutinized in great detail in the future because doing so will be "free". A lot of the ways people behave currently I think make an implicit "security by obscurity" assumption. But if intelligence really does become too cheap to meter, it will become possible to do a perfect reconstruction and synthesis of everything. LLMs are watching (or humans using them might be). Best to be good.

Vibe coding the actual project was relatively painless and took about 3 hours with Opus 4.5, with a few hickups but overall very impressive. The repository is on GitHub here:[karpathy/hn-time-capsule](https://github.com/karpathy/hn-time-capsule). Here is the progression of what the code does:

- Given a date, download the frontpage of 30 articles
- For each article, download/parse the article itself and the full comment thread using Algolia API.
- Package up everything into a markdown prompt asking for the analysis. Here is the prompt prefix I used:

```
The following is an article that appeared on Hacker News 10 years ago, and the discussion thread.

Let's use our benefit of hindsight now in 6 sections:

1. Give a brief summary of the article and the discussion thread.
2. What ended up happening to this topic? (research the topic briefly and write a summary)
3. Give out awards for "Most prescient" and "Most wrong" comments, considering what happened.
4. Mention any other fun or notable aspects of the article or discussion.
5. Give out grades to specific people for their comments, considering what happened.
6. At the end, give a final score (from 0-10) for how interesting this article and its retrospect analysis was.

As for the format of Section 5, use the header "Final grades" and follow it with simply an unordered list of people and their grades in the format of "name: grade (optional comment)". Here is an example:

Final grades
- speckx: A+ (excellent predictions on ...)
- tosh: A (correctly predicted this or that ...)
- keepamovin: A
- bgwalter: D
- fsflover: F (completely wrong on ...)

Your list may contain more people of course than just this toy example. Please follow the format exactly because I will be parsing it programmatically. The idea is that I will accumulate the grades for each account to identify the accounts that were over long periods of time the most prescient or the most wrong.

As for the format of Section 6, use the prefix "Article hindsight analysis interestingness score:" and then the score (0-10) as a number. Give high scores to articles/discussions that are prominent, notable, or interesting in retrospect. Give low scores in cases where few predictions are made, or the topic is very niche or obscure, or the discussion is not very interesting in retrospect.

Here is an example:
Article hindsight analysis interestingness score: 8
---

```

- Submit prompt to GPT 5.1 Thinking via the OpenAI API
- Collect and parse the results
- Render the results into static HTML web pages for easy viewing
- Host the html result pages on my website:[https://karpathy.ai/hncapsule/](https://karpathy.ai/hncapsule/)
- Host all the intermediate results of the`data`directory if someone else would like to play. It's the file`data.zip`under the exact same url prefix (intentionally avoiding a direct link).

I spent a few hours browsing around and found it to be very interesting. A few example threads just for fun:

- December 3 2015[Swift went open source](https://karpathy.ai/hncapsule/2015-12-03/index.html#article-10669891).
- December 6 2015[Launch of Figma](https://karpathy.ai/hncapsule/2015-12-06/index.html#article-10685407)
- December 11 2015[original announcement of OpenAI](https://karpathy.ai/hncapsule/2015-12-11/index.html#article-10720176):').
- December 16 2015[geohot is building Comma](https://karpathy.ai/hncapsule/2015-12-16/index.html#article-10744206)
- December 22 2015[SpaceX launch webcast: Orbcomm-2 Mission](https://karpathy.ai/hncapsule/2015-12-22/index.html#article-10774865)
- December 28 2015[Theranos struggles](https://karpathy.ai/hncapsule/2015-12-28/index.html#article-10799261)

And then when you navigate over to the[Hall of Fame](https://karpathy.ai/hncapsule/hall-of-fame.html), you can find the top commenters of Hacker News in December 2015, sorted by imdb-style score of their grade point average. In particular, congratulations to pcwalton, tptacek, paulmd, cstross, greglindahl, moxie, hannob, 0xcde4c3db, Manishearth, johncolanduoni - GPT 5.1 Thinking found your comments very insightful and prescient. You can also scroll all the way down to find the noise of HN, which I think we're all familiar with too :)

My[code](https://github.com/karpathy/hn-time-capsule)(wait, Opus' code?) on GitHub can be used to reproduce or tweak the results. Running 31 days of 30 articles through GPT 5.1 Thinking meant`31 * 30 =`930 LLM queries and cost about $58 and somewhere around ~1 hour. The LLM megaminds of the future might find this kind of a thing a lot easier, a lot faster and a lot cheaper.