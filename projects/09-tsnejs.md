# tSNEJS

**GitHub:** https://github.com/karpathy/tsnejs
**Stars:** 908 | **Forks:** 158 | **Language:** JavaScript
**License:** MIT

## 项目介绍

用 JavaScript 实现的 t-SNE 可视化算法。t-SNE 是一种将数据嵌入到 2 维或 3 维空间中的可视化算法。如果你的数据具有可测量的两两差异，该技术可以帮助识别聚类。

基于 van der Maaten 和 Hinton 2008 年的论文（JMLR，第 9 卷，第 2579-2605 页）。

tSNEJS 是一个"画画小帮手"，能把好多好多数字变成一幅你能看懂的画。比如你有 100 个东西的数据，看不出来谁和谁是一伙的，它就能把它们画在纸上，让长得像的靠在一起。就像把一堆混在一起的积木按颜色分开摆好！

## 在线演示

项目的[主站](https://cs.stanford.edu/people/karpathy/tsnejs/)上有一个在线 CSV 演示页面，用户可以粘贴数据，实时得到嵌入结果。

## 示例代码

```javascript
var opt = {}
opt.epsilon = 10;     // 学习率（10 = 默认值）
opt.perplexity = 30;  // 每个点大约影响多少个邻居（30 = 默认值）
opt.dim = 2;          // 嵌入的维度（2 = 默认值）

var tsne = new tsnejs.tSNE(opt);  // 创建一个 tSNE 实例

// 用成对不相似度矩阵初始化
var dists = [[1.0, 0.1, 0.2], [0.1, 1.0, 0.3], [0.2, 0.1, 1.0]];
tsne.initDataDist(dists);

for(var k = 0; k < 500; k++) {
  tsne.step();  // 每一步都在改进结果
}

var Y = tsne.getSolution();  // Y 是一个二维坐标数组，用于绘图
```

也可以通过 `tsne.initDataRaw(X)` 提供高维数据点，其中 X 是一个数组的数组。

## 许可证

MIT

---

*数据获取自 https://github.com/karpathy/tsnejs (2026-05-09)*