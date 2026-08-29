# Design System & UI Specification

Welcome to the **Brigitte Valeria Academic Design System**. This specification documents the visual language, color tokens, typography scales, layout frameworks, reusable UI components, accessibility rules, and templates used across the site.

Use this guide when authoring new pages, blog articles, research dossiers, protocol notes, or project showcases to ensure visual consistency and strict adherence to the site's aesthetic and accessibility standards.

---

## 1. Aesthetic Philosophy & Brand Identity

The site's visual identity embodies **"Clean High-Contrast Laboratory & Tech"** — merging the rigorous, organic world of plant molecular biology (*Wet Lab*) with the precision, structure, and computational syntax of genomics bioinformatics (*Dry Lab*).

### Core Pillars

1. **Scientific Precision & Spec Sheet Layouts**: Elements resemble laboratory instrumentation logs, scientific protocols, and terminal outputs (`JetBrains Mono`, `//` comments, bracketed IDs, metadata badges).
2. **Dual Nature Palette**:
   - **Bio / Chlorophyll (`bio-*`)**: Deep plant greens, emerald accents, and cellular highlights representing biological matter, live assays, and active research.
   - **Tech & Lab Neutrals (`lab-*`, `tech-*`)**: Clean slate, sterile laboratory whites, cool grays, and deep obsidian terminal blocks representing computational infrastructure.
3. **Subtle Tactile Textures**: Engineering-grade background grids (`.bg-grid-lab`, `.bg-dots-lab`), micro-interactions, reticle corner markers, and smooth depth transitions.
4. **Uncompromising Accessibility & Performance**: Zero client-side JavaScript frameworks, lightweight standalone CSS, WCAG 2.1/2.2 AA compliant contrast, full keyboard navigability, and respect for `prefers-reduced-motion`.

---

## 2. Color System & Design Tokens

All colors are configured in `tailwind.config.js` and follow an explicit semantic mapping:

### 2.1 Palette Breakdown

```
BIO PALETTE (Chlorophyll / Biological Focus)
┌──────────┬──────────┬──────────┬──────────┬──────────┬──────────┬──────────┬──────────┬──────────┐
│ bio-50   │ bio-100  │ bio-200  │ bio-400  │ bio-500  │ bio-600  │ bio-700  │ bio-800  │ bio-900  │
│ #ecfdf5  │ #d1fae5  │ #a7f3d0  │ #34d399  │ #10b981  │ #059669  │ #047857  │ #065f46  │ #064e3b  │
└──────────┴──────────┴──────────┴──────────┴──────────┴──────────┴──────────┴──────────┴──────────┘

LAB NEUTRALS (Sterile Slate / Surface & Text)
┌──────────┬──────────┬──────────┬──────────┬──────────┬──────────┬──────────┬──────────┬──────────┐
│ lab-50   │ lab-100  │ lab-200  │ lab-300  │ lab-500  │ lab-600  │ lab-700  │ lab-900  │ lab-950  │
│ #f8fafc  │ #f1f5f9  │ #e2e8f0  │ #cbd5e1  │ #64748b  │ #475569  │ #334155  │ #0f172a  │ #020617  │
└──────────┴──────────┴──────────┴──────────┴──────────┴──────────┴──────────┴──────────┴──────────┘

TECH ACCENTS (Computational Biology / Dry Lab)
┌──────────┬──────────┬──────────┬──────────┬──────────┬──────────┐
│ tech-50  │ tech-100 │ tech-200 │ tech-500 │ tech-700 │ tech-900 │
│ #f0f9ff  │ #e0f2fe  │ #bae6fd  │ #0ea5e9  │ #0369a1  │ #0c4a6e  │
└──────────┴──────────┴──────────┴──────────┴──────────┴──────────┘
```

### 2.2 Semantic Usage Guidelines

