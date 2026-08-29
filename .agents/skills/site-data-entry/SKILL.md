---
name: site-data-entry
description: "Add or update information in this Jekyll site's data objects through a short user interview. Use this skill whenever the user wants to add a publication, research interest, education milestone, talk, poster, workshop, toolkit skill, profile detail, biography text, academic link, or other portfolio information, even when they do not name the _data file. Inspect the existing schema, ask for missing facts, show the proposed YAML object, write it to the correct _data/*.yml file after confirmation, and validate the result."
---

# Site Data Entry

Use this skill to turn user-provided academic information into valid, site-compatible YAML.
The site keeps reusable content in `_data/`, so update those files instead of hardcoding content in templates.

## Workflow

1. Inspect the relevant `_data/*.yml` file and `README.md` before editing.
2. Identify whether the request is an append, an update, or a replacement.
3. Interview the user for missing information.
4. Normalize the answers into the existing schema and style.
5. Show the complete proposed object or changed mapping and ask for confirmation before writing.
6. Edit only the relevant data file.
7. Validate YAML and run `bundle exec jekyll build`.
8. Report the file changed, the object added or updated, and validation results.

Do not invent names, dates, URLs, authors, institutions, results, or other academic facts.
If a value is unknown, ask whether the user wants to omit it or leave it empty.
Do not add optional empty keys unless they help preserve the established structure.
Keep the current ordering unless the user asks for another order.
Preserve the site's existing quoting, indentation, list style, and field names when practical.

### Interview behavior

Start with a short classification question only when the target data object is unclear.
Then ask only for fields that are missing from the request.
Ask questions in small groups, with no more than four concise questions in one message.
Use plain language and explain why a field is needed when it may not be obvious.

For an update, first locate the matching record using a stable field such as `id`, title, DOI, degree, or event.
Show the current values that will change and ask the user to confirm ambiguous matches.
Do not silently replace a similar record or create a duplicate.

For links, ask whether each URL is a public page, PDF, code repository, or another resource.
Use the existing URL field instead of creating a new field.
For publications, ask for a DOI when available, but do not require one for a preprint or other record.

If the user provides all required facts in the first message, still show the normalized YAML preview before editing.
If the user has already clearly authorized the write and no facts are missing, confirmation can be brief: state the object and proceed after the preview.

## Data object selection

Use these mappings for the current site:

| User wants to add | File | Shape |
| --- | --- | --- |
| Name, title, affiliation, biography, disciplines, topics, or contact link | `_data/profile.yml` | One mapping |
| Research focus or project | `_data/research.yml` | List of mappings |
| Article, preprint, or publication | `_data/publications.yml` | List of mappings |
| Wet-lab or dry-lab ability | `_data/toolkit.yml` | Mapping with nested categories and groups |
| Degree, education, award, or academic milestone | `_data/timeline.yml` | List of mappings |
| Talk, poster, workshop, or presentation | `_data/talks.yml` | List of mappings |

Do not create a new data file for one record when an existing file matches the content.
If the request needs a new content type, explain that a template change may also be required and ask before creating it.

## Schemas and interview fields

Use only fields supported by the current template unless the user asks for a coordinated template change.
Optional fields may be omitted or set to an empty value.

### Profile: `_data/profile.yml`

This is a single mapping.
Ask only for the fields relevant to the requested change.

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
photo: "/assets/images/profile.jpg"
photo_alt: "Descriptive portrait alt text"
terminal_prompt: "Terminal-style research summary"
about_paragraphs:
  - "Biography paragraph"
core_disciplines:
  - "Discipline"
knows_about:
  - "Research topic"
contact:
  orcid: "0000-0000-0000-0000"
  orcid_url: "https://orcid.org/..."
  scholar_url: "https://scholar.google.com/..."
  github_url: "https://github.com/..."
  researchgate_url: "https://www.researchgate.net/..."
  cv_url: "/assets/files/cv.pdf"
