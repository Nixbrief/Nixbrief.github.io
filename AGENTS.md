# AGENTS.md

## Project Overview

Personal academic website for Brigitte Valeria (PhD candidate in Plant Molecular Biology & Functional Genomics), built with Jekyll 4 and Tailwind CSS v3.
Read @DESIGN.md file for design and content guidelines.

## Toolchain & Environment

- **Ruby version:** Managed via `mise.toml` (`ruby = "4.0.5"`).
- **Tailwind compilation:** Handled via `jekyll-tailwind` and `tailwindcss-ruby` standalone gem binary. **Node.js / npm is not required** for building or serving.

## Essential Commands

- **Install dependencies:** `bundle install`
- **Dev server:** `bundle exec jekyll serve` (runs at `http://localhost:4000`)
- **Build / Verify:** `bundle exec jekyll build`

## Architecture & Conventions

### Page Structure

- `/` contains the profile hero and Recent Publications.
- `/about/` contains About Me plus a native exclusive accordion for Research Interest, Toolkit, and Education. Keep the three `<details>` elements on the shared `name="about-sections"` group.
- The footer uses a three-column grid: the profile block spans two columns and Academic Links occupy the third. Do not restore the removed Specimen & Systems column without a content need.

### 1. Data-Driven Content (`_data/`)

All profile details, publications, and skills are decoupled from HTML:

- `_data/profile.yml`: Academic credentials, tagline, institution, social/academic links, photo path, quick stats.
- `_data/publications.yml`: Articles and preprints with DOI, links, abstract, tags.
- `_data/toolkit.yml`: Dual-matrix skills (`wet_lab` and `dry_lab`).
- `_data/timeline.yml`: Degrees, honors, institutions.
- `_data/talks.yml`: Presentations, posters, and workshops.

> **Rule:** Edit `_data/*.yml` for content updates. Do not hardcode content into `index.html`.

### 2. Layout & SEO Rules (`_layouts/default.html` & `_config.yml`)

- `{% seo %}` plugin (`jekyll-seo-tag`) handles primary meta and Open Graph tags.
- **Do not** add explicit `<title>` or `<meta name="description">` tags in `_layouts/default.html` (causes duplicate title tags in build output).
- URL and social links in `_config.yml` must use full HTTPS paths (`https://brigittevaleria.dev`) for valid Open Graph and canonical links.
- Keep JSON-LD `Person` schema updated if academic affiliations or specializations change.

### 3. Accessibility (a11y) Rules

- Maintain `#main-content` skip link and corresponding `id="main-content"` on `<main>`.
- All external links (`target="_blank"`) must include `rel="noopener noreferrer"` and `<span class="sr-only">(opens in a new tab)</span>`.
- Decorative iconography/emojis must have `aria-hidden="true"` or explicit `role="img"` with `aria-label`.