| Token | Hex / Class | Primary Use Cases |
| :--- | :--- | :--- |
| **Page Background** | `bg-lab-50` (`#f8fafc`) | Clean solid canvas surface |
| **Card Surface** | `bg-white` (`#ffffff`) | Primary containers, articles, content panels |
| **Sub-panel Surface** | `bg-lab-50` / `bg-lab-100` | Code blocks, nested spec summaries, sidebars |
| **Terminal Surface** | `bg-lab-900` (`#0f172a`) | Terminal headers, CLI blocks, specimen overlays |
| **Primary Text** | `text-lab-900` / `text-lab-950` | Headings, titles, high-contrast body text |
| **Secondary Text** | `text-lab-700` | Narrative paragraphs, descriptive copy |
| **Muted / Metadata** | `text-lab-500` / `text-lab-600` | Section labels (`//`), dates, locations, counts |
| **Primary Brand Accent**| `bg-bio-800` / `text-bio-800` | Primary buttons, active badges, key link hovers |
| **Focus Indicator** | `outline: 2px solid #047857` | Global `:focus-visible` ring on interactable elements |
| **Text Selection** | `selection:bg-bio-100` | Highlight background (`#d1fae5`), text `bio-950` |
| **Success / Active** | `bg-emerald-100 text-emerald-900` | Published papers, active status, completed runs |
| **Warning / In Review** | `bg-amber-100 text-amber-900` | Preprints, WIP pipelines, provisional protocols |

### 2.3 Dark Theme

The site features a **High-Precision Bioluminescent Laboratory** dark theme that pairs deep obsidian slate surfaces with luminous emerald accents and crisp slate typography for optimal contrast and reduced eye strain.

- **Default behavior:** When a visitor has not made a choice, use `prefers-color-scheme: dark` to select the initial theme and continue following system changes.
- **Explicit choice:** The header control is a binary light/dark switch. A click saves the selected value to `localStorage` under `theme`, which takes precedence over the system setting on future visits.
- **Theme application:** The `dark` class is applied to the root `<html>` element before the page renders, avoiding a flash of the wrong theme. Theme styles are defined in `assets/css/app.css` under `.dark` selectors and Tailwind's `darkMode: 'class'`.
- **Surface hierarchy:**
  - **Canvas Background:** Deep obsidian ground `#0b0f19`.
  - **Primary Cards & Containers:** Elevated laboratory slate `#121927` with crisp boundary borders `#26354d`.
  - **Sub-panels & Nested Boxes:** Elevated slate `#182235`.
  - **Terminal CLI Windows:** Deepest obsidian black `#060911` with contrasting chrome header `#182235`.
- **Dark typography & hierarchy:**
  - Titles & Headings: Crisp pure white `#ffffff` / `#f8fafc`.
  - Body Text: Clean readable slate `#cbd5e1`.
  - System Annotations (`//`): Muted slate `#94a3b8` / `#64748b`.
  - Section Markers (`01.`, etc.): Luminous emerald `#34d399`.
- **Bio accents & pills:** Translucent emerald tints (`rgba(16, 185, 129, 0.12)`) paired with `#6ee7b7` text and `#34d399` borders, avoiding heavy opaque green blocks.
- **Browser chrome:** Provide separate light (`#f8fafc`) and dark (`#0b0f19`) `theme-color` metadata values so browser UI matches the active system preference.

The toggle retains its accessible name, `aria-pressed` state, visible focus ring, and light/dark icon state.

---

## 3. Typography Hierarchy & Font Stacks

The system employs a paired dual-font strategy:

1. **`font-sans` (`Inter`, `Plus Jakarta Sans`, system-ui)**: Clean, high-legibility geometric sans-serif for academic prose, headings, and long-form body content.
2. **`font-mono` (`JetBrains Mono`, `Fira Code`, monospace)**: High-precision code font for section indexes, metadata badges, timestamps, prompt lines, specimen identifiers, and technical parameters.

### 3.1 Type Scale Reference

| Level | Font / Tailwind Classes | Tracking / Leading | Example Usage |
| :--- | :--- | :--- | :--- |
| **Display H1** | `font-sans text-3xl sm:text-5xl font-bold text-lab-950` | `tracking-tight leading-tight` | Profile Hero Name, Article Main Title |
| **Section H2** | `font-sans text-xl sm:text-2xl font-bold text-lab-900` | `tracking-tight leading-snug` | Major Section Headings (`01. About`, etc.) |
| **Card / Item H3** | `font-sans text-base sm:text-lg font-bold text-lab-900` | `leading-snug` | Publication Title, Research Focus Title |
| **Subhead H4** | `font-mono text-xs font-bold uppercase text-lab-600` | `tracking-wider` | Section Sub-groups (`// Degrees & Education`) |
| **Section Index** | `font-mono text-sm font-bold text-bio-700` | `tracking-normal` | Section prefixes (`01.`, `02.`, `03.`) |
| **Body (Default)** | `font-sans text-sm sm:text-base text-lab-700` | `leading-relaxed` | Article paragraphs, narrative text |
| **Body (Compact)**| `font-sans text-xs sm:text-sm text-lab-700` | `leading-normal` | Card summaries, method descriptions |
| **Mono Metadata** | `font-mono text-xs text-lab-600` | `leading-normal` | Citations, locations, stats, timestamps |
| **Micro Tag** | `font-mono text-[10px] or text-[11px] font-semibold` | `uppercase tracking-wider` | Tech pills, organism names, badges |