```

When adding a profile list item, such as a discipline or topic, append it to the existing list.
When changing a scalar value, update only that key.
If `photo` is present, require a meaningful `photo_alt`.

### Research: `_data/research.yml`

Required interview fields are `id`, `title`, `topic`, `description`, and at least one research context field such as `model_organisms` or `keywords`.
Ask for `icon` only if the user wants to choose it.

```yaml
- id: "unique-slug"
  title: "Research focus title"
  icon: "Short icon"
  topic: "Short category or topic badge"
  description: "Paragraph describing research aims, approach, and findings."
  highlight: "Short takeaway or emphasis statement"
  model_organisms:
    - "Organism"
  keywords:
    - "Method or keyword"
```

Make `id` lowercase, short, and hyphen-separated.
Check that it is unique before appending.
Use a flat paragraph for `description`, not a new nested structure.

### Publication: `_data/publications.yml`

Ask for `title`, `authors`, `journal`, `year`, `status`, and `type`.
Ask for `doi` and `doi_url` when available.
Ask for `pdf_url`, `code_url`, and `tags` only when relevant.

```yaml
- title: "Publication title"
  authors: "Author One; Author Two"
  journal: "Journal name"
  year: "2026"
  status: "Published"
  type: "Peer-Reviewed Article"
  doi: "10.xxxx/example"
  doi_url: "https://doi.org/..."
  pdf_url: "/assets/files/publication.pdf"
  code_url: "https://github.com/..."
  tags:
    - "keyword"
```

Keep `year` as a quoted string to match the current data.
Keep multiple authors in the existing semicolon-separated string format.
Use `status` values that match the site's display logic, such as `Published` or `Preprint`.
Do not add `abstract` unless the template has been checked and the user requests support for it.
Check DOI and title before creating a new record to avoid duplicates.

### Toolkit skill: `_data/toolkit.yml`

Toolkit data is grouped, so first determine the category and group.
Use an existing category when possible.
Only create a new category or group after asking the user and confirming its label, ID, icon, and description.

```yaml
categories:
  - id: "wet_lab"
    name: "Wet Lab // Molecular Biology"
    badge: "BENCH_WORK"
    icon: "Short icon"
    description: "Category summary"
    groups:
      - title: "Skill group"
        skills:
          - name: "Skill"
```

For a normal new skill, add one item under the selected existing group's `skills` list:

```yaml
- name: "Skill name"
```

Do not add skill levels unless the template and current data support them.

### Timeline milestone: `_data/timeline.yml`

Ask for `type`, `degree`, `institution`, and `location`.
Ask for `advisor`, `highlight`, and `badge` when applicable.

```yaml
- type: "education"
  degree: "Degree name"
  institution: "Institution name"
  location: "City, country"
  advisor: "Advisor name"
  highlight: "Achievement or focus"
  badge: "In Progress"
```

Use `type: "education"` for degrees unless the user identifies another supported milestone type.
Do not infer dates or periods because the current timeline template does not define them.

### Talk, poster, or workshop: `_data/talks.yml`

Ask for `type`, `title`, `event`, and `year`.
Ask for `location` and `tags` when available.

```yaml
- type: "Poster"
  title: "Presentation title"
  event: "Conference or event"
  year: "2026"
  location: "City, country"
  tags:
    - "topic"
```

Keep `year` as a quoted string.
If `_data/talks.yml` is empty, explain that adding the first item will make the Selected Talks & Posters section appear.

## YAML and site safety

Before editing, inspect the surrounding records so the new object uses the correct local style.
Use a targeted edit and do not rewrite unrelated data.
Do not edit `_site/`, `.jekyll-cache/`, `.sass-cache/`, or other generated files.
Do not change templates, CSS, configuration, or assets unless the user asks for a feature that the current data schema cannot represent.

Validate the edited file with Ruby's YAML parser, then run:

```sh
bundle exec jekyll build
```

If validation fails, fix the source YAML and rerun the check.
If the build fails, report the source error and do not edit generated output.
Review the final diff for accidental changes and confirm that no duplicate record was added.
