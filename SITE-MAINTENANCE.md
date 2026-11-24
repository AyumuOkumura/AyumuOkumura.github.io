# Local preview and maintenance

This site uses al-folio v1 at upstream commit `e5f84cc8da64bc31d05a0733f0b832d9d77c084d`. The template's MIT license is retained in LICENSE.

## Preview

```sh
docker compose pull
docker compose up
```

Open `http://localhost:8080/`. To stop, press Ctrl+C or run `docker compose down`. Build and check output without running a server:

```sh
docker compose run --rm --no-deps jekyll bundle exec jekyll build --destination /srv/jekyll/_site
python -m unittest discover -s tests -v
```

## Editing

- `_data/cv_content.json`: paired English and Japanese profile sections. Keep matching IDs, dates, and order in sync. Entries are text from the November 2026 CV and are displayed in source order.
- `_data/cv_links.json`: verified external sources keyed by entry ID, shared across languages. Labels distinguish DOI, lab news, KAKEN, and GitHub; use a source-specific label when adding links.
- `_includes/cv_sections.liquid`: shared presentation of both homepages; this site-specific include is a local al-folio override. Check override compatibility after upgrading the upstream gems.
- `_pages/about.md` and `_pages/ja.md`: homepages; CV download pages are `_pages/cv_download*.md`.
- `assets/profile/portrait.jpg`: profile photo. Replace this file with an optimized, metadata-free JPEG, then check the image dimensions in `_includes/cv_sections.liquid` and preview both languages.
- `assets/pdf/Ayumu-Okumura-CV.pdf`: original-format bilingual CV. It contains a telephone number and is publicly downloadable when published. Update it only after reviewing the resulting PDF.

The source DOCX is not in this repository. GitHub Pages and a public repository expose their contents publicly. Before pushing, confirm the remote with `git remote -v` and review changes with `git status` and `git diff`.
