# Academic Profile Website — Agent Replication Plan

This document is an execution plan designed for autonomous coding agents (or human developers) to replicate this personal academic profile website from scratch or for another researcher.

---

## 1. Project Specifications

| Property | Value |
| :--- | :--- |
| **Framework** | Jekyll 4 (`~> 4.4`) |
| **Styling** | Tailwind CSS v3 (standalone Ruby binary via `jekyll-tailwind` + `tailwindcss-ruby`) |
| **Node.js / npm** | **Not required** (Zero npm dependencies) |
| **Architecture** | 100% Data-Driven (`_data/*.yml` decoupled from Liquid HTML templates) |
| **Aesthetic** | Clean High-Contrast Laboratory & Tech (`JetBrains Mono`, `Inter`, Chlorophyll Green `#047857`, Slate `#0f172a`, Lab Grid) |
| **Standards** | WCAG 2.1 AA Accessible, Semantic HTML5, Schema.org JSON-LD Person Metadata, Google Scholar SEO |

---

## 2. Step-by-Step Implementation Flow

```
1. Environment & Gems ──► 2. Tailwind & CSS ──► 3. Data Architecture ──► 4. Layout & SEO/a11y ──► 5. index.html ──► 6. Verification
```

---

### Step 1: Environment & Dependency Setup

1. **Create `mise.toml`** (or `.ruby-version`):
   ```toml
   [tools]
   ruby = "4.0.5"
   ```

2. **Create `Gemfile`**:
   ```ruby
   source "https://rubygems.org"

   gem "jekyll", "~> 4.4"

   group :jekyll_plugins do
     gem "jekyll-seo-tag"
     gem "jekyll-tailwind"
     gem "tailwindcss-ruby", ">= 3", "< 4"
   end
   ```

3. **Create `_config.yml`**:
   ```yaml
   title: "Brigitte Valeria"
   tagline: "PhD Candidate in Biological Sciences | Plant Molecular Biology & Functional Genomics"
   description: "Academic profile and research portfolio of Brigitte Valeria, PhD candidate specializing in plant molecular biology, functional genomics, and CRISPR/Cas gene editing."
   url: "https://brigittevaleria.dev"
   baseurl: ""
   lang: "en"

   author:
     name: "Brigitte Valeria"
     job_title: "PhD Student / Graduate Researcher"
     works_for: "Center for Research in Biological Sciences"

   social:
     name: "Brigitte Valeria"
     links:
       - "https://orcid.org"
       - "https://scholar.google.com"
       - "https://github.com"
       - "https://researchgate.net"

   plugins:
     - jekyll-seo-tag
     - jekyll-tailwind

   tailwind:
     input: assets/css/app.css
     output: _site/assets/css/app.css
     minify: true
   ```

---

### Step 2: Tailwind & Custom CSS Theme Setup

1. **Create `tailwind.config.js`**:
   Configure custom font stacks, the `bio` (emerald) and `lab` (slate) palettes, and content scanning paths:
   ```javascript
   /** @type {import('tailwindcss').Config} */
   module.exports = {
     content: [
       "./**/*.{html,md}",
       "./_layouts/**/*.html",
       "./_includes/**/*.html",
       "./_data/**/*.yml"
     ],
     theme: {
       extend: {
         fontFamily: {
           sans: ['"Inter"', '"Plus Jakarta Sans"', 'system-ui', 'sans-serif'],
           mono: ['"JetBrains Mono"', '"Fira Code"', 'ui-monospace', 'monospace'],
         },
         colors: {
           bio: {
             50: "#ecfdf5", 100: "#d1fae5", 200: "#a7f3d0", 300: "#6ee7b7",
             400: "#34d399", 500: "#10b981", 600: "#059669", 700: "#047857",
             800: "#065f46", 900: "#064e3b", 950: "#022c22"
           },
           lab: {
             50: "#f8fafc", 100: "#f1f5f9", 200: "#e2e8f0", 300: "#cbd5e1",
             400: "#94a3b8", 500: "#64748b", 600: "#475569", 700: "#334155",
             800: "#1e293b", 900: "#0f172a", 950: "#020617"
           }
         }
       }
     },
     plugins: []
   };
   ```

2. **Create `assets/css/app.css`**:
   Import Google Fonts (`Inter` + `JetBrains Mono`), define `@tailwind` directives, `.bg-grid-lab` background utility, accessible `:focus-visible` styling, and `prefers-reduced-motion` fallbacks.

---

### Step 3: Data Architecture (`_data/*.yml`)

Create the 6 structured YAML schemas in `_data/`:

1. **`_data/profile.yml`**: Personal details, profile handle, title, institution, affiliation role, location, research status badge, terminal prompt string, photo path, social URLs (ORCID, Scholar, GitHub, ResearchGate), core disciplines, and quick stats matrix.
2. **`_data/research.yml`**: List of research pillars with `code_id` (e.g. `RES_01`), `summary`, `details`, `model_organisms`, `methods`, and `status`.
3. **`_data/publications.yml`**: Papers and preprints with `title`, `authors`, `journal`, `year`, `status` (`Published` or `Preprint`), `doi_url`, `code_url`, `pdf_url`, `abstract`, and `tags`.
4. **`_data/toolkit.yml`**: Categorized dual-matrix skills (`wet_lab` and `dry_lab`), subdivided into functional groups with skill levels (`Expert`, `Advanced`, `Proficient`).
5. **`_data/timeline.yml`**: Academic degrees, institutions, advisors, periods, and thesis highlights.
6. **`_data/talks.yml`**: Presentations, conference posters, invited workshops with locations and dates.

---

### Step 4: Asset Creation

1. **`assets/favicon.svg`**: SVG icon featuring emerald background with monogram/DNA motif.
2. **`assets/images/avatar-placeholder.svg`**: SVG placeholder with tech corner reticles, scientist silhouette, and molecular nodes.

---

### Step 5: Master Layout & SEO/a11y (`_layouts/default.html`)

Implement `_layouts/default.html` adhering to strict conventions:
- **Skip Link**: `<a href="#main-content" class="sr-only focus:not-sr-only ...">Skip to main content</a>`.
- **Landmarks**: `<header>`, `<nav aria-label="Main Navigation">`, `<main id="main-content" tabindex="-1">`, `<footer role="contentinfo">`.
- **SEO & Schema**: Use `{% seo %}` plugin for primary Open Graph/Twitter tags. Add JSON-LD `Person` structured data with `sameAs` and `knowsAbout` properties.
- **Academic Metadata**: Add `<meta name="citation_author">` and `<meta name="citation_institution">`.
- **Header Status Bar**: Keep the lab status and ORCID record, but avoid fabricated system/version labels such as `SYS: PLANT_GENOMICS_v3.4`.
- **Profile Branding**: Render the navigation sub-label from `site.data.profile.handle` with the `//` terminal-style prefix.
- **Rule**: Never add manual `<title>` tags above `{% seo %}` (prevents duplicate title tags in build output).

---

### Step 6: Single-Page Template (`index.html`)

Build `index.html` with modular sections iterating over `site.data`:
1. **Hero Spec Sheet**:
   - Terminal prompt badge (`terminal // profile_loader.sh`).
   - Profile photo frame (centered with `mx-auto` on mobile, left-aligned on desktop `sm:mx-0`).
   - Specimen badge, name heading, tagline, institution, and quick stats grid.
   - Quick connect buttons for Google Scholar, ORCID, GitHub, and ResearchGate.
2. **Section 01: About (`#about`)**: Narrative background and affiliation cards. Render core discipline badges by looping over `site.data.profile.core_disciplines`, and render the affiliation role from `site.data.profile.affiliation_role`. Do not include lab coordinates or a physical lab address section.
3. **Section 02: Research (`#research`)**: Grid of research project cards with methods and model organism tags.
4. **Section 03: Publications (`#publications`)**: Publication articles with status badges, DOI links, and abstract snippets.
5. **Section 04: Toolkit (`#toolkit`)**: Wet Lab vs. Dry Lab dual skill matrix.
6. **Section 05: Academic Journey (`#timeline`)**: Vertical milestone timeline alongside conference talks.

---

### Step 7: Build Verification & Checklist

Run the verification suite:
```bash
# 1. Install ruby dependencies
bundle install

# 2. Build and verify static output
bundle exec jekyll build

# 3. Test dev server locally
bundle exec jekyll serve
```

---

## 3. Critical Agent Guardrails & Gotchas

* **Zero Hardcoded Content**: All names, publications, skills, and links must be read from `_data/*.yml`.
* **No Node.js**: Do not run `npm install` or `npx tailwindcss`. The ruby gem handles compilation.
* **Accessibility (a11y)**:
  * Every external link (`target="_blank"`) MUST have `rel="noopener noreferrer"` and `<span class="sr-only">(opens in a new tab)</span>`.
  * Decorative SVGs and emojis must have `aria-hidden="true"`.
  * Heading hierarchy must remain strictly ordered (`h1` → `h2` → `h3` → `h4`).
* **SEO**: Full HTTPS URLs in `_config.yml` (`https://brigittevaleria.dev`) to ensure valid canonical links and JSON-LD schema URLs.
