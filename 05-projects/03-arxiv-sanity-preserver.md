# arxiv-sanity-preserver

**GitHub:** https://github.com/karpathy/arxiv-sanity-preserver
**Stars:** 5.7k | **Forks:** 1.4k | **Language:** Python
**License:** MIT

## Description

A web interface that attempts to tame the overwhelming flood of papers on Arxiv. It allows researchers to keep track of recent papers, search for papers, sort papers by similarity to any paper, see recent popular papers, add papers to a personal library, and get personalized recommendations of (new or old) Arxiv papers.

This code is running live at [www.arxiv-sanity.com](http://www.arxiv-sanity.com/), serving 25,000+ Arxiv papers from Machine Learning (cs.[CV|AI|CL|LG|NE]/stat.ML) over the last ~3 years.

**Update (Nov 27, 2021):** A from-scratch re-write called [arxiv-sanity-lite](https://arxiv-sanity-lite.com) is available — a smaller version focusing on the core value proposition.

## Code Layout

### Indexing Code
Uses Arxiv API to download recent papers in any categories, downloads all papers, extracts all text, creates tfidf vectors based on content. Backend scraping and computation: building a database, calculating content vectors, creating thumbnails, computing SVMs for users.

### User Interface
A web server (based on Flask/Tornado/sqlite) for searching and filtering papers by similarity.

## Dependencies

Multiple: numpy, feedparser, scikit-learn, flask, flask_limiter, tornado, dateutil, scipy, sqlite3. Also ImageMagick and pdftotext (`sudo apt-get install imagemagick poppler-utils`).

## Processing Pipeline

1. Run `fetch_papers.py` — query arxiv API, create `db.p`
2. Run `download_pdfs.py` — download papers to `pdf/`
3. Run `parse_pdf_to_text.py` — export text from PDFs to `txt/`
4. Run `thumb_pdf.py` — export thumbnails to `thumb/`
5. Run `analyze.py` — compute tfidf vectors (saves `tfidf.p`, `tfidf_meta.p`, `sim_dict.p`)
6. Run `buildsvm.py` — train SVMs for users (exports `user_sim.p`)
7. Run `make_cache.py` — preprocessing for faster server start
8. Run the flask server with `serve.py`

**Protip:** Set up numpy with BLAS (e.g. OpenBLAS) for analyze.py performance.

## Running Online

Run `python serve.py --prod`. Create a `secret_key.txt` file. The server is typically run in a screen session. The daily update workflow runs fetch_papers, download_pdfs, parse_pdf_to_text, thumb_pdf, analyze, buildsvm, make_cache scripts sequentially.

## License

MIT

---

*Fetched from https://github.com/karpathy/arxiv-sanity-preserver on 2026-05-09*