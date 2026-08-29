# Brigitte Valeria

This Jekyll site compiles Tailwind CSS with `jekyll-tailwind` and its standalone Ruby binary.
Node.js is not required.

## Start

```sh
bundle install
bundle exec jekyll serve
```

Open `http://localhost:4000`.

## Build

```sh
bundle exec jekyll build
```

## Site Data

All profile and portfolio content lives in `_data/` and is exposed to templates as `site.data.<filename>`.
Use YAML lists for repeatable records and mappings for grouped fields.
Fields marked optional can be omitted or set to an empty value.

### `_data/profile.yml`

A single mapping for the site identity, biography, affiliation, and links.
`photo` is optional, but `photo_alt` must be set when a photo is used.

```yaml
name: "Full name"
handle: "site-handle"
title: "Full academic title"
short_title: "Short title"
specialization: "Research specialization"
tagline: "Short research statement"
department: "Department or unit"
institution: "Institution name"
affiliation_role: "Current role"
location: "City, country"
status_badge: "Current status"
photo: "/assets/images/profile.jpg" # optional
photo_alt: "Descriptive portrait alt text" # required with photo
terminal_prompt: "Terminal-style research summary"
about_paragraphs:
  - "Biography paragraph"
core_disciplines:
  - "Discipline"
knows_about:
  - "JSON-LD research topic"
contact:
  orcid: "0000-0000-0000-0000"
  orcid_url: "https://orcid.org/..."
  scholar_url: "https://scholar.google.com/..."
  github_url: "https://github.com/..."
  researchgate_url: "https://www.researchgate.net/..."
  cv_url: "/assets/files/cv.pdf"
```

### `_data/publications.yml`

A list of publication cards.
`doi`, `doi_url`, `pdf_url`, and `code_url` are optional.
Only populated URLs render action links.

```yaml
- title: "Publication title"
  authors: "Author One; Author Two"
  journal: "Journal name"
  year: "2026"
  status: "Published"
  type: "Peer-Reviewed Article"
  doi: "10.xxxx/example" # optional
  doi_url: "https://doi.org/..." # optional
  pdf_url: "/assets/files/publication.pdf" # optional
  code_url: "https://github.com/..." # optional
  tags:
    - "keyword"
```

### `_data/toolkit.yml`

A mapping with a `categories` list.
Each category contains one or more skill groups.

```yaml
categories:
  - id: "unique-slug"
    name: "Category name"
    badge: "SHORT_LABEL"
    icon: "Emoji or short icon"
    description: "Category summary"
    groups:
      - title: "Skill group"
        skills:
          - name: "Skill"
```

### `_data/timeline.yml`

A list of education milestones.
`advisor`, `highlight`, and `badge` are optional.

```yaml
- type: "education"
  degree: "Degree name"
  institution: "Institution name"
  location: "City, country"
  advisor: "Advisor name" # optional
  highlight: "Achievement or focus" # optional
  badge: "In Progress" # optional
```

### `_data/talks.yml`

A list of selected talk and poster records.
The entire "Selected Talks & Posters" section is hidden when this file is empty or contains `[]`.

```yaml
- type: "Poster"
  title: "Presentation title"
  event: "Conference or event"
  year: "2026"
  location: "City, country"
  tags:
    - "topic"
```

## GitHub Pages Deployment

The deployment workflow publishes commits pushed to `master` through GitHub
Pages. It builds the site with the pinned Ruby dependencies, including the
Tailwind compiler, and deploys the generated `_site` directory.

Before the first deployment, create the `Nixbrief/nixbrief.github.io`
repository without initializing it. Then add it as this repository's `origin`
and push `master`:

```sh
git remote add origin git@github.com:Nixbrief/nixbrief.github.io.git
git push -u origin master
```

In GitHub, open **Settings > Pages** and select **GitHub Actions** as the
publishing source. Set `brigittevaleria.dev` as the custom domain in those
Pages settings; a `CNAME` file is not used by GitHub Actions deployments.

At the DNS provider, create these records:

| Type | Host | Value |
| --- | --- | --- |
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | nixbrief.github.io |

Optionally add IPv6 `AAAA` records for `@`: `2606:50c0:8000::153`,
`2606:50c0:8001::153`, `2606:50c0:8002::153`, and
`2606:50c0:8003::153`.

Verify the domain in GitHub account settings before assigning it to the
repository. After DNS propagation and a successful deployment, enable
**Enforce HTTPS** in **Settings > Pages**. If the domain uses CAA records,
allow `letsencrypt.org`.
