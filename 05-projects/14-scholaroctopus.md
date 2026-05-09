# ScholarOctopus

**Website:** https://cs.stanford.edu/people/karpathy/scholaroctopus/
**GitHub:** https://github.com/karpathy/scholaroctopus
**Stars:** 79 | **Forks:** 17 | **Language:** N/A

## Description

A collection pointing to ~7,000 papers drawn from 34 conferences in Computer Vision and Machine Learning — including CVPR, ICCV, NIPS, ICML, ECCV, BMVC — spanning 2006 to 2014.

An attempt to enable more rapid discovery of relevant literature. Papers are embedded with t-SNE based on tfidf vectors computed from bigrams of each paper. The author notes: "starting ScholarOctopus with these conferences because it is my primary area of expertise."

## Features

- Browse ~7,000 papers in an interactive 2D visualization
- "Export nearest 50 as CSV"
- "Nearest Papers" section
- Search by title or author
- Papers embedded with t-SNE for spatial clustering by topic similarity

## Data

Structured data for the visualization is available for download as JSON at `out.json`. Full stats at `stats.txt`.

## License

Maintained by @karpathy.

---

*Fetched from https://cs.stanford.edu/people/karpathy/scholaroctopus/ on 2026-05-09*

## 三岁版

ScholarOctopus 是一个巨大的"论文地图"，上面有7000多篇论文，就像一个星空图。每篇论文都是一颗星星，内容差不多的星星就靠在一起，这样你一看就知道"哦，这些论文都是讲同一个方向的"。你还能在上面搜索论文标题或作者名字，就像在地图上找地方一样方便。