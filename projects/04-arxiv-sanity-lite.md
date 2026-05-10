# arxiv-sanity-lite

**GitHub:** https://github.com/karpathy/arxiv-sanity-lite
**Website:** https://arxiv-sanity-lite.com
**Stars:** 1.6k | **Forks:** 192 | **Language:** Python
**License:** MIT

## 项目介绍

从零重写的精简版 arxiv-sanity。定期轮询 arxiv API 获取新论文。用户可以标记感兴趣的论文，系统基于论文摘要的 tfidf 特征训练 SVM，为每个标签推荐新论文。支持搜索、排名、排序、筛选等操作，界面美观。还可以根据你的标签每天通过邮件发送新论文推荐。

线上版本正在 [arxiv-sanity-lite.com](https://arxiv-sanity-lite.com) 运行。

这是"论文小助手"的轻便版——它更简单、更省地方，每天帮你看看有没有新论文出来，然后按你喜欢的"标签"给你推荐新的。还会每天发邮件告诉你："今天有新的论文哦！"

## 如何运行

### 更新数据库（通常通过 cron 调度）：

```bash
#!/bin/bash
python3 arxiv_daemon.py --num 2000
if [ $? -eq 0 ]; then
    echo "检测到新论文！运行 compute.py"
    python3 compute.py
else
    echo "没有新论文被添加，跳过特征计算"
fi
```

### 本地启动 flask 服务器：

```
export FLASK_APP=serve.py; flask run
```

所有数据库存储在 `data` 目录中。生产环境下，作者推荐在 Linode "Nanode 1 GB" 实例上运行，索引约 3 万篇论文，每月仅需 5 美元。

### （可选）定期发送邮件：
参见 `send_emails.py` 脚本。需要 `pip install sendgrid`。通过每日 cron 任务运行。

## 环境要求

```
pip install -r requirements.txt
```

## 待办事项
- 适配移动端，使用 media queries 优化页面
- 将 metas 表的 sqlitedict 替换为原生的 sqlite 表
- 构建反向索引，加快搜索速度

## 许可证

MIT

---

*数据获取自 https://github.com/karpathy/arxiv-sanity-lite (2026-05-09)*