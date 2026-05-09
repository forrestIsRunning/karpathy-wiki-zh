# arxiv-sanity-lite

**GitHub:** https://github.com/karpathy/arxiv-sanity-lite
**Website:** https://arxiv-sanity-lite.com
**Stars:** 1.6k | **Forks:** 192 | **Language:** Python
**License:** MIT

## Description

A much lighter-weight arxiv-sanity from-scratch re-write. Periodically polls arxiv API for new papers. Allows users to tag papers of interest, and recommends new papers for each tag based on SVMs over tfidf features of paper abstracts. Supports search, rank, sort, slice and dice results in a pretty web UI. Can send daily emails with recommendations of new papers based on your tags.

A live version is running at [arxiv-sanity-lite.com](https://arxiv-sanity-lite.com).

## How to Run

### Update the database (typically scheduled via cron):

```bash
#!/bin/bash
python3 arxiv_daemon.py --num 2000
if [ $? -eq 0 ]; then
    echo "New papers detected! Running compute.py"
    python3 compute.py
else
    echo "No new papers were added, skipping feature computation"
fi
```

### Serve the flask server locally:

```
export FLASK_APP=serve.py; flask run
```

All database is stored inside the `data` directory. For production, the author recommends running on a Linode "Nanode 1 GB" instance indexing ~30K papers for $5/month.

### (Optional) Send periodic emails:
See `send_emails.py` script. Requires `pip install sendgrid`. Run in a daily cron job.

## Requirements

```
pip install -r requirements.txt
```

## Todos
- Make website mobile friendly with media queries
- Replace sqlitedict for metas table with proper sqlite table
- Build reverse index for faster search

## License

MIT

---

*Fetched from https://github.com/karpathy/arxiv-sanity-lite on 2026-05-09*