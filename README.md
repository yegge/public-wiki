# Yegge Public Wiki

This repository hosts the **Yegge Public Wiki**, a dark‑mode, searchable wiki powered by **MkDocs** + **Material** theme and deployed automatically with **GitHub Pages**.

---

## 🚀 Quickstart

### 1. Clone the repo

```bash
git clone https://github.com/yegge/public-wiki.git
cd public-wiki
```

### 2. Local preview

```bash
python3 -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install mkdocs mkdocs-material
mkdocs serve
```

Now open http://127.0.0.1:8000 in your browser.

### 3. Publish changes

Commit & push to `main`. GitHub Actions will auto‑build and deploy to the `gh-pages` branch. Pages then serves it live.

---

## 📂 Repo Layout

```text
public-wiki/
├─ docs/                 # All Markdown content
│  ├─ index.md           # Home page
│  ├─ guide/             # Guides and FAQ
│  ├─ about/             # Brand & assets
│  └─ assets/            # Logos, CSS, media
├─ mkdocs.yml            # MkDocs site config
├─ .gitignore            # Ignore build artifacts
└─ .github/workflows/    # Deploy workflow
```

---

## 🖼️ Branding

Logos go in `docs/assets/logos/`:

- `yegge-logo.jpeg`
- `yegge-logo-invert.jpeg`
- `angershade-mark.png`
- `thecorruptive-logo.jpeg`
- `short-icon.png`

These are referenced in the site config and brand page.

---

## 🔧 Deployment workflow

File: `.github/workflows/deploy.yml`

```yaml
name: Build and Deploy MkDocs

on:
  push:
    branches: [ "main" ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.x'
      - run: |
          python -m pip install --upgrade pip
          pip install mkdocs mkdocs-material
      - run: mkdocs gh-deploy --force
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

---

## 🌐 GitHub Pages

After the first deploy:

1. Go to **Settings → Pages**.
2. Set **Source** to **Deploy from branch**, pick `gh-pages`.
3. Your wiki will be live at:  
   https://yegge.github.io/public-wiki/

(Optional) Add `wiki.yegge.com` as a custom domain.

---

## 📖 Authoring

- Write in Markdown (`.md`) under `docs/`.
- Add to navigation in `mkdocs.yml`.
- Push to `main` → auto publish.

---

## ✅ Purpose

The goal is to keep authoring dead simple (Markdown only) while producing a polished, always‑up‑to‑date wiki with zero manual builds.