---

## 4. Spacing, Layout Grids & Surfaces

### 4.1 Page Layout Grid

All standard pages should sit inside the canonical container:

```html
<div class="mx-auto max-w-6xl px-4 sm:px-6 py-10 space-y-16 sm:space-y-20">
  <!-- Page Sections -->
</div>
```

### 4.2 Background Treatments & Texture Catalog

The default body styling uses a **Clean Solid Canvas** (`bg-lab-50` / dark: `#0b0f19`) to keep the visual focus entirely on content, typography, and card hierarchy without distracting graph-paper lines.

For future design exploration or special dossier layouts, the following background alternatives are cataloged:

#### Active Standard: Clean Solid Canvas (Default)
- **Class:** `bg-lab-50` (light: `#f8fafc`, dark: `#0b0f19`).
- **Aesthetic:** Modern, minimalist, distraction-free.

#### Alternative A: Soft Ambient Bioluminescent Glow
- **Aesthetic:** High-end biotech / modern SaaS look with soft radial aura behind the hero.
- **Implementation:**
  ```css
  .bg-ambient-glow {
    background-image: radial-gradient(circle at 50% 0%, rgba(16, 185, 129, 0.05) 0%, transparent 60%);
  }
  .dark .bg-ambient-glow {
    background-image: radial-gradient(circle at 50% 0%, rgba(16, 185, 129, 0.08) 0%, transparent 65%);
  }
  ```

#### Alternative B: Wide-Spaced Modern Micro-Dots
- **Aesthetic:** Subtle developer canvas without looking like school notebook grid lines.
- **Implementation:**
  ```css
  .bg-dots-lab {
    background-size: 32px 32px;
    background-image: radial-gradient(rgba(148, 163, 184, 0.25) 1px, transparent 1px);
  }
  .dark .bg-dots-lab {
    background-image: radial-gradient(rgba(148, 163, 184, 0.12) 1px, transparent 1px);
  }
  ```

#### Alternative C: Subtle Micro-Noise / Film Grain
- **Aesthetic:** Tactile, stationery / matte paper quality.
- **Implementation:** SVG grain overlay with `opacity: 0.035` and CSS `mix-blend-mode: overlay`.

#### Alternative D: Engineering Graph Grid (Archived)
- **Class:** `.bg-grid-lab` (24px square grid overlay).
- **Implementation:**
  ```css
  .bg-grid-lab {
    background-size: 24px 24px;
    background-image: 
      linear-gradient(to right, rgba(226, 232, 240, 0.6) 1px, transparent 1px),
      linear-gradient(to bottom, rgba(226, 232, 240, 0.6) 1px, transparent 1px);
  }
  .dark .bg-grid-lab {
    background-image:
      linear-gradient(to right, rgba(51, 65, 85, 0.22) 1px, transparent 1px),
      linear-gradient(to bottom, rgba(51, 65, 85, 0.22) 1px, transparent 1px);
  }
  ```

### 4.3 Card Micro-Interactions (`.lab-card`)

Interactive cards (publications, research items, articles) use `.lab-card`:

```css
.lab-card {
  transition: all 0.2s cubic-bezier(0.16, 1, 0.3, 1);
}

@media (prefers-reduced-motion: no-preference) {
  .lab-card:hover {
    transform: translateY(-2px);
    box-shadow: 0 10px 25px -5px rgba(4, 120, 87, 0.08), 0 8px 10px -6px rgba(4, 120, 87, 0.04);
  }
}
```

---

## 5. UI Component Library & Code Patterns

Use these copy-pasteable HTML snippets when building new pages or features.

