### 扩展程序黑客技巧

我想分享几个关于一个强大技能的例子，这个技能我在过去一年里逐渐掌握。它就是快速编写 Chrome 自定义浏览器扩展程序并用来定制我最喜欢的网站的能力。编写扩展程序非常快：你需要一个简短的 manifest 文件，里面包含一些元信息，一个包含你代码的文件夹里有几个 js/html 文件，然后你只需从扩展程序菜单中点击几下激活该文件夹即可。总的来说，你可以用扩展程序做很多有趣的事情：

- 添加按钮、右键菜单项
- 修改 Omnibox（地址栏）的功能
- 创建扩展程序专属的网页来显示各种数据/设置
- 你的扩展程序可以有本地（或同步）的持久化数据存储
- 你可以在任何网页的 DOM 上运行几乎任意的 JavaScript

我无法强调最后一项有多么强大。你可以运行 JavaScript。在任何网页之上。你可以读取页面 DOM。你可以自动地、在页面加载时甚至周期性地写入 DOM！这给了你完全的自由来按照自己的喜好修改任何网页：删除烦人的内容、添加新功能、记录/抓取网站数据、改变布局等等。这简直太疯狂了！

我将带你了解一些例子，用 Twitter 的可能修改来展示这可以多么简单和强大。Twitter 很有趣，我经常使用它，但他们的网站很烦人，有一些丑陋的元素，有时缺乏我想要的功能。普通人会请求功能然后等待，但有了扩展程序黑客技巧这门黑暗艺术，我们可以做得更好。让我们直接开始吧。

### 修复丑陋的东西

