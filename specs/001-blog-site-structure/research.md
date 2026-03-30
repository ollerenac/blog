# Research: Blog Site Structure & Pages

**Feature**: `001-blog-site-structure`
**Date**: 2026-03-30

---

## Dark Theme on Jekyll / Minima

**Decision**: Override minima's CSS custom properties + add custom SCSS partials. Do not fork the theme.

**Rationale**: Minima 3.x exposes CSS custom properties (`--minima-*`) that can be overridden in a custom `assets/css/main.scss`. This avoids copying and maintaining the full theme source while still allowing complete visual control. Adding SCSS partials under `_sass/` is the Jekyll-standard extension point.

**Alternatives considered**:
- Forking minima entirely — rejected, creates maintenance burden for a blog that needs to stay simple.
- Using a third-party dark theme — rejected, violates Static & Simple principle (unknown plugin compatibility, extra dependency).
- Inline styles — rejected, unmaintainable at scale.

---

## Syntax Highlighting

**Decision**: Use Rouge (built into Jekyll) with custom SCSS overrides that replace the default light Monokai colors with a dark-optimized palette.

**Rationale**: Rouge ships with Jekyll and GitHub Pages — zero additional dependencies. The `.highlight` CSS class wraps all fenced code blocks. Overriding these styles in `_sass/_syntax.scss` gives full color control without any JavaScript syntax highlighter library.

**Key colors for dark palette**:
- Background: `#141414` (slightly lighter than page bg for depth)
- Comments: `#555555`
- Keywords: `#c792ea` (soft purple)
- Strings: `#c3e88d` (soft green)
- Numbers/constants: `#f78c6c` (soft orange)
- Functions: `#82aaff` (soft blue)

**Alternatives considered**:
- Prism.js — rejected, requires JavaScript, violates minimal-JS constraint.
- highlight.js — same reason.

---

## Featured Post Designation

**Decision**: Add `featured: true` to one post's front-matter. Landing page uses Liquid: `{% assign featured = site.posts | where: "featured", true | first %}`.

**Rationale**: Simplest possible approach — no plugin, no database, no config file. The `where` filter is available in Jekyll's standard Liquid. If no post has `featured: true`, the landing page gracefully falls back to the most recent post.

**Fallback**: `{% assign featured = featured | default: site.posts.first %}`

---

## Research Sessions Page

**Decision**: Tag-based filtering. Posts tagged `research-session` appear on the Research Sessions page. Liquid: `{% assign sessions = site.posts | where_exp: "p", "p.tags contains 'research-session'" %}`.

**Rationale**: Reuses the existing `_posts/` collection with no new Jekyll collections or plugins. Simple, constitution-compliant.

**Alternatives considered**:
- Separate `_sessions/` Jekyll collection — rejected (chosen option B in spec clarification).
- Category-based filtering — tags are more flexible and already required by the constitution's bilingual convention.

---

## Figure with Attribution

**Decision**: Custom `_includes/figure.html` partial with parameters: `src`, `alt`, `caption`, `source_name`, `source_url`.

**Usage in posts**:
```liquid
{% include figure.html
   src="/assets/images/example.png"
   alt="Description of image"
   caption="Figure 1: What this shows"
   source_name="Author Name"
   source_url="https://example.com/original-post" %}
```

**Rendered output**: `<figure>` element with `<img>`, `<figcaption>` containing caption text and a linked attribution credit.

**Fallback**: If `source_name` is absent, renders "Source unknown" rather than a blank attribution field.

---

## Bilingual Post Format

**Decision**: Single file per post. `lang: bilingual` in front-matter. Spanish content first, then a `---` Markdown horizontal rule, then English content.

**Rationale**: Matches the constitution exactly. No plugin needed. The `lang` tag (`lang-es`, `lang-en`, or `lang-bilingual`) enables tag-based filtering from the tags page (future spec).

**Example front-matter**:
```yaml
---
layout: post
title: "Qué es SDD / What is SDD"
date: 2026-03-30
tags: [sdd, spec-kit, lang-bilingual, research-session]
lang: bilingual
featured: false
---
```

---

## GitHub Pages Compatibility

**Decision**: Use a `Gemfile` that pins the `github-pages` gem, which bundles a compatible Jekyll version and approved plugins.

**Rationale**: The `github-pages` gem ensures the local build exactly matches what GitHub Pages will build. Avoids deployment surprises from version mismatches.

**Key constraint**: The `github-pages` gem pins Jekyll to a specific version (currently ~3.9.x for the legacy gem). To use Jekyll 4.x with GitHub Pages, the GitHub Actions deployment approach (already chosen in the constitution) allows using any Jekyll version — the Actions workflow builds locally and pushes the output, bypassing GitHub Pages' own build system.

**Resolution**: Use Jekyll 4.x in the Gemfile directly (not the `github-pages` gem). The GitHub Actions workflow handles building and deploying. This is already the chosen deployment method per the constitution.

---

## All NEEDS CLARIFICATION Items: Resolved

All unknowns from the spec have been resolved above. No blockers for Phase 1.
