# Data Model: Blog Site Structure & Pages

**Feature**: `001-blog-site-structure`
**Date**: 2026-03-30

---

## Post (Jekyll Front-Matter Schema)

All files in `_posts/` use this schema. Research sessions are posts with `research-session` in tags.

```yaml
---
layout: post           # Required. Always "post"
title: ""              # Required. String. Used in <title>, headings, feeds
date: YYYY-MM-DD       # Required. Publication date
tags: []               # Required. Array. Must include one lang-* tag.
                       #   Common tags: sdd, spec-kit, research-session,
                       #               lang-es, lang-en, lang-bilingual
lang: ""               # Required. One of: es | en | bilingual
featured: false        # Optional. Boolean. Exactly one post should have true.
                       #   Defaults to false if omitted.
excerpt: ""            # Optional. Manual excerpt shown on landing/listings.
                       #   If omitted, Jekyll auto-generates from first paragraph.
---
```

**Validation rules**:
- `lang` must be one of `es`, `en`, `bilingual`
- `tags` must contain the matching `lang-*` tag (`lang-es`, `lang-en`, or `lang-bilingual`)
- `featured: true` should appear on exactly one post at any time
- Bilingual posts: Spanish section first, English section after a `---` divider

---

## Figure Include Parameters

Used via `{% include figure.html ... %}` in post/page body content.

| Parameter | Required | Type | Description |
|-----------|----------|------|-------------|
| `src` | Yes | String | Path to image file (relative to site root or absolute URL) |
| `alt` | Yes | String | Alt text for accessibility |
| `caption` | No | String | Visible caption text below image |
| `source_name` | No | String | Attribution: name of original author or publication |
| `source_url` | No | String | Attribution: URL to original source |

**Fallback behavior**:
- If `caption` is absent: no caption rendered
- If `source_name` is absent but `source_url` is present: renders URL as attribution
- If both `source_name` and `source_url` are absent: renders "Source unknown"
- If `source_name` is present but `source_url` is absent: renders name as plain text (no link)

---

## FAQ Entry Schema

FAQ entries are defined directly in `faq.md` front-matter as a YAML array, rendered via Liquid loop.

```yaml
---
layout: page
title: FAQ
faqs:
  - question: "What is spec-driven development?"
    answer: "SDD is a workflow where every feature begins with a written specification..."
  - question: "What is spec-kit?"
    answer: "spec-kit is a scaffolding tool by GitHub that sets up the SDD workflow..."
---
```

| Field | Required | Type | Description |
|-------|----------|------|-------------|
| `question` | Yes | String | Short, scannable question (< 100 chars recommended) |
| `answer` | Yes | String | Concise answer, 1–3 sentences |

---

## Page Front-Matter Schema

Used by `about.md`, `faq.md`, `research-sessions.md`, `404.md`.

```yaml
---
layout: page           # Required. Always "page"
title: ""              # Required. Used in <title> and page heading
permalink: /path/      # Optional. Overrides default URL slug.
lang: en               # Optional. Defaults to "en" for static pages.
---
```

---

## Site Configuration (`_config.yml`) Key Fields

```yaml
title: "Learning SDD"
description: "A blog documenting the process of learning spec-driven development with Claude Code"
baseurl: "/blog"
url: "https://ollerenac.github.io"
lang: en

theme: minima

# Exclude spec-kit and project management files from Jekyll build
exclude:
  - .specify/
  - .claude/
  - specs/
  - docs/
  - Gemfile
  - Gemfile.lock
  - README.md
  - CLAUDE.md

# Syntax highlighting
highlighter: rouge
markdown: kramdown
kramdown:
  syntax_highlighter: rouge

# Pagination (future — not in scope for this spec)
# plugins:
#   - jekyll-paginate
```
