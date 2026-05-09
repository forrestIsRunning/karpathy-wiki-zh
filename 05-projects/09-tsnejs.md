# tSNEJS

**GitHub:** https://github.com/karpathy/tsnejs
**Stars:** 908 | **Forks:** 158 | **Language:** JavaScript
**License:** MIT

## Description

Implementation of t-SNE visualization algorithm in Javascript. t-SNE is a visualization algorithm that embeds things in 2 or 3 dimensions. If you have data with measurable pairwise differences, the technique can help identify clusters.

Based on the 2008 paper by van der Maaten and Hinton (JMLR, Volume 9, pages 2579-2605).

## Online Demo

The project's [main website](https://cs.stanford.edu/people/karpathy/tsnejs/) hosts a live CSV demo where users can paste data and get on-the-fly embeddings.

## Example Code

```javascript
var opt = {}
opt.epsilon = 10;     // learning rate (10 = default)
opt.perplexity = 30;  // roughly how many neighbors each point influences (30 = default)
opt.dim = 2;          // dimensionality of the embedding (2 = default)

var tsne = new tsnejs.tSNE(opt);  // create a tSNE instance

// initialize with pairwise dissimilarities
var dists = [[1.0, 0.1, 0.2], [0.1, 1.0, 0.3], [0.2, 0.1, 1.0]];
tsne.initDataDist(dists);

for(var k = 0; k < 500; k++) {
  tsne.step();  // each call improves the solution
}

var Y = tsne.getSolution();  // Y is an array of 2-D points for plotting
```

Data can also be supplied as high-dimensional points via `tsne.initDataRaw(X)`, where X is an array of arrays.

## License

MIT

---

*Fetched from https://github.com/karpathy/tsnejs on 2026-05-09*

## 三岁版

tSNEJS 是一个"画画小帮手"，能把好多好多数字变成一幅你能看懂的画。比如你有100个东西的数据，看不出来谁和谁是一伙的，它就能把它们画在纸上，让长得像的靠在一起。就像把一堆混在一起的积木按颜色分开摆好！