### 5.1 Section Header (Standard Laboratory Header)

```html
<section id="section-id" aria-labelledby="section-heading" class="scroll-mt-24 space-y-6">
  <div class="flex items-center justify-between border-b border-lab-200 pb-3">
    <div class="flex items-center gap-3">
      <span class="font-mono text-sm font-bold text-bio-700" aria-hidden="true">01.</span>
      <h2 id="section-heading" class="text-xl sm:text-2xl font-bold tracking-tight text-lab-900">
        Section Title
      </h2>
    </div>
    <span class="text-xs font-mono text-lab-500 font-medium hidden sm:inline">// SYSTEM_LABEL</span>
  </div>

  <!-- Content goes here -->
</section>
```

---

### 5.2 Terminal / CLI Code Box

```html
<div class="rounded-xl border border-lab-300/80 bg-white shadow-sm overflow-hidden" role="region" aria-label="Terminal Environment">
  <!-- Chrome Top Bar -->
  <div class="flex items-center justify-between border-b border-lab-200 bg-lab-100/70 px-4 py-2.5 text-xs font-mono">
    <div class="flex items-center gap-2">
      <span class="h-3 w-3 rounded-full bg-rose-400 inline-block" aria-hidden="true"></span>
      <span class="h-3 w-3 rounded-full bg-amber-400 inline-block" aria-hidden="true"></span>
      <span class="h-3 w-3 rounded-full bg-emerald-400 inline-block" aria-hidden="true"></span>
      <span class="ml-2 font-medium text-lab-700">terminal // script_name.sh</span>
    </div>
    <div class="text-lab-600 hidden sm:block">
      STATUS: <span class="text-bio-800 font-bold">200_OK</span>
    </div>
  </div>

  <!-- Terminal Body -->
  <div class="p-4 sm:p-5 bg-lab-900 text-lab-100 font-mono text-xs sm:text-sm overflow-x-auto">
    <div class="text-bio-400 font-semibold">
      user@lab:~$ run-pipeline --sample "At_col0_wt" --output "results/"
    </div>
    <div class="mt-2 text-lab-300 text-xs">
      [INFO] Transcriptome alignment complete (98.4% mapping efficiency).
    </div>
  </div>
</div>
```

---

### 5.3 Badges, Tags & Pill Tokens

#### Active Status Pill

```html
<div class="inline-flex items-center gap-2 rounded-full border border-bio-200 bg-bio-50/90 px-3 py-1 text-xs font-mono font-semibold text-bio-900">
  <span class="h-1.5 w-1.5 rounded-full bg-bio-600 motion-safe:animate-pulse" aria-hidden="true"></span>
  <span>Plant Molecular Biology & Functional Genomics</span>
</div>
```

#### Specimen / Code ID Badge

```html
<span class="font-mono text-[11px] font-bold text-bio-900 bg-bio-50 border border-bio-200 px-2 py-0.5 rounded">
  RES_01 // GENOMICS
</span>
```

#### Model Organism Tag (Italicized)

```html
<span class="inline-block rounded bg-lab-100 px-2 py-0.5 text-[11px] font-mono text-lab-800 italic border border-lab-200">
  Arabidopsis thaliana
</span>
```

#### Keyword / Hash Tag

```html
<span class="rounded bg-lab-100 px-2 py-0.5 text-[11px] font-mono text-lab-700 border border-lab-200">
  #CRISPR-Cas9
</span>
```

#### Publication Status Pills

```html
<!-- Published Status -->
<span class="rounded bg-emerald-100 text-emerald-900 border border-emerald-300 px-2 py-0.5 font-mono text-xs font-bold">
  ● Published
</span>

<!-- Preprint Status -->
<span class="rounded bg-amber-100 text-amber-900 border border-amber-300 px-2 py-0.5 font-mono text-xs font-bold">
  ⚡ Preprint
</span>
```

---

### 5.4 Specimen Portrait Frame (With Reticles)

