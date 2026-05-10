---

**中文翻译**

Karpathy 回顾了自己从 90 年代末第一次体验 VR 到 2017 年的心路历程。

90 年代末第一次 VR 体验：低分辨率、重影、延迟，体验糟糕但让他兴奋不已——"这就是未来！"但之后 VR 消失了十几年。

2012 年看到 Oculus Kickstarter 时他兴奋极了。后来买了 HTC Vive，但玩了 2 小时后只说"挺酷的"，就回去工作了。朋友们试过后也只说"酷"，但并不急于再体验。

**VR 现在的问题**：
1. **性价比低**：游戏贵（$29.99-$59.99）但深度不够，像手机上的 $0.99 游戏
2. **设计反模式**：很多开发者忽略 VR 的基本约束（不能旋转/加速镜头，会导致晕眩）
3. **核心问题**：VR 头盔仍然太重/太笨，每隔 30 分钟不舒服
4. **催化剂缺失**：VR 仍然面临鸡和蛋的问题——没有足够好的内容导致用户不足，用户不足导致内容开发者不投入

Karpathy 对 AR（如 HoloLens/Meta 2）更乐观——光线叠加比数百英寸的头戴显示器更实用。

**结论**：VR 技术的执行没有跟上想象力。他在 90 年代末就想拥有"替身"去虚拟世界，但这个梦想的现比预期慢得多。

---

# Virtual Reality: still not quite there, again.

- **Author:** Andrej Karpathy
- **Published:** January 17, 2017
- **URL:** https://karpathy.medium.com/virtual-reality-still-not-quite-there-again-5f51f2b43867
- **Claps:** 841
- **Read time:** 11 min

---

The first time I tried out Virtual Reality was a while ago — somewhere in the late 1990's. I was quite young so my memory is a bit hazy, but I remember a research-lab-like room full of hardware, wires, and in the middle a large chair with a big helmet that came down over your head. I was put through some standard 3 minute demo where you look around, things move around you, they scare you by dropping you down, basics. The display was low-resolution, had strong ghosting artifacts, there was long response lag, and the whole thing was quite a terrible experience. I remember finally putting up the helmet and feeling simultaneously highly nauseated and… extremely excited. This was the future!

And then… nothing happened. I never saw that headset again. I rarely ever saw VR mentioned in tech headlines. No VR arcades sprung up across the street that I could visit with my friends. For the young me, VR became an embarrassing misprediction, right next to "obviously we'll have flying cars/jetpacks soon". Eventually, dreams of fantastical digital universes slipped from my mind entirely. Over time I realized that some technical advances are too easy to imagine, but too hard to execute, and VR falls into this category. I just had to patiently wait for its time to come.

Fast forward to 2012, you can imagine my excitement when I saw the Oculus Kickstarter campaign. It was a dream come true. I don't want this to be too long of a story. TLDR: I end up buying a Vive. Somewhere mid 2016, a Vive gets delivered to my doorstep somewhere around noon and I skip work, intending to play with it the whole day. I was living in a small dorm room at the university so I moved almost everything from my room to the (shared) living room to get enough space.

I think I played with the Vive for about 2 hours that day and you know what? It was… pretty cool. I powered down the computer and went back to work for the remainder of the day.

> "Pretty cool."

This is the phrase I would come to hear over and over again, as I demoed my Vive to my friends. I tried to AB test many aspects of my presentation: the games that I launched, their order, how I described VR or its possibilities, but nothing changed this reaction too much. My friends would put it on, try out some of the games and then, quite content, hand it back to me. They'd insist it was "cool", some were even "blown away", but it was clear they also weren't too eager to get back.

Today, my Vive is organized in a messy pile of wires in the corner my room. I turn it on from time to time to try out the latest and greatest, but for the most part it collects dust. I did get to explore quite a bit though, so I feel qualified to have some opinions on what things VR do/do not work **today**.

## The features of doing VR wrong

**Overpriced tech demos**. The first issue I noticed immediately is that VR games are expensive (e.g. up to $59.99), but as a friend of mine described it, many of them are "not too deep". They are the $0.99 games for your phone, except on your face, and for $29.99. I think I ended up spending several hundred dollars buying games for a total of maybe 10 hours of game time.

**VR design anti-patterns**. It's also surprising how many developers try to ignore the new form factor and its constraints. For instance, you **cannot** translate or rotate (or worse, accelerate) the camera because it gives people nausea. You'd think this simple fact would be obvious common knowledge, but more than 50% of VR games still think that accelerating you around is okay.

**A single bug away from nausea**. I've also experienced game bugs that do weird things to your field of view. Games can switch rapidly from a 3D view to a 2D view "glued" to your eyes, or the screen can flicker, or everything will briefly reverse along some axis, or the inputs to your eyes get switched, or the camera will rapidly spiral out, or something weird. These are extremely negative experiences that usually result in tearing your headset from your head and having to sit down for a while, or completely give up for the evening.

## The features of doing VR properly

