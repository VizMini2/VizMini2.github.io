# VizMini2.github.io

Documentation website for **VizMini2**, published with GitHub Pages at
<https://vizmini2.github.io/>.

This repository only contains **the built website** (static HTML generated with
Sphinx). The documentation sources live in the app repository
(`Rviz2-Mini/docs`), not here.

## Layout

| Path | Contents |
|---|---|
| `index.html`, `tabs/`, `config/`, `tutorials/`, `help/`, … | English documentation (site root) |
| `es/` | Spanish documentation (same tree) |
| `_static/` | Theme CSS/JS, logo (`vizmini2.svg`), screenshots (`shots/`) and videos (`clips/`) |
| `app-ads.txt` | AdMob declaration; it must stay at the root of the domain |
| `.nojekyll` | **Do not delete**: without it GitHub Pages ignores folders starting with `_` (`_static/`) and the site loses its styles |
| `LICENSE`, `README.md` | Repository files only |

## Building the website

The sources are two independent Sphinx projects, one per language, using the
`sphinx_rtd_theme` theme and `myst_parser` (to include Markdown):

```
Rviz2-Mini/docs/
├── en/            → published at the root
├── es/            → published under es/
└── _generated/    → per-language CHANGELOG.md, generated before building
```

1. Install the dependencies (once, preferably in a virtual environment):

   ```bash
   python3 -m venv ~/.venvs/vizmini-docs
   source ~/.venvs/vizmini-docs/bin/activate
   pip install sphinx sphinx-rtd-theme myst-parser
   ```

2. Generate `docs/_generated/<language>/CHANGELOG.md` with the step provided by
   the app repository (the app's `CHANGELOG.md` adapted to each language).

3. Build both languages into a temporary folder:

   ```bash
   cd Rviz2-Mini/docs
   sphinx-build -b html -d _build/doctrees/en en _build/html
   sphinx-build -b html -d _build/doctrees/es es _build/html/es
   ```

   `-d` keeps the Sphinx cache (`.doctrees`) out of the output, so it is not
   published.

4. Copy the result into this repository without touching the repository's own
   files:

   ```bash
   rsync -a --delete \
     --exclude .git --exclude README.md --exclude LICENSE \
     --exclude .nojekyll --exclude app-ads.txt --exclude .buildinfo \
     _build/html/ /path/to/VizMini2.github.io/
   ```

   `--delete` removes pages that no longer exist in the documentation. The
   exclusions are essential: without them `.git` and the other files listed in
   the table above would be deleted.

> The logo (`_static/vizmini2.svg`) and the favicon (`_static/favicon.png`, 64×64)
> come from the sources: keep the current ones in `docs/en/_static/` and
> `docs/es/_static/`, and set `html_favicon = "_static/favicon.png"` in both
> `conf.py` files. Otherwise a rebuild brings back the old icon and the 600 KB SVG
> as favicon.

## Testing locally

GitHub Pages serves static files, so any HTTP server will do:

```bash
cd VizMini2.github.io
python3 -m http.server 8000
```

Then open <http://localhost:8000/> (English) and <http://localhost:8000/es/>
(Spanish). Stop the server with Ctrl+C.

- Do not open `index.html` by double-clicking it (`file://`): search and some
  scripts do not work that way.
- All links are relative, so what works locally works the same once published.
- Browsers cache the favicon aggressively: if you still see the old one, do a
  hard reload (Ctrl+Shift+R) or use a private window.
- To check for broken links automatically, from the sources:
  `sphinx-build -b linkcheck en _build/linkcheck`.

## Publishing

1. Review the changes and push them to `main`:

   ```bash
   git status
   git add -A
   git commit -m "Docs: <what changes>"
   git push origin main
   ```

2. The first time, on GitHub: **Settings → Pages → Build and deployment →
   Source: Deploy from a branch**, branch `main`, folder `/ (root)`.

3. GitHub takes a minute or two to publish it. Progress is shown in the
   **Actions** tab ("pages build and deployment"). If the changes do not show up,
   do a hard reload (Ctrl+Shift+R).

## License

Apache 2.0, see [LICENSE](LICENSE).