```html
<div class="shrink-0 relative group mx-auto sm:mx-0">
  <div class="relative h-36 w-36 sm:h-44 sm:w-44 rounded-2xl overflow-hidden border border-lab-200/90 bg-lab-100/50 shadow-sm ring-1 ring-lab-300/60">
    <img 
      src="/assets/images/avatar-placeholder.svg" 
      alt="Scientist Portrait" 
      class="h-full w-full object-cover transition-transform duration-300 group-hover:scale-105"
      width="176"
      height="176"
    >
  </div>
  <!-- Decorative Tech Corner Reticles -->
  <span class="absolute -top-1 -left-1 h-3 w-3 border-t-2 border-l-2 border-bio-600" aria-hidden="true"></span>
  <span class="absolute -bottom-1 -right-1 h-3 w-3 border-b-2 border-r-2 border-bio-600" aria-hidden="true"></span>
</div>
```

---

### 5.5 Buttons, Action Links & Header Navigation

#### Primary Solid Button (Bio Emerald)

```html
<a href="/cv.pdf" class="inline-flex items-center gap-1.5 rounded-md bg-bio-800 px-2.5 py-1.5 sm:px-3.5 sm:py-1.5 text-xs font-mono font-medium text-white shadow-sm transition hover:bg-bio-700 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-bio-600 focus-visible:ring-offset-2">
  <svg class="h-3.5 w-3.5" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" aria-hidden="true">
    <path stroke-linecap="round" stroke-linejoin="round" d="M3 16.5v2.25A2.25 2.25 0 005.25 21h13.5A2.25 2.25 0 0021 18.75V16.5M16.5 12L12 16.5m0 0L7.5 12m4.5 4.5V3" />
  </svg>
  <span class="hidden sm:inline">Download Dossier.pdf</span>
  <span class="sm:hidden">CV</span>
</a>
```

#### Secondary / Link Out Button (Laboratory Surface)

```html
<a href="https://doi.org/..." target="_blank" rel="noopener noreferrer" class="flex-1 sm:flex-initial flex items-center justify-between rounded border border-lab-200 bg-lab-50 px-2.5 py-1.5 text-xs font-mono text-lab-800 hover:border-bio-500 hover:bg-bio-50 hover:text-bio-900 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-bio-600">
  <span class="flex items-center gap-2">
    <span>DOI link</span>
  </span>
  <span aria-hidden="true">↗</span>
  <span class="sr-only">(opens in a new tab)</span>
</a>
```

#### Mobile Navigation Menu & Toggle Pattern

```html
<!-- Mobile Menu Toggle Button (md:hidden) -->
<button type="button" data-mobile-menu-toggle aria-expanded="false" aria-controls="mobile-nav" class="md:hidden inline-flex items-center justify-center rounded-md border border-lab-200 bg-lab-50 p-1.5 text-lab-800 shadow-sm transition hover:border-bio-500 hover:bg-bio-50 hover:text-bio-900 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-bio-600" aria-label="Toggle navigation menu">
  <svg data-menu-icon="closed" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2" aria-hidden="true">
    <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
  </svg>
  <svg data-menu-icon="open" class="hidden h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2" aria-hidden="true">
    <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
  </svg>
</button>

<!-- Mobile Navigation Drawer -->
<div id="mobile-nav" data-mobile-menu class="hidden md:hidden border-t border-lab-200/70 bg-white/95 px-4 py-3 space-y-1 shadow-sm">
  <div class="text-[10px] font-mono font-bold uppercase tracking-wider text-lab-500 px-3 py-1">// Navigation Menu</div>
  <a href="/" class="flex items-center gap-2.5 px-3 py-2 font-mono text-xs font-medium text-lab-700 hover:text-lab-950 hover:underline hover:underline-offset-4 hover:decoration-2 hover:decoration-bio-600 transition-colors">
    <span class="text-bio-700 font-bold" aria-hidden="true">01.</span> Home
  </a>
  <a href="/about/" class="flex items-center gap-2.5 px-3 py-2 font-mono text-xs font-medium text-lab-700 hover:text-lab-950 hover:underline hover:underline-offset-4 hover:decoration-2 hover:decoration-bio-600 transition-colors">
    <span class="text-bio-700 font-bold" aria-hidden="true">02.</span> About
  </a>
  <a href="/gallery/" class="flex items-center gap-2.5 px-3 py-2 font-mono text-xs font-medium text-lab-700 hover:text-lab-950 hover:underline hover:underline-offset-4 hover:decoration-2 hover:decoration-bio-600 transition-colors">
    <span class="text-bio-700 font-bold" aria-hidden="true">03.</span> Gallery
  </a>
</div>
```

