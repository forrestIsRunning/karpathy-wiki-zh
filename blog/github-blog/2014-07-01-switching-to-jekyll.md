受到 [Mark Reid](https://twitter.com/mdreid) 的博文 [从 Jekyll 切换到 Hakyll](http://mark.reid.name/blog/switching-to-hakyll.html) 的启发，我决定放弃 Wordpress，尝试一下 Jekyll（注意，我现在还觉得自己不够高手去切换到基于 Haskell 的 Hakyll）。我可以自信地说，我对这个决定再满意不过了。

### Wordpress 怪兽

*"Wordpress 有什么问题？"* 你可能会问。让我们看看，全是问题：

- Wordpress 博客笨重、缓慢且臃肿。
- Wordpress 使用 **.php** 动态渲染。实际上只有少数小众应用需要这样做。动态代码执行让你的博客暴露给黑客和漏洞利用：零日攻击、病毒等。我自己的博客大约两个月前被黑，我所有的文章都被注入了垃圾内容，我删除后它们又神奇地重新出现了。
- Wordpress 在广大不知道还有其他选择的人群中很流行，因此吸引了最大数量的垃圾评论发送者。
- 你的文章永远被困在一个丑陋的、Wordpress 特有的 SQL 数据库里（yuck）。你不能轻松地导入/导出文章。你并没有真正以原始、灵活的形式拥有你的内容。
- Wordpress 在中国被屏蔽。

> Wordpress 是一个臃肿、笨重、缓慢、易受攻击、封闭的烂摊子。

### Jekyll <3

[Jekyll](http://jekyllrb.com/) 将自己描述为构建*"简单、博客感知的静态网站"*的工具，最初由 Github 的联合创始人之一 [Tom Preston-Werner](http://tom.preston-werner.com/) 编写。它是扁平且透明的：你的博客工作空间是一个包含配置文件的文件夹，以及几个用于 CSS 和 HTML 模板的文件夹。例如，我所有的内容存放在两个文件夹中：

1. 我的博客文章只是 `_posts` 文件夹中的文件，用 [Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) 编写。当然，包括这篇文章本身。
2. 我的图片都在一个 `assets` 文件夹中。

就这样。你在命令行调用 `$ jekyll build`，它会自动将 `_posts` 文件夹中找到的所有文章从 markdown 渲染成 HTML，用页头/页脚模板包装起来，创建列出所有文章的父索引页面，并将所有内容输出到 `_site` 目录。`_site` 目录保存着你整个网站的所有静态内容。然后可以将其上传到你喜欢的任何网络服务器。

整个代码库只有大约 7 个文件。很容易看出 HTML 模板是如何组合成你的最终网站的。调整 CSS 或任何 HTML 模板都非常简单。例如，我通过修改 HTML 模板为所有页面添加了 **Google Analytics** 跟踪代码，并通过修改文章模板添加了 Disqus Javascript 代码来为所有文章添加 **Disqus** 评论功能。

#### Github 集成

最后，正如你所料，Jekyll 与 Github 紧密集成：创建一个类似 `username.github.io` 的仓库，并将你的文件添加到该仓库。Github 会自动用 Jekyll 编译你的文件，并使 `_site` 文件夹可用。例如，我的博客在 [karpathy.github.io](http://karpathy.github.io/)。因此，Github 确保你的博客**永久备份在简单的 markdown 中**，并且**托管你的内容**！

> Jekyll 取得了完美的平衡：它提供了恰到好处的功能。

#### 工作流程示例

为了让你感受一下工作流程，我要添加一篇新博文时会执行以下操作：

```bash
$ cd _posts
$ vim 2014-07-02-example-page.markdown
```

现在我们在 markdown 中写博文，下面是一个示例文件：

```bash
---
layout: post
title:  "Post title"
excerpt: "A nice post"
date:   2014-07-02 10:00:00
---

Hello world, this is **markdown**.
```

让我们现在回到控制台。我可以用 `$ jekyll serve --watch` 在本地 Web 服务器上预览更改（watch 开关会在你写文件时刷新任何更新的文件）。现在让我们直接推送上线：

```bash
$ cd ..
$ git add .
$ git commit -m "new blog post"
$ git push
```

执行最后一个命令后，Github 会检测到我的仓库已更改，并自动刷新 [karpathy.github.io](http://karpathy.github.io/)，使其指向新生成的 `_site`。我的文章上线了！

总之，这只是一个小小的尝鲜。去看看 [Jekyll](http://jekyllrb.com/) 吧，用一种更健康的方式开始写博客！

---

*English original below:*

Inspired by [Mark Reid's](https://twitter.com/mdreid) blog post [Switching from Jekyll to Hakyll](http://mark.reid.name/blog/switching-to-hakyll.html) I decided to abandon Wordpress and give Jekyll a try (note, I currently do not yet feel pro enough to switch to Haskell-based Hakyll). I can confidently say that I could not be happier about this decision.

### Wordpress Monster

*"So what's wrong with Wordpress?"* You may ask. Let's see, everything:

- Wordpress blogs are clunky, slow and bloated.
- Wordpress is dynamically rendered with **.php**. There are really only few niche applications where this is necessary. Dynamic code execution exposes your blog to hackers and exploits: zero-day attacks, viruses, etc. My own blog was hacked ~2 months ago and all my posts had been infected with spammy content that kept re-inserting itself magically when I removed it.
- Wordpress is popular among the masses of people who don't know any better, and therefore attracts the largest amount of spammers.
- Your posts are stuck forever in an ugly, Wordpress-specific SQL database (ew). You can't easily import/export posts. You do not really own your content in raw and nimble form.
- Wordpress is blocked in China.

> Wordpress is a bloated, clunky, slow, vulnerable, closed mess.

### Jekyll <3

[Jekyll](http://jekyllrb.com/) describes itself as a tool for building *"Simple, blog-aware, static sites"*, and was originally written by one of the Github co-founders, [Tom Preston-Werner](http://tom.preston-werner.com/). It is flat and transparent: Your blog workspace is a single folder with a config file, and a few folders for CSS and HTML templates. All my content, for example, lives in two folders:

1. My blog posts are just files in a single folder `_posts`, written in [Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet). Including this post, of course.
2. My images are in a single folder `assets`.

That's it. You call `$ jekyll build` from command line and it will automatically render all posts it finds in your `_posts` folder from markdown to HTML, wraps it with header/footer templates, creates the parent index page that lists all your posts and outputs everything into a directory `_site`. The `_site` directory holds your entire webpage as static content. It can then be uploaded to a webserver wherever you like.

The entire code base consists of like 7 files. It's easy to see how the HTML templates get composed to your final site. It's trivial to tweak the CSS or any of the HTML templates. For example, I added **Google Analytics** tracking code to all my pages by tweaking the html template, and also **Disqus** comments to all my posts by tweaking the posts template with the Disqus Javascript code.

#### Github integration

Lastly, as you might expect Jekyll is tightly integrated with Github: create a repository that looks like `username.github.io` and add your files to the repo. Github will automatically compile your files with Jekyll and make the `_site` folder available. For example, mine lives on [karpathy.github.io](http://karpathy.github.io/). Thus, Github makes sure that your blog is beautifully backed up **forever in simple markdown**, and also **hosts your content**!

> Jekyll strikes the balance: It's packed with just the right amount of features.

#### Example workflow

To give a flavor for the workflow, to add a new blog post I proceed as follows:

```bash
$ cd _posts
$ vim 2014-07-02-example-page.markdown
```

Now we write the blog post in markdown, here's an example file:

```bash
---
layout: post
title:  "Post title"
excerpt: "A nice post"
date:   2014-07-02 10:00:00
---

Hello world, this is **markdown**.
```

Lets pop back out to console now. I could preview the changes in a local webserver with `$ jekyll serve --watch` (the watch switch refreshes any updated files as you write them). Now let's just push it live:

```bash
$ cd ..
$ git add .
$ git commit -m "new blog post"
$ git push
```

After the last command, Github will see that my repo has changed and automatically refreshes [karpathy.github.io](http://karpathy.github.io/) to point to the newly generated `_site`. My post is live!

Anyway, that's just a brief taste. Check out [Jekyll](http://jekyllrb.com/) and get blogging in a sane way!