I found that it's not too difficult to create an experience that a person would describe as "pretty cool". Even the number of people who have their "mind blown" is by itself irrelevant to the success of the platform. What **is** difficult is making one that a person wants to come back to. Only a few games have achieved this for me so far. They fall into three categories:

**1. Full body experiences**. These are games like AudioShield and Holopoint. There is usually some background music and you have to move your body to achieve game goals. I find these games fun and repeatable whenever I'm in a dancing/moving/feeling really cool mood. Similarly, I love games that get you to manipulate things with your controllers (e.g. Job Simulator). If you've only used VR with a gamepad, you are missing out.

**2. Creative experiences**. These are things like TiltBrush, or any other app that channels your creativity in this new paradigm. TiltBrush today is like the MSPaint of the past, with just the most basic tools and features, but I believe there is a lot of potential for applications like this.

**3. Social experiences**. These are things like AltspaceVR, Rec Room, or Keep Talking and Nobody Explodes. The genius part about these experiences is that the developers don't have to do the hard work of importing too much complexity into the game. All they have to do is involve people, and their social interactions deliver the complexity and repeatability.

In my opinion the experiences that will eventually make VR most compelling will have these features, and ideally all of them combined. They will connect people over multiplayer (3), give them ways of creating and sharing (2), and take advantage of full body presence in inventive ways (1).

## What is VR for?

If you look at the experiences built for VR today, you'll notice that most of them are (usually single-player) games. For example I looked at 100 "new releases" for VR today and 100% of them are games. This might be because games are easier or faster to build.

> VR is for games as much as Personal Computers are for games, spreadsheets, or searching cooking recipes.

It is notoriously difficult to predict future uses of novel technologies. In 1980's Personal Computer software involved games and personal finance applications. Amusingly, today all of the action is in a single binary application (the browser), but we can look at some of the 20 most popular websites and see that they cluster around some basic human wants:

- **Information: "I want to know something"** — Google, YouTube, Wikipedia, Stack Overflow
- **Social/Communication: "I want to talk to someone"** — Google (gmail), Facebook, Twitter, Instagram
- **Entertainment: "I want to be amused"** — YouTube, Reddit

In particular, the most valuable companies here have little to do with games, and all of their products are free to use. The PC gaming market is still there and doing fine, estimated to be worth around $36B in 2016, most of it from free-to-play online titles. We can see similar trends reflected in the mobile market.

Long story short, currently the most content made for VR are games, but looking at the trends above it seems quite unlikely to me that games (in any quantity) will be the thing that makes VR go big. It's also not clear to me that many people "get" this, or agree with it, with the possible exception of Facebook, judging by Zuck's latest VR demo.

## Where does all of this put us?

I think it is likely that we are in a situation now where some technologies (especially those that are 1) easy to predict and 2) potentially very impactful) can in fact undergo multiple cycles whenever something exciting happens in the space. No one wants to miss the possibly few hundred $B wave that is coming at some point.

**Why not yet?** Despite the excitement that goes back to my childhood, I've come to be more pessimistic than optimistic about VR in the short term. There are still too many problems. VR is not like a TV that you can leave running in the background while you chat with a friend or cook a dinner. It's not like a mobile phone that I can keep around and casually glance at to get some instant gratification. Today, VR is an activity (you have to take a long sequence of non-default actions to plug in), it disconnects you from your immediate surroundings, any interruptions are costly (e.g. I get a phone call, or I need to eat or use the restroom), and also makes you look quite silly. You also won't avoid some stigma associated with escapism / being a nerd, something that you cannot fix in a few years.

**When it does happen**. In the medium term (e.g. a decade or two), I could see us make a lot of progress on the hardware and mitigate many of the above problems. For instance, we could shrink VR into face/hand-tracking, high-visual-fidelity, very-low-tracking-error-rate Ray-Ban sunglasses that make you look cool, and you can just slip on in a second to "plug in". If this does happen, I feel confident making a few predictions about what the killer app for VR would look like. It:

- Would have the features above (1. offers functionality that isn't already "good enough" on an existing technology (especially a mobile phone), in this case e.g. body/face tracking and interactions, 2. allows users to create and share, and 3. is social first).
- It will be **free.** It will not be $59.99. You'll pay in other ways of course, either by paying $9.99 for a silly hat, or with your privacy.
- It will cater to basic human needs we see coming up over and over again across time: "I want to know something", "I want to talk to someone" and "I want to be amused". It will not be any specific game.

Or hey, even more amusingly, a killer app could be something B2B, like enabling remote robotic work, where the worker's commands get recorded and become training data for autonomous robotic systems. This is the core premise of my [short story on AI](https://karpathy.github.io/2015/11/14/ai/).

**The long term**. And finally in the long term, how likely is it that we'll have a compelling parallel digital universe (e.g. Ready Player One style) that a good fraction of humanity will plug into for a good portion of their life? On this time scale I'm relatively optimistic. After all, we'll need some artificial difficulty in form of social fun and games when the AIs are doing all the work. Just kidding. I think. A *great* way to end the post.