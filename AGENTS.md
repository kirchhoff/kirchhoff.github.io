# AGENTS.md

This file provides guidance to Codex (Codex.ai/code) when working with code in this repository.

## Project Overview

Academic personal website for Ph.D. Wenda Tang, hosted on GitHub Pages at `kirchhoff.github.io`. Built with Jekyll using the [academicpages](https://github.com/academicpages/academicpages.github.io) theme (forked from Minimal Mistakes).

## Local Development

```bash
bundle install          # Install Ruby dependencies (delete Gemfile.lock if errors)
bundle exec jekyll liveserve   # Serve at localhost:4000 with live reload
```

Use `_config.dev.yml` as an override for local development (sets URL to localhost, disables analytics, expands CSS):
```bash
bundle exec jekyll serve --config _config.yml,_config.dev.yml
```

JS assets are built via npm:
```bash
npm run build:js   # Uglifies JS into assets/js/main.min.js
```

## Architecture

- **`_config.yml`** — Primary site configuration: author info, social links, collections, plugins, defaults. Must restart server after changes.
- **`_data/navigation.yml`** — Top navigation bar links. Currently only shows "CV".
- **Collections** (each has `output: true` in `_config.yml`):
  - `_publications/` — Academic papers (markdown with YAML front matter)
  - `_talks/` — Conference presentations
  - `_teaching/` — Teaching experience
  - `_portfolio/` — Project portfolio
  - `_posts/` — Blog posts
- **`_pages/`** — Standalone pages (about, cv, publications index, etc.). Included via `_config.yml`'s `include` directive since Jekyll ignores underscore dirs by default.
- **`_layouts/`** — Page templates. `default.html` wraps everything; `single.html` for most content; `talk.html` for talks; `archive.html` for listing pages.
- **`_includes/`** — Reusable HTML partials (author profile sidebar, head/footer, SEO, analytics, comments, etc.).
- **`_sass/`** — SCSS partials compiled by Jekyll.
- **`images/`** — Site images (author avatar, content images).
- **`files/`** — Downloadable files (PDFs, etc.), served at `/files/filename`.
- **`markdown_generator/`** — Python/Jupyter scripts to generate publication and talk markdown files from TSV data.

## Content Conventions

Content files use YAML front matter. Publications example:
```yaml
---
title: "Paper Title"
collection: publications
permalink: /publication/slug
date: 2024-01-01
venue: 'Conference Name'
---
```

The `permalink` in front matter determines the URL path. Collection type determines which layout defaults apply (configured in `_config.yml` under `defaults`).

## Key Configuration

- Site URL: `https://kirchhoff.github.io`
- Author avatar: set via `author.avatar` in `_config.yml` (filename in `images/`)
- Google Scholar, GitHub, email: configured under `author` in `_config.yml`
- Plugins: jekyll-paginate, jekyll-sitemap, jekyll-gist, jekyll-feed, jekyll-redirect-from
