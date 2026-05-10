# NIPS Preview

**Website:** https://cs.stanford.edu/people/karpathy/nipspreview/
**GitHub:** https://github.com/karpathy/nipspreview
**Stars:** 186 | **Forks:** 65 | **Language:** Python

## 项目介绍

NIPS 2012 录用论文的更美观、更易读的呈现格式。脚本生成 .html 页面，方便浏览 NIPS 论文。

NIPS Preview 是一个"论文书架"，帮你看清楚学术大会上每一篇论文。它把每篇文章的标题、作者、主要内容都整理得漂漂亮亮的，还告诉你这篇文章在讲什么方向——是讲"数学理论"还是"计算机视觉"之类的。就像把一堆书按类别摆在书架上，方便你挑着看。

每篇论文页面展示以下内容：
- 标题和作者
- PDF、BibTeX 和补充材料的链接
- 按 tf-idf 相似度排序的链接
- 摘要（可展开）
- 论文中出现频率最高的 100 个词，按 LDA 主题模型（k=7 个主题）进行颜色编码：
  - 主题 0：理论
  - 主题 1：强化学习
  - 主题 2：图模型
  - 主题 3：深度学习/视觉
  - 主题 4：优化
  - 主题 5：神经科学
  - 主题 6：嵌入等

用户可以通过切换按各个 LDA 主题排序来按学科领域筛选论文。

---

*数据获取自 https://cs.stanford.edu/people/karpathy/nipspreview/ (2026-05-09)*