---

### 5.6 Publication / Article Card Pattern

```html
<article class="lab-card rounded-xl border border-lab-200 bg-white p-5 sm:p-6 shadow-sm hover:border-bio-400" aria-labelledby="pub-title-1">
  <div class="flex flex-col sm:flex-row sm:items-start sm:justify-between gap-3">
    
    <div class="space-y-2 flex-1">
      <div class="flex flex-wrap items-center gap-2 text-xs font-mono">
        <span class="rounded bg-emerald-100 text-emerald-900 border border-emerald-300 px-2 py-0.5 font-bold">
          ● Published
        </span>
        <span class="text-lab-700 font-bold">The Plant Journal (2025)</span>
        <span class="text-lab-400" aria-hidden="true">•</span>
        <span class="text-lab-600">Research Article</span>
      </div>

      <h3 id="pub-title-1" class="text-base sm:text-lg font-bold text-lab-900 leading-snug">
        Multiplex CRISPR/Cas9 editing reveals regulatory checkpoints in Arabidopsis stress acclimation
      </h3>

      <p class="text-xs sm:text-sm font-mono text-lab-700">
        <strong class="text-lab-900">Valeria, B.</strong>, Chen, L., & Ramirez, M.
      </p>

      <p class="text-xs sm:text-sm text-lab-700 pt-1 leading-relaxed">
        <span class="font-bold text-lab-900">Abstract snippet:</span> Targeted mutagenesis across three stress-responsive loci revealed unexpected functional redundancy in transcription factor cascades...
      </p>

      <div class="flex flex-wrap gap-1.5 pt-2">
        <span class="rounded bg-lab-100 px-2 py-0.5 text-[11px] font-mono text-lab-700 border border-lab-200">#CRISPR</span>
        <span class="rounded bg-lab-100 px-2 py-0.5 text-[11px] font-mono text-lab-700 border border-lab-200">#Arabidopsis</span>
      </div>
    </div>

    <!-- Actions Column -->
    <div class="flex flex-wrap sm:flex-col gap-2 pt-3 sm:pt-0 border-t sm:border-t-0 border-lab-100 sm:w-36 text-xs font-mono shrink-0">
      <a href="#" target="_blank" rel="noopener noreferrer" class="flex-1 sm:flex-initial flex items-center justify-between rounded border border-lab-200 bg-lab-50 px-2.5 py-1.5 text-lab-800 hover:border-bio-500 hover:bg-bio-50">
        <span>DOI Link</span>
        <span aria-hidden="true">↗</span>
        <span class="sr-only">(opens in a new tab)</span>
      </a>
      <a href="#" class="flex-1 sm:flex-initial flex items-center justify-between rounded bg-bio-800 px-2.5 py-1.5 text-white hover:bg-bio-700">
        <span>PDF Copy</span>
        <span aria-hidden="true">↓</span>
      </a>
    </div>

  </div>
</article>
```
```

---

### 5.7 Vertical Milestone Timeline

```html
<div class="relative border-l-2 border-bio-200 pl-6 space-y-8 ml-2">
  <div class="relative group">
    <!-- Timeline node dot -->
    <span class="absolute -left-[31px] top-1 h-3.5 w-3.5 rounded-full border-2 border-bio-600 bg-white" aria-hidden="true"></span>

    <div class="space-y-1">
      <div class="flex flex-wrap items-center gap-2">
        <span class="font-mono text-xs font-bold text-bio-900 bg-bio-50 border border-bio-200 px-2 py-0.5 rounded">
          2024 — Present
        </span>
        <span class="text-xs font-mono font-medium text-lab-600">
          Doctoral Studies
        </span>
      </div>

      <h4 class="text-base font-bold text-lab-900 pt-1">
        PhD in Biological Sciences (Plant Molecular Biology)
      </h4>

      <div class="text-xs font-medium text-lab-700">
        Department of Plant Molecular Biology • <span class="text-lab-600 font-mono">Mexico City</span>
      </div>

      <p class="text-xs sm:text-sm text-lab-700 pt-1 leading-relaxed">
        Research focus: Genome editing and epigenetic control of stress adaptation.
      </p>
    </div>
  </div>
