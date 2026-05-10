# covid-sanity (biomed-sanity)

**GitHub:** https://github.com/karpathy/covid-sanity
**Stars:** 391 | **Forks:** 54 | **Language:** Python
**License:** MIT

## 项目介绍

整理来自 medRxiv 和 bioRxiv 的 COVID-19 SARS-CoV-2 预印本。原始数据来自 bioRxiv 页面。该项目让数据可搜索、可排序等。"最相似"搜索使用基于摘要 tfidf 特征向量训练的 exemplar SVM。

在线运行于 [biomed-sanity.com](https://biomed-sanity.com)（因为"covid-sanity"这个术语被"保护"了，无法注册 covid-sanity.com）。

注意：相似度搜索的质量取决于超参数，如 SVM 训练中的 `C` 和 `max_features`（当前设置为 2000）。

该项目在精神上是前一个项目 [arxiv-sanity](https://github.com/karpathy/arxiv-sanity-preserver) 的延续。

covid-sanity 是新冠病毒研究论文的"整理小能手"。在疫情期间科学家们写了好多好多关于病毒的文章，这个工具就帮大家把这些论文收在一起、排好顺序，还能找出"这篇和那篇好像差不多"的文章。就像帮你整理一桌子乱糟糟的画纸！

## 本地开发

```bash
$ pip install -r requirements.txt
$ python run.py
$ export FLASK_APP=serve.py
$ flask run
```

## 生产部署

推荐配置：NGINX 和 Gunicorn。服务器在 screen 会话中运行，配合 `pull.sh` 脚本每小时更新。Crontab 示例：

```
3 * * * * /root/covid-sanity/pull.sh > /root/cron.log 2>&1
```

## Twitter 集成

可选。配置 python-twitter API 并将密钥写入 `twitter.txt`。`twitter_daemon.py` 进程循环拉取每篇论文的推文。

## 许可证

MIT

---

*数据获取自 https://github.com/karpathy/covid-sanity (2026-05-09)*