Twitter 最近的一次改动添加了这段丑陋的文字，默认一直可见，出现在每条推文上：![](https://karpathy.github.io/assets/chrome1.jpeg)

我理解这能让人们不经意间更多地点击这些按钮，并增加 Twitter 的互动数据，但它既没用又丑陋，而且占用了太多空间。让我们右键点击其中一个，选择"检查元素"。这会打开页面的 HTML，我们看到罪魁祸首的 DOM 元素：

![](https://karpathy.github.io/assets/chrome2.jpeg)

所以我们有一个列表 `<ul></ul>`，其中包含 `<li>` 项，分别对应回复、转推、收藏和更多。在每个项里面，他们有一个 `<a>`（处理点击操作的锚点），再往深处有一个 `<span>` 作为图标，最后跟着包裹在 `<b>` 中的丑陋文字。这看起来很容易，我们将根据它们的 class 属性找到所有这些元素，向下深入到文字并将其删除。所以我们为 TwitterClean 扩展程序创建一个新文件夹，复制粘贴一些 manifest 样板代码，并设置它在 Twitter 加载时加载一个 JavaScript 文件。例如，在 twitter.com 页面加载后立即执行：

```javascript
var clean_twitter = function(){
  var ugly = [];
  ugly.push('.action-reply-container');
  ugly.push('.action-rt-container');
  ugly.push('.action-del-container');
  ugly.push('.action-fav-container');
  ugly.push('.more-tweet-actions');

  for(var i=0;i<ugly.length;i++) {
    var u = $(ugly[i]).find('b');
    u.text('');
  }
}
```

加载扩展程序，刷新 Twitter，噗！所有文字都不见了，只剩下图标。这些就足够了。哦，既然我们在 twitter.com 加载时自动运行的代码里，让我们也顺手加上这一行：

```javascript
$('.promoted-tweet').hide(); // 哎呀！
```

这一行调皮代码的作用是什么，我就不多说了：)

### 自动加载新推文

这是另一个烦人的地方：你在侧边显示器上开着 Twitter，新推文来了，但 Twitter 不会自动加载它们！它只显示这个：

![](https://karpathy.github.io/assets/chrome3.jpeg)

这就是 Twitter 被动攻击式的表情，告诉你还有两条推文要显示，但又拒绝真正显示它们。这对用户来说也太有用了。相反，他们希望你停下手中的事，点击按钮来加载新推文。幸运的是，你精通扩展程序黑客技巧，所以你可以简单地右键点击这个标题，去"检查元素"，然后看到告诉你"有更多推文"的 `<div>` 元素有类 "js-new-tweets-bar"。非常简单：

```javascript
var periodic = function() {
  L = document.getElementsByClassName('js-new-tweets-bar');
  if(L.length > 0){
    L[0].click();
  }
}
setInterval(periodic, 1000);
```

当这段代码在 **twitter.com** 加载时运行，它会设置代码每隔一秒（1000 毫秒）查找烦人的栏，然后运行它的点击事件处理程序来加载新推文。就这么简单，现在你的推文会在可用时自动流式显示，而无需你每次都手动刷新。我们只写了 5 分钟代码，就调整了 Twitter 的外观，删除了一些"功能"并添加了一些功能！我们势如破竹！现在让我们做一些更酷的事情。

### 高亮显示来自不常发推者的推文

有一天，我决定用 Twitter 的 REST API 收集一周内我时间线上的推文，发现 30 个账号占据了我看到的所有推文的 50%。由于我总共关注了 384 个账号，这只有 7%！不幸的是，对 Twitter 来说每条推文生来平等，这意味着那些每天发 100 条推文的烦人社交媒体大师完全淹没了你其他那些认为"应该有值得发推的内容才发"的朋友的推文。好吧，实际情况不完全是这样，但我希望有一种机制来高亮显示非常不常发推的人，并看到那些低频内容。Twitter 永远不会实现这个功能，因为这对他们的收入模式完全没有意义，但幸运的是，我们可以很容易地自己拼凑出来！首先，这是一个函数，它遍历你时间线上的所有推文，查看是谁发的，并将每条独特的推文"计费"给原始用户：

```javascript
var charge_tweets = function() {

  // get all tweets in twitter timeline
  var items = $('.tweet');
  for(var i=0;i<items.length;i++) {
    var it = items[i];

    // extract information from tweet HTML
    var original_user = $(it).attr('data-screen-name');
    var retweeter = $(it).attr('data-retweeter');
    var tweet_id = $(it).attr('data-tweet-id');

    // a bit of logic
    var charged_user = original_user;
    if(typeof retweeter !== 'undefined') {
      charged_user = retweeter;
    }

    // charge tweet to the user
    if(charge.hasOwnProperty(charged_user)) {
      var L = charge[charged_user];
      if($.inArray(tweet_id, L) === -1) {
        L.push(tweet_id);  
      }
    } else {
      charge[charged_user] = [tweet_id];
    }
  }
};
```

基本上，每一条推文都有类 "tweet"，所以像上面那样遍历它们很简单。同样，通过检查 HTML 的布局方式，我们可以简单地抓取用户和（唯一的）推文 ID，并用它来构建一个 `user_string -> [tweet id, ...]` 的字典。当然，我们需要让这个积累几天，才能为我们关注的所有人测量出一个好的发推频率分布，因为我们一次次访问 Twitter，总是看到更多人的新推文。但这也意味着我们需要从 Chrome 的本地扩展存储中加载和保存 **charge** 字典，否则每次关闭标签页时我们都会丢失所有计费工作！非常简单：

```javascript
var save_charge = function() {
  chrome.storage.local.set({'charge': charge});
}

var load_charge = function() {
  chrome.storage.local.get('charge', function (result) {
    if(result.charge) {
      charge = result.charge;
      console.log('loaded tweet frequency stats:');
      console.log(charge);
    } else {
      console.log('no tweet frequency to load');
    }
  });
}
```

现在我们只需确保在启动时运行 load_charge()，并在有新推文且我们的 *charge* 字典发生变化时运行 save_charge()。基于这个 *charge* 字典，我们可以轻松地找到，比如说，第 50 百分位的频率，并高亮显示来自发推特频率低于我们关注用户中 50% 的用户的任何推文：

```javascript
var display_charges = function() {

  var items = $('.tweet');
  for(var i=0;i<items.length;i++) {
    var it = items[i];

    // ... as above and then:

    var charged_tweets = charge[charged_user];
    var charge_count = charged_tweets.length;

    // adjust highlight color of the tweet according to rareness
    if(charge_percentile > 0) {
      var ratio = charge_count / charge_percentile;
      var x = Math.floor(Math.min(ratio,1)*255);
      $(it).css('background-color', 'rgb(255,255,' + x + ')');
    }
  }
}
```

这只是众多可能性中的一种。这里，对于很少发推的用户，*ratio* 会很低，我们根据稀有程度将他们的推文设置为黄色。在你的时间线上很难不注意到这一点！:) 同时，为什么不也加上：

```javascript
var VIP = ['elonmusk'];
if($.inArray(charged_user, VIP) !== -1) {
  $(it).css('background-color', 'rgb(150,255,150)'); 
}
```

这样，埃隆·马斯克（或其他你喜欢的 Twitter 用户）的推文将总是发出明亮的绿色光芒，很难不被注意到！不错。下面是我们得到的效果：

![](https://karpathy.github.io/assets/chrome4.jpeg)

看看这个！Mashable 和一个需要让他每个关注者都知道自己"啊——"的人看起来正常，埃隆的推文是难以忽视的绿色，而一个相对不常发推特的人被轻微高亮为黄色。

### 总结

我们用了大约 100 行 JavaScript 和 10 分钟（再加一点练习），就调整了 Twitter 的外观，删除了呃……不想要的内容，让 Twitter 自动刷新，并添加了一个全新的功能来高亮显示不常发推的人！

然而我们只是刚刚触及表面。如果你能熟练地用 Chrome 出色的检查器浏览页面 HTML，并会写 HTML/Javascript/CSS，这些快速技巧有潜力通过给你强大的选项来自定义你最喜欢的网站，从而显著改善你的在线体验。如果你还不熟悉，也许是时候去看看 Chrome 扩展程序" [入门指南](http://developer.chrome.com/extensions/getstarted.html) "并写几个小技巧了：)

哦，如果你想要上面代码的完整版本，你可以在这里找到：[链接](http://cs.stanford.edu/people/karpathy/twitteropt.zip)（注意代码有些粗糙，但毕竟是个快速拼凑的东西！）。如果你有任何问题，请通过 [@karpathy](https://twitter.com/karpathy) 告诉我，下次再见！

---

*English original below:*

### Extension Hacking

I wanted to share a few examples of a powerful skill that I've been gradually picking up over the last year. It is simply the ability to quickly hack together custom browser extensions in Chrome and using them to customize my favorite websites. Writing extensions is very fast: you need a short manifest file that contains some boring meta information, a few js/html files with your code in a folder, and then you simply activate the folder as an extension from the Extensions menu with a few clicks. In general, you can do a lot of fancy things with extensions:

- add buttons, context-menu items
- modify functionality of Omnibox
- create extension-specific webpages that display various data/settings
- your extension is allowed to have local (or synced), persistent storage of data
- you can run almost arbitrary Javascript over the DOM of any webpage

I can't stress how powerful the last item is. You can run Javascript. On top of any webpage. You can Read the page DOM. You can write to it, automatically, on load of the webpage or even periodically! This gives you complete freedom in modifying any webpage to your tastes: remove annoying content, add new features, log/scrape website data, change the layout, etc. It's completely crazy!

I'll walk you through some examples with possible mods of Twitter just to give you a glimpse of how easy and powerful this can be. Twitter is fun and I use it often, but their website is annoying, has some ugly elements, and sometimes lacks certain functionality I would like it to have. A normal person would request features and wait, but with the dark arts of extension hacking we can do much better. Lets get right to it.

### Fixing the Ugly

A recent change on Twitter added this ugly text, visible by default and always, on every single tweet: ![](https://karpathy.github.io/assets/chrome1.jpeg)

I understand it gets people to accidentally click on these more and pads Twitter's engagement numbers, but it's useless, ugly, and it just takes up too much space. Lets right click on one of these and choose Inspect Element. This opens up the HTML of the page and here we see the culprit DOM elements:

![](https://karpathy.github.io/assets/chrome2.jpeg)

So we have a list `<ul></ul>` with items `<li>` one for each of Reply, Retweet, Favorite and More. Inside every of them they have a `<a>` (anchor that processes the click action), deeper we have a `<span>` that becomes the icon, and finally followed by the ugly text wrapped in `<b>`. That looks easy enough, we will find all these elements based on their class attribute, descend down to find the text and get rid of it. So we create a new folder for TwitterClean extension, copy paste some manifest boring code and set it up to load a javascript file anytime twitter loads. For example, right after twitter.com page loads, lets execute:

```javascript
var clean_twitter = function(){
  var ugly = [];
  ugly.push('.action-reply-container');
  ugly.push('.action-rt-container');
  ugly.push('.action-del-container');
  ugly.push('.action-fav-container');
  ugly.push('.more-tweet-actions');

  for(var i=0;i<ugly.length;i++) {
    var u = $(ugly[i]).find('b');
    u.text('');
  }
}
```

Load the Extension, refresh Twitter and poof! All the text is gone and we're just left with the icons. These suffice. Oh and while we're at code we run automatically on load of twitter.com, lets slip this one is as well:

```javascript
$('.promoted-tweet').hide(); // oops!
```

I'll let you figure out what that single naughty line of code does for you:)

### Loading new tweets automatically

Here's another annoyance: you have your Twitter running on your side monitor and new tweets come in, but Twitter doesn't load them automatically! It just shows this:

![](https://karpathy.github.io/assets/chrome3.jpeg)

That's the passive aggressive look of Twitter telling you that there are two more tweets to show, but also refusing to actually show them. That would be too useful to their users. Instead, they want you to stop what you're doing and click the button to load the new tweets. Luckily, you are skilled at extension hacking so you can simply right click the caption, go to Inspect Element, and see that the <div> element that tells you there are more tweets has class "js-new-tweets-bar". Easy enough:

```javascript
var periodic = function() {
  L = document.getElementsByClassName('js-new-tweets-bar');
  if(L.length > 0){
    L[0].click();
  }
}
setInterval(periodic, 1000);
```

When this gets run when **twitter.com** loads, it sets up the code to look for the annoying bar every second (1000 milliseconds) and then runs its click event handler which loads the new tweets. That's all it takes, and now your tweets are streaming down automatically whenever they are available without you having to explicitly refresh them all the time. We've only written code for 5 minutes and in that time we tweaked the way Twitter looked, removed some "functionality" and added some functionality! We're on a roll! Let's do something fancier now.

### Highlighting tweets from rare tweeters (wait, or tweepers?)

One day I decided to collect tweets on my timeline over a period of a week using Twitter's REST API and saw that 30 accounts make up 50% of everything I see on Twitter. Since I follow 384 accounts in total, that's only 7%! Unfortunately, for Twitter every tweet is created equal, which means that this annoying social media guru person who tweets 100 times a day completely drowns tweets coming from your other friends who believe that one should also have something worthy of tweeting too. Okay well it's not exactly like that but I wished there was a mechanism for highlighting the very infrequent tweeters and seeing that low frequency content. Twitter will never implement this because it makes Zero sense for their revenue model, but luckily, we can hack this together quite easily! First, here's a function that goes through all tweets on your timeline, looks at who tweeted, and "charges" every unique tweet to the originating user:

```javascript
var charge_tweets = function() {

  // get all tweets in twitter timeline
  var items = $('.tweet');
  for(var i=0;i<items.length;i++) {
    var it = items[i];

    // extract information from tweet HTML
    var original_user = $(it).attr('data-screen-name');
    var retweeter = $(it).attr('data-retweeter');
    var tweet_id = $(it).attr('data-tweet-id');

    // a bit of logic
    var charged_user = original_user;
    if(typeof retweeter !== 'undefined') {
      charged_user = retweeter;
    }

    // charge tweet to the user
    if(charge.hasOwnProperty(charged_user)) {
      var L = charge[charged_user];
      if($.inArray(tweet_id, L) === -1) {
        L.push(tweet_id);  
      }
    } else {
      charge[charged_user] = [tweet_id];
    }
  }
};
```

Basically, it turns out every tweet has class "tweet", so it is trivial to iterate over them as seen above. Similarly, by inspecting the way the HTML is laid out, it turns out we can simply scrape the user and the (unique) tweet id and use it to build up a dictionary of `user_string -> [tweet id, ...]`. Of course, we will have to let this accumulate for a few days before it measures a good tweeting frequency distribution for all people we follow as we visit Twitter again and again always seeing new tweets from more people. But this also means we have to load and save the **charge** dictionary from Chrome's local extension storage or otherwise we would lose all our charging work whenever we close the Tab! Easy enough:

```javascript
var save_charge = function() {
  chrome.storage.local.set({'charge': charge});
}

var load_charge = function() {
  chrome.storage.local.get('charge', function (result) {
    if(result.charge) {
      charge = result.charge;
      console.log('loaded tweet frequency stats:');
      console.log(charge);
    } else {
      console.log('no tweet frequency to load');
    }
  });
}
```

Now we just make sure to run load\_charge() at start up, and save\_charge() anytime there are new tweets and our *charge* dictionary changes. Based on this *charge* dictionary we can easily find, say, the 50th percentile frequency, and highlight any tweet that comes from a user who tweets less often than 50% of the users we follow:

```javascript
var display_charges = function() {

  var items = $('.tweet');
  for(var i=0;i<items.length;i++) {
    var it = items[i];

    // ... as above and then:

    var charged_tweets = charge[charged_user];
    var charge_count = charged_tweets.length;

    // adjust highlight color of the tweet according to rareness
    if(charge_percentile > 0) {
      var ratio = charge_count / charge_percentile;
      var x = Math.floor(Math.min(ratio,1)*255);
      $(it).css('background-color', 'rgb(255,255,' + x + ')');
    }
  }
}
```

This is just one possibility out of many. Here, *ratio* will be low for users who rarely tweet, and we're setting their tweet to be yellow based on their rareness. Very hard to not notice on your timeline!:) And while we're at it, why not also fit in:

```javascript
var VIP = ['elonmusk'];
if($.inArray(charged_user, VIP) !== -1) {
  $(it).css('background-color', 'rgb(150,255,150)'); 
}
```

This way, Elon Musk's (or your other Twitter favorites) tweets will always glow a vibrant, green color that is hard to notice! Nice. Here's what we get:

![](https://karpathy.github.io/assets/chrome4.jpeg)

Just look at that! Mashable and some person who needed every single one of his followers to know "Aarrrgh" look normal, Elon's tweets are hard to miss green, and someone who doesn't tweet relatively as often is highlighted a bit as yellow.

### Summary

It took us ~100 lines and 10 minutes of Javascript (with a bit of practice) and we tweaked Twitter's look, removed err… undesirable content, made Twitter autorefresh, and added an entirely new feature that highlights infrequent tweepers!

Yet we've only barely scratched the surface. If you're comfortable with navigating HTML of pages with Chrome's 强大的 inspector and writing HTML/Javascript/CSS, these quick hacks have the potential to significantly improve your online experience by giving you powerful options for customizing your favorite sites. And if you are not comfortable, perhaps it's time to head over to Chrome Extensions " [Getting Started](http://developer.chrome.com/extensions/getstarted.html) " and write a few hacks:)

Oh, and if you'd like the full code of the above, you may find it here: [LINK](http://cs.stanford.edu/people/karpathy/twitteropt.zip) (Note it is a bit rough around the edges, but then it is a quick hack after all!). Let me know if you have any issues on [@karpathy](https://twitter.com/karpathy), and until later!