</div>
```

---

### 5.8 Page and Footer Layout

- The home page is limited to the hero and Recent Publications; extended profile material lives on `/about/`.
- On `/about/`, Research Interest, Toolkit, and Education are compact native `<details>` panels sharing `name="about-sections"` so only one can be open at once. Prefer this native behavior over JavaScript.
- The top navigation bar adapts to mobile viewports using a collapsible mobile menu drawer (`#mobile-nav` with `[data-mobile-menu-toggle]`), compact action buttons, and responsive text badges.
- The footer uses a three-column grid at desktop sizes (profile spanning two columns, Academic Links occupying the third) and cleanly stacks with centered text alignment at mobile viewports.

---

## 6. Article & New Page Template Guidelines

When adding new standalone articles, laboratory notes, or subpages (e.g., `_posts/` or `research/`), use the following layout and typography rules.

### 6.1 Article Front Matter Template

```yaml
---
layout: default
title: "Mapping Gene Regulatory Networks via Multiplex CRISPR"
description: "A comprehensive laboratory protocol and computational pipeline for plant functional genomics."
date: 2026-08-20
author: "Brigitte Valeria"
tags:
  - Transcriptomics
  - RNA-seq
  - Protocol
---
```

### 6.2 Article HTML Structure Blueprint

```html
<article class="mx-auto max-w-4xl px-4 sm:px-6 py-10 space-y-10">

  <!-- Breadcrumb / Return Nav -->
  <nav aria-label="Breadcrumb" class="text-xs font-mono text-lab-600 flex items-center gap-2">
    <a href="{{ '/' | relative_url }}" class="hover:text-bio-800 underline underline-offset-2">Home</a>
    <span aria-hidden="true">/</span>
    <span class="text-lab-800 font-medium">Articles</span>
  </nav>

  <!-- Article Header Spec Sheet -->
  <header class="rounded-2xl border border-lab-200 bg-white p-6 sm:p-8 space-y-4 shadow-sm">
    <div class="flex flex-wrap items-center gap-2">
      <span class="rounded bg-bio-50 px-2.5 py-0.5 text-xs font-mono font-semibold text-bio-900 border border-bio-200">
        LAB_NOTE // GENOMICS
      </span>
      <span class="text-xs font-mono text-lab-500">Published: August 20, 2026</span>
    </div>

    <h1 class="text-2xl sm:text-4xl font-bold tracking-tight text-lab-950 font-sans">
      Mapping Gene Regulatory Networks via Multiplex CRISPR
    </h1>

    <p class="text-base text-lab-700 leading-relaxed font-sans">
      A step-by-step walkthrough detailing sgRNA vector design, protoplast transfection efficiency, and subsequent differential expression analysis in DESeq2.
    </p>

    <div class="pt-2 flex flex-wrap items-center gap-2 text-xs font-mono text-lab-600 border-t border-lab-100">
      <span>Author: <strong class="text-lab-900">Brigitte Valeria</strong></span>
      <span aria-hidden="true">•</span>
      <span>Model: <em class="text-lab-800">Arabidopsis thaliana</em></span>
    </div>
  </header>

  <!-- Article Prose Content -->
  <div class="rounded-2xl border border-lab-200 bg-white p-6 sm:p-10 shadow-sm space-y-6 text-lab-800 leading-relaxed font-sans text-sm sm:text-base">
    
    <h2 class="text-xl font-bold text-lab-950 pt-2 border-b border-lab-100 pb-2">
      1. Introduction & Biological Premise
    </h2>
    <p>
      Understanding transcriptional cascades requires perturbation of redundant paralogs simultaneously...
    </p>

    <!-- Callout / Lab Note Block -->
    <div class="rounded-lg border-l-4 border-bio-600 bg-bio-50/60 p-4 space-y-1">
      <div class="font-mono text-xs font-bold text-bio-950 uppercase tracking-wide">
        // Experimental Parameter Note
      </div>
      <p class="text-xs sm:text-sm text-bio-900">
        Ensure protoplasts are maintained at 22°C in W5 buffer during the 16-hour post-transfection incubation period.
      </p>
    </div>

    <h2 class="text-xl font-bold text-lab-950 pt-2 border-b border-lab-100 pb-2">
      2. Computational Pipeline Execution
    </h2>
    <p>
      The following Bash pipeline was deployed on our HPC cluster for automated read trimming and STAR alignment:
    </p>

    <!-- Code Block with Lab Chrome -->
    <div class="rounded-xl border border-lab-300 bg-lab-900 text-lab-100 font-mono text-xs overflow-hidden">
      <div class="bg-lab-950 px-4 py-2 border-b border-lab-800 text-lab-400 flex items-center justify-between text-[11px]">
        <span>pipeline.nf</span>
        <span>Nextflow DSL2</span>
      </div>
      <pre class="p-4 overflow-x-auto leading-relaxed"><code>process ALIGN_READS {
    tag "$sample_id"
    publishDir "results/alignments", mode: 'copy'

    input:
    tuple val(sample_id), path(reads)

    output:
    tuple val(sample_id), path("*.bam"), emit: bam

    script:
    """
    STAR --genomeDir /ref/arabidopsis/ --readFilesIn ${reads[0]} ${reads[1]} --outSAMtype BAM SortedByCoordinate
    """
}</code></pre>
    </div>

  </div>

  <!-- Article Colophon / Citation Box -->
  <footer class="rounded-xl border border-lab-200 bg-lab-50 p-6 space-y-3 font-mono text-xs text-lab-700">
    <div class="font-bold text-lab-900 uppercase">// Suggested Citation</div>
    <div class="bg-white p-3 rounded border border-lab-200 select-all text-[11px] text-lab-800">
      Valeria, B. (2026). Mapping Gene Regulatory Networks via Multiplex CRISPR. Brigitte Valeria Academic Portfolio. https://brigittevaleria.dev/
    </div>
  </footer>

</article>
```

