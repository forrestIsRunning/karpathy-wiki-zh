![](https://karpathy.github.io/assets/tsne_preview.jpeg)

我最近在研究将无标签高维数据嵌入到二维空间进行可视化的各种方法。针对这个任务，人们已经提出了多种多样的方法。[这篇 2009 年的综述论文](http://homepage.tudelft.nl/19j49/Matlab_Toolbox_for_Dimensionality_Reduction_files/TR_Dimensiereductie.pdf) 包含了其中许多方法的绝佳参考文献（PCA、Kernel PCA、Isomap、LLE、自编码器等）。如果你有 MATLAB，[降维工具箱](http://homepage.tudelft.nl/19j49/Matlab_Toolbox_for_Dimensionality_Reduction.html) 提供了其中许多方法的良好实现。Scikit Learn 也有一小节关于[流形学习](http://scikit-learn.org/stable/modules/manifold.html)的内容及相关实现。

在这些算法中，t-SNE 因其优美直观的公式、简单的梯度和优良的特性而突出。这里有一个 Laurens van der Maaten（作者本人）解释该方法的 [Google Tech Talks 视频](http://www.youtube.com/watch?v=RJVL80Gg3lA)。我决定从头重新实现 t-SNE，因为这样做是我所知道的最好的学习方式，而用什么语言实现最好呢——当然是 Javascript！:)

长话短说，我用 JS 实现了 t-SNE，以 [tsnejs](https://github.com/karpathy/tsnejs) 的形式发布在 Github 上，并创建了一个小演示，用这个库基于谈论内容来可视化顶级 Twitter 账号。在这篇文章中，我想记录一下这样一个为期一天的小项目，从头到尾的过程。这也给了我一个机会来描述我的一些项目工具箱，这些可能对其他人也有用。

### 最终演示

首先，看一下[最终演示](http://cs.stanford.edu/people/karpathy/tsnejs/)。为了创建这个演示，我找到了 Twitter 上关注数最高的 500 个账号，下载了他们各 200 条推文，然后衡量他们推文内容的差异。这些差异随后被输入到 t-SNE 中，以生成二维可视化，其中位置相近的人发推的内容也相似。有趣！

### 获取顶级推主

我们首先要确定前 500 名推主。我搜索了"top twitter accounts"，找到了 http://twitaholic.com/，上面列出了它们。然而，这些账号嵌入在网页中，我们需要以结构化格式提取它们。为此，我喜欢使用最近出现的 YC 创业公司 [Kimono](https://www.kimonolabs.com/)；我大量使用它从网站抓取结构化数据。它让你点击感兴趣的元素（这里是 Twitter 用户名），并以 JSON 格式提取它们。易如反掌！

### 收集推文

现在我们有了前 500 名推主的列表，我们想获取他们的推文以了解他们谈论什么。我选择用于此任务的库是 [Tweepy](https://github.com/tweepy/tweepy)。他们的文档相当糟糕，但如果你浏览源代码，事情似乎相对简单。以下是一个为给定用户获取 200 条推文的示例调用：

```python
tweets = tweepy.Cursor(api.user_timeline, screen_name=user).items(200)
```

我们对所有用户进行迭代，提取推文文本，并将其全部转储到文件中，每个账号一个文件。在这个过程中我不得不小心处理两个烦人的问题：

- Twitter 对 API 调用设置了严格的速率限制，所以这实际上花了几个小时来收集，期间充满了 try catch 块和 `time.sleep` 调用。
- 返回的文本是 Unicode 编码的，如果你试图将其写入文件，就会遇到麻烦。

针对第二个烦恼的一个解决方法是使用 codecs 库：

```python
import codecs
codecs.open(filename, 'w', 'utf-8').write(tweet_texts)
```

哦，让我们也获取并保存 Twitter 头像，我们将在可视化中使用它们。一个用户的示例如下：

```python
import urllib # 是的我知道这个已弃用
userobj = api.get_user(screen_name = user)
urllib.urlretrieve(imgname, userobj.profile_image_url) # 将图片保存到磁盘
```

我应该提一下，我写了很多快速且粗糙的 Python 代码，都在 [IPython Notebooks](http://ipython.org/notebook.html) 中，我强烈推荐。如果你还在用文本编辑器写所有的 Python 代码，你真的错过了很多。

### 量化推主差异

我们现在有 500 个推主和他们各自最近的 200 条推文，拼接在 500 个文件中。我们想知道谁在谈论相似的话题。[Scikit learn](http://scikit-learn.org/stable/) 非常适合这类快速的 NLP 任务。具体来说，我们加载所有文件并创建一个 500 元素的数组，其中每个元素是拼接后的 200 条推文。然后我们使用 [TfidfVectorizer](http://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html) 类从文本数据中提取所有单词和双词组，并将每个用户的语言转换为一个 tfidf 向量。这个向量是每个人使用语言的指纹。以下是我们如何简单地实现：

```python
from sklearn.feature_extraction.text import CountVectorizer,TfidfVectorizer
vectorizer = TfidfVectorizer(min_df=2, stop_words = 'english',\
strip_accents = 'unicode', lowercase=True, ngram_range=(1,2),\
norm='l2', smooth_idf=True, sublinear_tf=False, use_idf=True)
X = vectorizer.fit_transform(user_language_array)
D = -(X * X.T).todense() # Distance matrix: dot product between tfidf vectors
```

在上面的代码中，`user_language_array` 是一个 500 元素的数组，包含拼接后的推文。`TfidfVectorizer` 类遍历所有推文，并记录所有单词（unigrams）和双词词组（bigrams，即两个词的序列）。它用所有 unigram/bigram 构建一个字典，并基本统计每个人使用每个词/词组的频率。以下是一些推文文本转换为 unigram/bigram 的示例：

![](https://karpathy.github.io/assets/tsne_sentprepro.jpeg)

tfidf 向量以行的形式堆叠在 `X` 中，其大小为 `500 x 87,342`。这 87,342 个维度中的每一个都对应某个 unigram 或 bigram。例如，第 10,000 个维度可能对应 unigram "YOLO" 的使用频率。这些向量经过 L2 归一化，因此这些向量之间的点积与任意两个向量之间的夹角有关。这可以解释为语言的相似性。最后，我们将矩阵和用户名导出到 JSON 文件中，准备在 Javascript 中加载！

### 可视化部分

我们现在创建一个 .html 文件，并导入 [jQuery](http://jquery.com/)（一如既往）和 [d3js](http://d3js.org/)，我喜欢用它们来进行任何类型的绘图。我们用 jQuery 加载存储距离和用户名的 JSON，并用 d3js 初始化将容纳所有用户的 SVG 元素。开始时，我们将用户绘制在随机位置，但很快我们会用 t-SNE 排列它们，使相似的用户聚类在一起。查看[演示页面](http://cs.stanford.edu/people/karpathy/tsnejs/)的代码以了解 jQuery 和 d3js 部分（Ctrl+U）。在代码中，我们看到一些我喜欢使用的东西：

- 我喜欢使用 **Google Fonts** 来获得比默认字体更漂亮的字体。例如，这里我导入了 Roboto，然后在 CSS 中使用它。
- 接下来，我们看到导入 **syntaxhighlighter** 代码，它可以动态高亮页面上的代码。
- 然后我们看到 **Google 跟踪 JS 代码**，这让我可以在 Google Analytics 上跟踪网站的统计数据。
- 我在这网站上没有使用 **Bootstrap**，因为它非常小巧简单，但通常我会使用，因为这会让你的网站在移动设备上也能很好地工作。

### t-SNE

![](https://karpathy.github.io/assets/tsne_eg.jpeg)

最后我们进入核心部分！我们需要在 d3js 图中排列用户，使得相似的用户出现在附近。t-SNE 的代价函数在 [van der Maaten 和 Hinton 2008 年的论文](http://jmlr.csail.mit.edu/papers/volume9/vandermaaten08a/vandermaaten08a.pdf) 中进行了描述。与许多其他方法类似，我们在原始空间和嵌入空间中设置两种距离度量，并最小化它们的差异。特别是在 t-SNE 中，原始空间距离基于高斯分布，而嵌入空间基于重尾的 Student-t 分布。KL 散度公式有一个很好的特性，即它在惩罚两个空间之间的距离时是不对称的：

- 如果两个点在原始空间中很接近，那么在嵌入中这两个点之间存在很强的吸引力
- 相反，如果两个点在原始空间中相距很远，算法相对自由地将这些点放置在任意位置

因此，该算法偏好保存高维数据的局部结构。方便的是，作者在他们的[网站](http://homepage.tudelft.nl/19j49/t-SNE.html)上链接了 t-SNE 的多种实现，这也让我们可以查看一些参考代码（如果你和我一样，读代码可能比读文字描述容易得多）。我们准备编写 Javascript 版本了！

最终代码可以在 Github 上的 [tsne.js 文件](https://github.com/karpathy/tsnejs) 中看到。注意我们如何将所有 JS 代码包装在一个函数闭包中，以使我们不污染全局命名空间。这是 Javascript 中一个非常常见的技巧，本质上用于实现类。还要注意我不得不在开头包含的大量实用样板代码，因为 Javascript 并不专门为数学而设计:) 所有魔法发生的核心函数是 `costGrad()`，它计算代价函数和目标的梯度。此函数的正确实现通过 `debugGrad()` 梯度检查进行双重验证。一旦分析梯度与数值梯度一致，我们就大功告成了！我们设置一段 Javascript 来重复调用我们的 `step()` 函数（`setInterval()` 调用），并在计算过程中绘制结果。

呼！再次给出最终结果：[t-SNE 演示](http://cs.stanford.edu/people/karpathy/tsnejs/)。

我希望其中一些参考资料对你有用。如果你使用 tsnejs 来嵌入你的数据，请告诉我！

## 彩蛋：词嵌入 t-SNE 可视化

我创建了另一个演示，这次是可视化词向量嵌入。请前往[这里](http://cs.stanford.edu/people/karpathy/tsnejs/wordvecs.html)查看。词嵌入按照这篇 [ACL 2012 论文](http://www.socher.org/index.php/Main/ImprovingWordRepresentationsViaGlobalContextAndMultipleWordPrototypes) 中描述的方法进行训练。

这个（无监督的）目标函数使得那些可以互换的单词（即在非常相似的上下文环境中出现的单词）在嵌入空间中彼此靠近。这一点在可视化中清晰可见！

---

*English original below:*

![](https://karpathy.github.io/assets/tsne_preview.jpeg)

I was recently looking into various ways of embedding unlabeled, high-dimensional data in 2 dimensions for visualization. A wide variety of methods have been proposed for this task. [This Review paper](http://homepage.tudelft.nl/19j49/Matlab_Toolbox_for_Dimensionality_Reduction_files/TR_Dimensiereductie.pdf) from 2009 contains nice references to many of them (PCA, Kernel PCA, Isomap, LLE, Autoencoders, etc.). If you have Matlab available, the [Dimensionality Reduction Toolbox](http://homepage.tudelft.nl/19j49/Matlab_Toolbox_for_Dimensionality_Reduction.html) has a nice implementation of many of these methods. Scikit Learn also has a brief section on [Manifold Learning](http://scikit-learn.org/stable/modules/manifold.html) along with the implementation.

Among these algorithms, t-SNE comes across as one that has a pleasing, intuitive formulation, simple gradient and nice properties. Here is a [Google Tech Talks video](http://www.youtube.com/watch?v=RJVL80Gg3lA) of Laurens van der Maaten (the author) explaining the method. I set out to re-implement t-SNE from scratch since doing so is the best way of learning something that I know of, and what better language to do this in than - Javascript!:)

Long story short, I've implemented t-SNE in JS, released it as [tsnejs on Github](https://github.com/karpathy/tsnejs), and created a small demo that uses the library to visualize the top twitter accounts based on what they talk about. In this post, I thought it might be fun to document a small 1-day project like this, from beginning to end. This also gives me an opportunity to describe some of my projects toolkit, which others might find useful.

### Final demo

First, take a look at the [final demo](http://cs.stanford.edu/people/karpathy/tsnejs/). To create this demo I found the top 500 most followed accounts on Twitter, downloaded 200 of their tweets and then measured differences in what they tweet about. These differences are then fed to t-SNE to produce a 2-dimensional visualization, where nearby people tweet similar things. Fun!

### Fetching top tweeps

We first have to identify the top 500 tweeps. I googled "top twitter accounts" and found http://twitaholic.com/, which lists them out. However, the accounts are embedded in the webpage and we need to extract them in structured format. For this, I love a recent YC startup [Kimono](https://www.kimonolabs.com/); I use it extensively to scrape structured data from websites. It lets you click the elements of interest (the Twitter handles in this case), and extracts them out in JSON. Easy as pie!

### Collecting tweets

Now we have a list of top 500 tweeps and we'd like to obtain their tweets to get an idea about what they tweet about. My library of choice for this task is [Tweepy](https://github.com/tweepy/tweepy). Their documentation is quite terrible but if you browse the source code things seem relatively simple. Here's an example call to get 200 tweets for a given user:

```python
tweets = tweepy.Cursor(api.user_timeline, screen_name=user).items(200)
```

We iterate this over all users, extract the tweet text, and dumpt it all into files, one per account. I had to be careful with two annoyances in process:

- Twitter puts severe rate limits on API calls, so this actually took several hours to collect, wrapped up in try catch blocks and `time.sleep` calls.
- The returned text is in Unicode, which leads to trouble if you're going to try to write it to file.

One solution for the second annoyance is to use the codecs library:

```python
import codecs
codecs.open(filename, 'w', 'utf-8').write(tweet_texts)
```

Oh, and lets also grab and save the Twitter profile pictures, which we'll use in the visualization. An example for one user might be:

```python
import urllib # yes I know this is deprecated
userobj = api.get_user(screen_name = user)
urllib.urlretrieve(imgname, userobj.profile_image_url) # save image to disk
```

I should mention that I write a lot of quick and dirty Python code in [IPython Notebooks](http://ipython.org/notebook.html), which I very warmly recommend. If you're writing all your Python in text editors, you're seriously missing out.

### Quantifying Tweep differences

We now have 500 tweeps and their 200 most recent tweets concatenated in 500 files. We'd now like to find who tweets about similar things. [Scikit learn](http://scikit-learn.org/stable/) is very nice for quick NLP tasks like this. In particular, we load up all the files and create a 500-long array where every element are the 200 concatenated tweets. Then we use the [TfidfVectorizer](http://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html) class to extract all words and bigrams from the text data, and to turn every user's language into one tfidf vector. This vector is a fingerprint of the language that each person uses. Here's how we can simply wire this up:

```python
from sklearn.feature_extraction.text import CountVectorizer,TfidfVectorizer
vectorizer = TfidfVectorizer(min_df=2, stop_words = 'english',\
strip_accents = 'unicode', lowercase=True, ngram_range=(1,2),\
norm='l2', smooth_idf=True, sublinear_tf=False, use_idf=True)
X = vectorizer.fit_transform(user_language_array)
D = -(X * X.T).todense() # Distance matrix: dot product between tfidf vectors
```

In the above, `user_language_array` is the 500-element array that has the concatenated tweets. The `TfidfVectorizer` class looks through all tweets and takes note of all words (unigrams) and word bigrams (i.e. series of two words). It builds a dictionary out of all unigram/bigrams and essentially counts up how often every person uses each one. Here's an example of some tweet text converted to unigram/bigrams:

![](https://karpathy.github.io/assets/tsne_sentprepro.jpeg)

The tfidf vectors are returned stacked up as rows inside `X`, which has size `500 x 87,342`. Every one of the 87,342 dimensions corresponds to some unigram or bigram. For example, the 10,000th dimension could correspond to the frequency of usage of the unigram "YOLO". The vectors are L2 normalized, so the dot product between these vectors is related to the angle between any two vectors. This can be interpreted as the similarity of language. Finally, we dump the matrix and the usernames into a JSON file, and we're ready to load things up in Javascript!

### The Visualization parts

We now create an.html file and import [jQuery](http://jquery.com/) (as always), and [d3js](http://d3js.org/), which I like to use for any kind of plotting. We load up the JSON that stores our distances and usernames with jQuery, and use d3js to initialize the SVG element that will hold all the users. For starters, we plot the users at random position but we will soon arrange them so that similar users cluster nearby with t-SNE. Inspect the code on the [demo page](http://cs.stanford.edu/people/karpathy/tsnejs/) to see the jQuery and d3js parts (Ctrl+U). In the code, we see a few things I like to use:

- I like to use **Google Fonts** to get prettier-than-default fonts. Here, for example I'm importing Roboto, and then using it in the CSS.
- Next, we see an import of **syntaxhighlighter** code which dynamically highlights code on your page.
- Then we see **Google tracking JS code**, which lets me track statistics for the website on Google Analytics.
- I didn't use **Bootstrap** on this website because it's very small and simple, but normally I would because this makes your website right away work nicely on mobile.

### t-SNE

![](https://karpathy.github.io/assets/tsne_eg.jpeg)

Finally we get to the meat! We need to arrange the users in our d3js plot so that similar users appear nearby. The t-SNE cost function was described in this [2008 paper by van der Maaten and Hinton](http://jmlr.csail.mit.edu/papers/volume9/vandermaaten08a/vandermaaten08a.pdf). Similar to many other methods, we set up two distance metrics in the original and the embedded space and minimize their difference. In t-SNE in particular, the original space distance is based on a Gaussian distribution and the embedded space is based on the heavy-tailed Student-t distribution. The KL-divergence formulation has the nice property that it is asymmetric in how it penalizes distances between the two spaces:

- If two points are close in the original space, there is a strong attractive force between the the points in the embedding
- Conversely, if the two points are far apart in the original space, the algorithm is relatively free to place these points around.

Thus, the algorithm preferentially cares about preserving the local structure of the high-dimensional data. Conveniently, the authors link to multiple implementations of t-SNE on [their website](http://homepage.tudelft.nl/19j49/t-SNE.html), which allows us to see some code for reference as well (if you're like me, reading code can be much easier than reading text descriptions). We're ready to write up the Javascript version!

The final code can be seen in [tsne.js file](https://github.com/karpathy/tsnejs), on Github. Note how we're wrapping all the JS code into a function closure so that we don't pollute the global namespace. This is a very common trick in Javascript that is essentially used to implement classes. Note also the large number of utility boring code I had to include up top because Javascript is not exactly intended for math:) The core function where all magic happens is `costGrad()`, which computes the cost function and the gradient of the objective. The correct implementation of this function is double checked with `debugGrad()` gradient check. Once the analytic gradient checks out compared to numeric gradient, we're good to go! We set up a piece of Javascript to call our `step()` function repeatedly (`setInterval()` call), and we plot the solution as it gets computed.

Phew! Final result, again: [t-SNE demo](http://cs.stanford.edu/people/karpathy/tsnejs/).

I hope some of the references were useful. If you use tsnejs to embed some of your data, let me know!

## Bonus: Word Embedding t-SNE Visualization

I created another demo, this time to visualize word vector embeddings. Head [over here](http://cs.stanford.edu/people/karpathy/tsnejs/wordvecs.html) to see it. The word embeddings are trained as described in this [ACL 2012 paper](http://www.socher.org/index.php/Main/ImprovingWordRepresentationsViaGlobalContextAndMultipleWordPrototypes).

The (unsupervised) objective function makes it so that words that are interchangable (i.e. occur in very similar surrounding context) are close in the embedding. This comes across in the visualization!