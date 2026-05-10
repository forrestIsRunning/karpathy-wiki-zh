# ScholarOctopus

**Website:** https://cs.stanford.edu/people/karpathy/scholaroctopus/
**GitHub:** https://github.com/karpathy/scholaroctopus
**Stars:** 79 | **Forks:** 17 | **Language:** N/A

## 项目介绍

一个收录了约 7,000 篇论文的合集，涵盖计算机视觉和机器学习领域的 34 个会议——包括 CVPR、ICCV、NIPS、ICML、ECCV、BMVC——时间跨度从 2006 年到 2014 年。

旨在帮助人们更快地发现相关文献。论文基于每篇论文的二元词组的 tfidf 向量，使用 t-SNE 进行嵌入。作者注明："从这些会议开始启动 ScholarOctopus，因为这是我的主要专业领域。"

ScholarOctopus 是一个巨大的"论文地图"，上面有 7000 多篇论文，就像一个星空图。每篇论文都是一颗星星，内容差不多的星星就靠在一起，这样你一看就知道"哦，这些论文都是讲同一个方向的"。你还能在上面搜索论文标题或作者名字，就像在地图上找地方一样方便。

## 功能特性

- 在交互式 2D 可视化中浏览约 7,000 篇论文
- "导出最近的 50 篇为 CSV"
- "附近论文"板块
- 按标题或作者搜索
- 论文通过 t-SNE 嵌入，按主题相似度进行空间聚类

## 数据

可视化的结构化数据可以 JSON 格式下载，文件名为 `out.json`。完整统计信息在 `stats.txt` 中。

## 许可证

由 @karpathy 维护。

---

*数据获取自 https://cs.stanford.edu/people/karpathy/scholaroctopus/ (2026-05-09)*