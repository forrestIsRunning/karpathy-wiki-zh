### Quantifying Hacker News

I thought it would be fun to analyze the activity on one of my favorite sources of interesting links and information, [Hacker News](https://news.ycombinator.com/). My source of data is a script I’ve set up some time in August that downloads HN (the Front page and the New stories page) every minute. We will be interested in visualizing the stories as they get upvoted during the day, figuring out which domains/users are most popular, what topics are most popular, and the best time to post a story. I’m making all my data and code (Python data collection scripts + IPython Notebook for analysis) available in case you’d like to carry out a similar analysis.

### Data collection protocol

I set up a very simple python script that scrapes the HN **front page** and the **new stories page** every minute. A single day of data begins at 4am (PST) and ends at 4am the next day. The.html files are saved compressed as gzipped pickles and one day occupies roughly 10mb in this format. I had bring down my machine for a few days a few times so there are some gaps in the data, but in the end we get 47 days of data from period between August 22 and October 30.

### Raw HTML data parsing

The parsing Python script uses **BeautifulSoup** to convert the raw HTML into a more structured JSON. This script was by the way by no means simple to write – HN is based on unstructured tables and I had to discover many strange edge cases in its behavior along the way. At the end I ended up with a 100-line ugliest-parsing-function-ever (really, I’m not proud of it) but it works and outputs something like the following for a single story at a specific snapshot:

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