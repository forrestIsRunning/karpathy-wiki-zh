---
title: "Finding the Best Sleep Tracker"
date: 2025-03-24
url: https://karpathy.bearblog.dev/finding-the-best-sleep-tracker/
---

Finding the Best Sleep Tracker

*24 Mar, 2025*

About 2 months ago I stumbled by this Bryan Johnson video on[How I FIXED My Terrible Sleep - 10 Habits](https://www.youtube.com/watch?v=Wk9p3dhMYdk). I resolved that day to listen to Bryan and try to improve my sleep. But before we can improve it, first - how should we measure it? Bryan Johnson seems to use[Whoop](https://www.whoop.com/us/en/), but at that time I only had my Apple Watch (coupled with one of the popular sleep apps -[AutoSleep](https://apps.apple.com/us/app/autosleep-track-sleep-on-watch/id1164801111)). And then a long time ago I used and liked[Oura](https://ouraring.com/). And I also had an order in for the new and fancy[8Sleep Pod 4 Ultra](https://www.eightsleep.com/), which I was aware offers some sleep tracking too. So I found myself in a bit of a pickle - which one should I pick to track my sleep? And the answer of course is... to initiate a comprehensive tracking project to compare the 4 major candidates and find the. best. sleep. tracker. So that's what I did. This is me fully geared up and ready for bed:

![sleep_edit](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/sleep_edit.webp)

I've now gathered roughly 2 months of data. I kept the raw data in a simple spreadsheet, recording some of the basic measurements: the amount of sleep (Light, REM, Deep, and Awake tossing and turning), heart rate measurements (Resting Heart Rate (RHR), Heart Rate Variability (HRV)), and the sleep Score offered by each app. I'd log these every day right when I wake up so that I can compare and contrast the numbers and relate them to how I felt that morning. You can find my[raw data in this spreadsheet](https://docs.google.com/spreadsheets/d/1mJeKtLuDE9hOuc2e_WjfaP1sds22k_sO2foIvSZLohw/edit?usp=sharing), it looks like this:

![sleep_data](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/sleep_data.webp)

**Qualitative assessment**. Now, to spare you some suspense, after 2 months of data collection and staring at the results basically every morning, it was very pretty easy to guess that Oura and Whoop are both "Tier 1" - fairly similar and quite high quality in their sleep tracking. They both give similar scores that also correlated with the way I felt in the morning*most of the time*. Next is 8Sleep, which is ok. And finally, I was sad to learn that Apple Watch + AutoSleep (which I had used in the past for many months) was really, really terrible. Its scores are basically almost random and they swing around wildly, with little correlation to how I felt in the morning in comparison.

Let's now look at some of the data. First, let's look at the values that all 4 signals take on over the 2 months, with their histograms:

![signals](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/signals.webp)

As we can see, AutoSleep and 8Sleep are way too easy to please, giving out really high scores and pushing against the 100 score boundary. Whoop is also a little too easy to please, giving out 100 scores. Oura is the most difficult to please, shows a relatively nice gaussian distribution of scores, and offering the most dynamic range. I take this to be a good and nice property of Oura. Indeed, after 2 months my highest ever score on Oura was 92, while I can get 100 on Whoop fairly regularly. This means that I can keep going and striving for even more optimal sleep, one day.

Next, I was very curious about the correlation analysis between the trackers. We take all the scores and plot pairwise correlation scatter plots to see which of the trackers "agree the most" with each other. Here it is:

![corr](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/corr.webp)

And here are the correlations sorted:

```
Whoop vs Oura: 0.65
Oura vs 8Sleep: 0.59
Oura vs AutoSleep: 0.47
8Sleep vs AutoSleep: 0.42
Whoop vs 8Sleep: 0.38
Whoop vs AutoSleep: 0.14

```

Whoop and Oura seem to enjoy the highest correlation at ~0.65, while the other trackers are a bit all over the place. In particular, Whoop and AutoSleep are almost uncorrelated (0.14!). If we think that Whoop is good (which I think it is), AutoSleep looks almost like a noise generator.

**Matters of Heart Rate**. Next, I was interested to look at the Resting Heart Rate (RHR) and Heart Rate Variability (HRV). First, all trackers except 8Sleep agree quite highly on the heart rate during the night, including the Apple Watch. 8 Sleep is the worst because... it's a mattress so it doesn't have a direct measurement of the heart rate. I'm actually a bit impressed that it has a correlation this high:

```
           AutoSleep    8Sleep      Oura     Whoop
AutoSleep   1.000000  0.947151  0.908987  0.942587
8Sleep      0.947151  1.000000  0.947977  0.878552
Oura        0.908987  0.947977  1.000000  0.904023
Whoop       0.942587  0.878552  0.904023  1.000000

```

Having established that all 3 devices (Oura, Whoop, AutoSleep) give a good and consistent measurement of resting heart rate during the night, I was curious if there is a correlation with the sleep score, as this is something Bryan mentioned a few times in his videos. In other words, is a lower RHR associated with better sleep score? Keep in mind that this is just correlation analysis, indeed, I have no idea if the apps take RHR as one of the measurements when they calculate the sleep score. For Whoop, it seems like there is a tiny bit of a correlation, i.e. lower RHR comes with higher sleep score (~0.13).

![whoopcorr](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/whoopcorr.webp)

But for Oura there is none:

![ouracorr](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/ouracorr.webp)

So... I'm not sure what to make of this. Going in, I thought that lower RHR would correlate quite well to better score but this doesn't seem to be the case.

Lastly, during the 2 months of data collection I was exercising regularly, getting about 30 minutes on average of Zone 2 cardio every day, except twice a week also doing a 4x4x4 HIIT (4 min off, 4 min on, 4 times). I was curious if this showed up and indeed it seems like it does, pretty cool:

![improvement](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/improvement.webp)

Using Whoop-Oura average measurement of both RHR and HRV, my resting heart rate has improved (decreased) by a bit less than 3 bpm over the duration of these 60 days (from ~51 bpm -> 48 ~bpm), which is awesome. In addition, my HRV has also improved (increased), (from ~49 -> 54). I love to see exercise adaptations in the data. For some unknown reason, notice also that the HRV values from Whoop seem to be inflated above those of Oura by about 5. I'm not exactly sure why, possibly they calculate it differently... but it's a bit surprising and unexplained.

Lastly, over the duration of 2 months I tried to improve my sleep quality, but it's all mixed up with a bunch of random events, parties, injuries, and also random experiments I tried to run here and there. As another example, my last week was rough because I was obsessed with a technical problem and couldn't sleep well. So unfortunately, overall, I am not seeing a dramatic increase in my sleep quality just yet. But I see this as a long-term project and I hope to increase these scores on average over the duration of the year. Maybe if squint hard enough my sleep has improved a tiny amount (?), but let's face it this is cope hah:

![sleepovertime](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/sleepovertime.webp)

**Yes, sleep matters**. Overall, I will say with absolute certainty that Bryan is basically right, and my sleep scores correlate strongly with the quality of work I am able to do that day. When my score is low, I lack agency, I lack courage, I lack creativity, I'm simply tired. When my sleep score is high, I can power through anything. On my best days, I can sit down and work through 14 hours and barely notice the passage of time. It's not subtle. The effects are not a function of a single day's sleep but of the accumulated sleep debt over a duration of last few days. So in other words a single bad night is usually ok. But a few in a row is bad news. And vice versa. Listen to Bryan.

**Shopping recommendations**. Finally, I wanted to close with some recommendations to others who might want to undertake sleep tracking and improve their sleep.

- 

Oura is Tier 1 / super solid tracker. The app is excellent and I love the single "overview pane" with all the data about that sleep (Whoop needs a lot more clicking around the app). I love that Oura score doesn't saturate that easily, that its scores are a gaussian, and that it has dynamic range. Unfortunately, I find the ring form factor quite inconvenient because it's a little thick, and fingers are used extensively (e.g. hand washing, food preparation, etc.) When I go to the gym, I find myself removing the ring often because it interferes with my grip strength, and it could get scratched. The ring has to be sized correctly and your finger changes its size. Sometimes it's a little too snug, sometimes a little too loose. The ring also has to be rotated correctly for the best results (the notch has to be down), so you'll keep finding it rotated wrong and correcting it. I also don't love having to take the ring on and off to charge it.

- 

Whoop is also a Tier 1 / super solid tracker. The app is excellent. It can be a bit overwhelming at first and requires quite a bit of moving around, but it is very comprehensive, full-featured and customizable, more than Oura. It also has a pretty neat and useful LLM integration. I also really like the Community feature, though it is severely undercooked, under-designed, and feels orphaned. I think Oura has a better "grand overview" page for a single dense summary of one night of sleep. I don't like that Whoop saturates at 100 fairly easily. I find that Whoop is significantly better when it comes to the form factor. Having the tracker on your wrist is just so significantly easier and less intrusive into your daily life. In addition, you never have to take it off because the charger attaches on and off onto it!

- 

I didn't find 8Sleep to be very reliable in its sleep tracking. The scores don't make as much sense to me when I wake up, and as we saw above they don't correlate very strongly with Whoop or Oura.

- 

AutoSleep is basically a random number generator. Maybe there is a better app on Apple Watch for sleep tracking, but I haven't found it. Do not use.

![apps](https://bear-images.sfo2.cdn.digitaloceanspaces.com/karpathy/apps.webp)

Above: The 4 apps. Left to right:**Oura**- I love this "grand overview" summary page, it's dense with just the info you want, and it's super easy to swipe left/right for other days.**Whoop**- less dense, you have to move around a lot to "treasure hunt" the information you want.**8Sleep**- pretty decent.**AutoSleep**- looks cool but the numbers are all wrong so`¯\(ツ)/¯`.

Summarizing all of that into my advice right now: Get Whoop for 9.5/10, reliable, convenient sleep tracking with an excellent app (once you get to know it a bit). Get Oura for 10/10 tracking, if you're ok with the ring form factor.

Did I skip your favorite obviously best sleep tracker? Let me know on X[@karpathy](https://x.com/karpathy).