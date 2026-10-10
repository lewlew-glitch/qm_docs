# Quartermaster Docs

MkDocs Material site for [Quartermaster](https://www.qmstack.com/), hosted on Vercel at
https://docs.qmstack.com/.

## Run it locally

```bash
python3 -m venv .venv
.venv/bin/pip install -r requirements.txt
.venv/bin/mkdocs serve        # live preview at http://127.0.0.1:8000
.venv/bin/mkdocs build --strict   # static site in ./site, fails on broken links
```

## Deploy

Vercel builds it from `vercel.json`: a fresh virtualenv, `mkdocs build --strict`, and the
`site/` folder served as static files. Push to `main` and Vercel publishes it; a push to any
other branch gets a preview URL first.

To change a page, edit its file under `docs/` on a branch and open a pull request.