---

## 7. Accessibility (a11y) & SEO Requirements

All pages and components must follow these strict accessibility mandates:

### 7.1 Accessibility Rules

1. **Keyboard Skip Link**: Must include `<a href="#main-content" ...>Skip to main content</a>` as the first interactable element in `_layouts/default.html`.
2. **External Link Safety**: Every external link (`target="_blank"`) MUST include:
   - `rel="noopener noreferrer"`
   - Visually hidden screen-reader text: `<span class="sr-only">(opens in a new tab)</span>`.
3. **Decorative Icons & SVGs**: Any emoji or decorative SVG must have `aria-hidden="true"`, or if conveying critical meaning, explicit `role="img"` and `aria-label="Description"`.
4. **Focus Rings**: Never remove `:focus` outlines without replacing them. Interactive elements must use `focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-bio-600 focus-visible:ring-offset-2`.
5. **Heading Level Integrity**: Maintain logical heading hierarchy (`h1` → `h2` → `h3` → `h4`). Never skip levels for aesthetic sizing (use Tailwind font-size classes instead).
6. **Motion Sensitivity**: Animations (such as pulsing status dots) must be wrapped with `motion-safe:animate-pulse`, and transitions must be neutralized under `@media (prefers-reduced-motion: reduce)`.

### 7.2 Academic SEO & Structured Data

1. **SEO Metadata Tag**: Managed exclusively via `{% seo %}` plugin in `_layouts/default.html`. Do not hardcode `<title>` or `<meta name="description">` tags in templates.
2. **Google Scholar Metadata**: Include `<meta name="citation_author">` and `<meta name="citation_institution">` in layouts.
3. **JSON-LD Schema**: Ensure `Person` and `ScholarlyArticle` structured data schemas are updated when affiliations or publications change.

---

## 8. Summary Checklist for New Pages

Before publishing any new page or article, verify:

- [ ] **Data Decoupling**: If modifying core profile/publication data, update `_data/*.yml` instead of hardcoding text into HTML templates.
- [ ] **Font Hierarchy**: Headings use `font-sans font-bold`, while code IDs, badges, indexes, and dates use `font-mono`.
- [ ] **Color Contrast**: Text on light cards uses `text-lab-900` or `text-lab-700`; badges use appropriate text/bg color pairs (e.g. `bg-bio-50 text-bio-900`).
- [ ] **Accessible Links**: All external links have `rel="noopener noreferrer"` and `(opens in a new tab)` screen reader spans.
- [ ] **Interactive Hover**: Cards have `.lab-card` and `hover:border-bio-400`.
- [ ] **Build Verification**: Run `bundle exec jekyll build` to ensure zero compilation or syntax errors.
