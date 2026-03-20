# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Academic research lab website for the Body Pain Perception Lab (Aarhus University, Denmark). Built with Jekyll using the Academic Pages template, deployed via GitHub Pages.

## Build & Development Commands

```bash
# Local development (requires Ruby/Bundler)
bundle install
bundle exec jekyll serve -l    # Serves at localhost:4000 with live reload

# Docker alternative
docker compose up              # Serves at localhost:4000

# JavaScript assets
npm run build:js               # Minify/combine JS into assets/js/main.min.js
npm run watch:js               # Watch mode for JS changes
```

No test infrastructure exists.

## Architecture

**Jekyll Collections** — the core content model:
- `_publications/` — 60+ papers, named `YYYY-MM-DD-slug.md`, categorized as manuscripts/conferences/preprints/books
- `_people/` — Lab members, numbered files (`01_FF.md`, `02_AGM.md`, etc.) controlling display order
- `_pages/` — Site pages (about, projects, publications, news, join)

**Layout hierarchy**: `compress.html` → `default.html` → `single.html`/`talk.html`

**Data files** (`_data/`): `navigation.yml` defines the site menu; `authors.yml` for contributor metadata.

**Markdown generators** (`markdown_generator/`): Python/Jupyter scripts that convert TSV files into collection markdown files. Used for bulk content generation.

**Styling**: SASS in `_sass/`, compiled by Jekyll. Theme customization in `_sass/theme/`.

## Content Conventions

Publication frontmatter pattern:
```yaml
---
title: "Paper Title"
collection: publications
category: manuscripts    # manuscripts | conferences | preprints | books
permalink: /publication/YYYY-MM-DD-slug
date: YYYY-MM-DD
venue: 'Journal Name'
---
```

People files use numbered prefixes for ordering and include bio, research interests, and social links (Google Scholar, ORCID).

News updates go in `_pages/news.md` as chronological entries.

## Key Configuration

- `_config.yml` — Jekyll settings, collection definitions, site metadata, plugin list
- Plugins: jekyll-feed, jekyll-sitemap, jekyll-redirect-from, jemoji, jekyll-paginate
- Markdown: kramdown with GFM input
- Build output (`_site/`) is gitignored
