# covid-sanity (biomed-sanity)

**GitHub:** https://github.com/karpathy/covid-sanity
**Stars:** 391 | **Forks:** 54 | **Language:** Python
**License:** MIT

## Description

Organizes COVID-19 SARS-CoV-2 preprints from medRxiv and bioRxiv. Raw data comes from the bioRxiv page. The project makes the data searchable, sortable, and more. The "most similar" search uses an exemplar SVM trained on tfidf feature vectors from the abstracts.

Running live at [biomed-sanity.com](https://biomed-sanity.com) (couldn't register covid-sanity.com because the term was "protected").

Note: the quality of the similarity search depends on hyperparameters like `C` in SVM training and `max_features` (currently set at 2,000).

This project follows a previous one in spirit — [arxiv-sanity](https://github.com/karpathy/arxiv-sanity-preserver).

## Development (Local)

```bash
$ pip install -r requirements.txt
$ python run.py
$ export FLASK_APP=serve.py
$ flask run
```

## Production

Recommended setup: NGINX and Gunicorn. The server runs in a screen session with a `pull.sh` script for hourly updates. Crontab example:

```
3 * * * * /root/covid-sanity/pull.sh > /root/cron.log 2>&1
```

## Twitter Integration

Optional. Set up python-twitter API and write secrets to `twitter.txt`. The `twitter_daemon.py` process pulls tweets for every paper in cycles.

## License

MIT

---

*Fetched from https://github.com/karpathy/covid-sanity on 2026-05-09*

## 三岁版

covid-sanity 是新冠病毒研究论文的"整理小能手"。在疫情期间科学家们写了好多好多关于病毒的文章，这个工具就帮大家把这些论文收在一起、排好顺序，还能找出"这篇和那篇好像差不多"的文章。就像帮你整理一桌子乱糟糟的画纸！