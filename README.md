# Haoze Chang's website

Academic homepage and Markdown notes for https://haozechang.github.io.
The layout is inspired by [Jon Barron's website](https://jonbarron.info/).

## Local preview

```bash
bundle install
bundle exec jekyll serve --host 127.0.0.1 --port 4000 --no-watch
```

Open http://localhost:4000. If using a remote server, forward port 4000
with SSH or your editor. `--no-watch` avoids the server's exhausted inotify
watch limit. Restart Jekyll after editing any source file.

## Content

- `index.html`: introduction, education, and homepage sections.
- `_data/publications.json`: seven publications, grouped by year in descending order. Each paper's `image` field points to its figure under `assets/images/pub/`. Five papers come from Google Scholar and publisher records; two NeurIPS 2026 papers are verified against the official conference pages and have no page numbers.
- `_posts/`: Markdown notes; the nine local notes and the additional LaTeX note from the old repository are preserved verbatim.
- `post_imgs/`: original note images, with their existing paths.
- `assets/cv.pdf`: existing CV.
- `assets/images/profile.jpg`: portrait extracted from the existing CV.
- `assets/css/site.css`: homepage and article styles.
- `assets/fonts/`: self-hosted Lato fonts, matching the reference site, with their license.
- `assets/css/syntax.css`: code highlighting generated with `bundle exec rougify style github`.

Add a note as `_posts/YYYY-MM-DD-title.md`:

```markdown
---
title: "Your note title"
date: 2026-11-17
---

Write Markdown here.
```

The note appears automatically in `/notes/`, the homepage, and the RSS feed.
Put note images under `post_imgs/` and reference `/post_imgs/your-image.png`.

## GitHub Pages

Use the existing `HaozeChang/HaozeChang.github.io` repository. There is no
need to delete or recreate it. Replace its old website files with this
project's source files, including `.github/workflows/pages.yml`.

In the repository, set **Settings → Pages → Build and deployment → Source**
to **GitHub Actions**. Push to `master` or `main` to build and publish.
The workflow also offers a manual **Run workflow** button.

The build uses the locked Jekyll dependencies rather than a separate theme.
`_site/`, caches, and local dependencies are ignored and should not be committed.

## Materials to update

The personal introduction, education dates, and CV come from the previous
local site. The contact email is `hzchang@stu.xmu.edu.cn`, as provided by the author.
Teaching and academic services also follow the author-provided information.

To re-extract the CV portrait, run `pdfimages -f 1 -l 1 -j assets/cv.pdf /tmp/cv-portrait`
and copy its first JPEG to `assets/images/profile.jpg`.

## Publication metadata

The five published papers were checked against the [Google Scholar profile](https://scholar.google.com/citations?user=VT-KkjgAAAAJ)
and publisher-deposited Crossref records on 2026-11-17. DOI and metadata source URLs
are kept in the data file without adding publication links to the page.

Publication grouping and displayed years follow the author's requested years:
the SNR adaptive attention TVT paper is listed under 2025, and the attention-based
JSCC WiSATS paper under 2024. Journal volume, issue, and pages retain the
publisher-registered metadata. `scholar_year` retains the profile's original year.

The two NeurIPS 2026 papers are listed without volume, issue, or page numbers.
Titles and complete author order were checked against the official poster pages:

- https://neurips.cc/virtual/2026/poster/151724
- https://neurips.cc/virtual/2026/poster/153081
