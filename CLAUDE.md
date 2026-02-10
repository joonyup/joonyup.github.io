# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Jekyll-based academic personal website for JoonYup Park (Assistant Professor, University of Hawai'i at Manoa). Hosted on GitHub Pages, deployed automatically on push to master.

## Build & Development Commands

```bash
bundle install                 # Install Ruby dependencies
bundle exec jekyll serve       # Local dev server at http://localhost:4000
docker-compose up              # Alternative: run via Docker on port 4000
```

Theme skin changes (`theme_skin` in `_config.yml`) require restarting the server.

## Architecture

**Content-driven static site**: Almost all website content lives in a single file `_data/data.yml`. The Jekyll templating system renders this data through `_includes/` partials into the `_layouts/default.html` layout.

### Key files

- `_data/data.yml` — Single source of truth for all site content (profile, papers, education, research interests, references). Syntax errors here break the entire site.
- `_config.yml` — Jekyll settings, theme skin selection (ceramic/blue/turquoise/green/berry/orange), Google Analytics config.
- `_layouts/default.html` — Main page layout that assembles all `_includes/` partials.
- `_layouts/print.html` — Print-friendly layout.
- `index.html` — Entry point, uses default layout.

### Content sections (`_includes/`)

Each section of the page is a separate partial. The active ones for this site are: `sidebar.html`, `contact.html`, `career-profile.html`, `education.html`, `workingpapers.html`, `restingpapers.html`, `jobmarketpaper.html`, `references.html`. Other partials (experiences, projects, skills, publications) exist from the theme but are not actively used.

### Styling (`_sass/`)

- `_base.scss` — CSS Grid layout (10-column: 3 sidebar + 7 main content)
- `_responsive.scss` — Mobile breakpoints
- `_print.scss` — Print styles
- `skins/` — Color theme variants, selected via `_config.yml` `theme_skin`
- `assets/css/main.scss` — Entry point that imports all SASS

### Static assets

- `pdfs/` — Academic paper PDFs and CV, linked from `_data/data.yml`
- `assets/images/` — Profile photo and theme samples
- `assets/plugins/` — Vendored Bootstrap, jQuery, Font Awesome

## Content Updates

The most common task is updating `_data/data.yml` to add/edit papers, update the profile, or modify research interests. The YAML structure uses nested lists with fields like `title`, `coauthors`, `abstract`, `link`, `award`, and `presentations`.
