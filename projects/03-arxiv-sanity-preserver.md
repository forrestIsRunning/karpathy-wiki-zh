# arxiv-sanity-preserver

**GitHub:** https://github.com/karpathy/arxiv-sanity-preserver
**Stars:** 5.7k | **Forks:** 1.4k | **Language:** Python
**License:** MIT

## 项目介绍

一个网页界面，旨在驯服 Arxiv 上铺天盖地的论文洪流。它让研究人员能够跟踪最新论文、搜索论文、按相似度对论文排序、查看近期热门论文、将论文添加到个人文库，并获得个性化推荐（无论是新论文还是旧论文）。

该代码正在 [www.arxiv-sanity.com](http://www.arxiv-sanity.com/) 上运行，覆盖了过去约 3 年来自机器学习领域（cs.[CV|AI|CL|LG|NE]/stat.ML）的 25,000 多篇 Arxiv 论文。

**更新（2021 年 11 月 27 日）：** 一个从零重写的版本 [arxiv-sanity-lite](https://arxiv-sanity-lite.com) 已经上线——更精简，聚焦于核心价值。

这就像你的"论文小助手"。每天有太多科学论文冒出来，根本看不过来，它就帮你自动从网上收论文、整理好，还能推荐你可能感兴趣的文章。就像有一个好朋友先帮你把好玩的东西挑出来，省得你在一大堆里面自己翻。

## 代码结构

### 索引代码
使用 Arxiv API 下载任何类别的最新论文，下载所有论文，提取所有文本，根据内容创建 tfidf 向量。后端抓取和计算：构建数据库、计算内容向量、创建缩略图、为用户计算 SVM。

### 用户界面
基于 Flask/Tornado/sqlite 的 Web 服务器，用于按相似度搜索和筛选论文。

## 依赖项

多个依赖：numpy、feedparser、scikit-learn、flask、flask_limiter、tornado、dateutil、scipy、sqlite3。还需要 ImageMagick 和 pdftotext（`sudo apt-get install imagemagick poppler-utils`）。

## 处理流程

1. 运行 `fetch_papers.py` — 查询 arxiv API，创建 `db.p`
2. 运行 `download_pdfs.py` — 将论文下载到 `pdf/`
3. 运行 `parse_pdf_to_text.py` — 从 PDF 导出文本到 `txt/`
4. 运行 `thumb_pdf.py` — 导出缩略图到 `thumb/`
5. 运行 `analyze.py` — 计算 tfidf 向量（保存 `tfidf.p`、`tfidf_meta.p`、`sim_dict.p`）
6. 运行 `buildsvm.py` — 为用户训练 SVM（导出 `user_sim.p`）
7. 运行 `make_cache.py` — 预处理，加快服务器启动速度
8. 使用 `serve.py` 运行 flask 服务器

**小贴士：** 为 analyze.py 的性能考虑，请搭配 BLAS（例如 OpenBLAS）使用 numpy。

## 在线运行

运行 `python serve.py --prod`。创建一个 `secret_key.txt` 文件。服务器通常在 screen 会话中运行。每日更新工作流依次执行 fetch_papers、download_pdfs、parse_pdf_to_text、thumb_pdf、analyze、buildsvm、make_cache 脚本。

## 许可证

MIT

---

*数据获取自 https://github.com/karpathy/arxiv-sanity-preserver (2026-05-09)*