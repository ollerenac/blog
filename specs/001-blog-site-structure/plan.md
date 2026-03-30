# Implementation Plan: Blog Site Structure & Pages

**Branch**: `001-blog-site-structure` | **Date**: 2026-03-30 | **Spec**: [spec.md](./spec.md)
**Input**: Feature specification from `/specs/001-blog-site-structure/spec.md`

---

## Summary

Build a complete Jekyll static blog with five pages (landing, research sessions, about, FAQ, 404), a dark minimal design system, and a rich content model supporting syntax-highlighted code blocks, attributed figures, and quoted README excerpts. All content is mocked. The site is bilingual (Spanish/English) per the constitution, deployed via GitHub Actions to GitHub Pages.

---

## Technical Context

**Language/Version**: Ruby (Jekyll 4.x), HTML5, CSS3, Markdown (Kramdown)
**Primary Dependencies**: `jekyll` (4.x), `minima` theme (overridden), `rouge` (syntax highlighting, bundled with Jekyll), `webrick` (local dev server)
**Storage**: N/A — static files only
**Testing**: Manual visual testing + `jekyll build --dry-run` for build validation; Lighthouse for performance/accessibility spot-checks
**Target Platform**: GitHub Pages (static file hosting), all modern browsers, mobile-first responsive
**Project Type**: Static site / personal blog
**Performance Goals**: Lighthouse performance score ≥ 90; pages load in < 2s on a standard connection
**Constraints**: GitHub Pages compatible (no unsupported plugins), no server-side runtime, JavaScript kept to an absolute minimum, all dependencies must be GitHub Pages-safe gems
**Scale/Scope**: < 20 mocked posts/sessions at launch; single author; no user accounts

---

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Status | Notes |
|-----------|--------|-------|
| I. Content-First | ✅ PASS | Every page and component directly serves content creation or reading. No features added speculatively. |
| II. Static & Simple | ✅ PASS | Jekyll + minima override + custom CSS only. No server runtime. No unsupported plugins. YAGNI applied strictly — custom CSS replaces theme styling, no additional JS frameworks. |
| III. Spec-Driven Development | ✅ PASS | Full spec completed and approved before this plan. |
| IV. Bilingual by Convention | ✅ PASS | `lang` front-matter field required on all posts. Bilingual posts: Spanish first, English after `---` divider. Language tags (`lang-es`, `lang-en`) on every post. |
| V. Open & Transparent | ✅ PASS | Giscus comments are deferred to a separate spec (out of scope here, not removed). Conversation log is maintained. |

**Constitution Check: PASSED — proceed to Phase 0.**

---

## Project Structure

### Documentation (this feature)

```text
specs/001-blog-site-structure/
├── plan.md              # This file
├── research.md          # Phase 0 output
├── data-model.md        # Phase 1 output
├── quickstart.md        # Phase 1 output
├── contracts/           # Phase 1 output
│   ├── post-frontmatter.md
│   └── figure-include.md
└── tasks.md             # Phase 2 output (via /speckit.tasks)
```

### Source Code (repository root)

```text
/
├── _posts/                        # All blog posts and research sessions
│   ├── 2026-03-30-welcome.md      # Featured post (mocked)
│   ├── 2026-03-28-session-01.md   # Research session (mocked)
│   └── 2026-03-25-session-02.md   # Research session (mocked)
├── _layouts/
│   ├── default.html               # Base layout (dark theme shell)
│   ├── post.html                  # Post layout (extends default)
│   └── page.html                  # Static page layout (extends default)
├── _includes/
│   ├── header.html                # Site nav
│   ├── footer.html                # Minimal footer
│   └── figure.html                # Captioned figure with attribution
├── _sass/
│   ├── _variables.scss            # Color palette, typography tokens
│   ├── _base.scss                 # Reset + base dark styles
│   ├── _layout.scss               # Page/post layout
│   ├── _syntax.scss               # Code block / syntax highlighting overrides
│   └── _components.scss           # Figure, blockquote, FAQ, nav
├── assets/
│   └── css/
│       └── main.scss              # Entry point (imports all partials)
├── research-sessions.md           # Research Sessions page
├── about.md                       # About page
├── faq.md                         # FAQ page
├── 404.md                         # Custom 404 page
├── index.md                       # Landing page
├── _config.yml                    # Jekyll config
├── Gemfile                        # Ruby dependencies
└── .github/
    └── workflows/
        └── deploy.yml             # GitHub Actions deployment
```

**Structure Decision**: Single Jekyll project at repo root. No src/ subdirectory — Jekyll convention places content files at root level. Spec-kit artifacts (`.specify/`, `specs/`, `docs/`) coexist at root and are excluded from Jekyll build via `_config.yml` `exclude:` list.

---

## Complexity Tracking

No constitution violations. No complexity justification required.

---

## Phase 0: Research

*See [research.md](./research.md) for full findings.*

**Resolved decisions:**

| Decision | Resolution |
|----------|------------|
| Dark theme approach | Override minima CSS variables + custom SCSS partials. No theme fork required. |
| Syntax highlighting | Rouge (built into Jekyll). Custom SCSS overrides default highlighting colors to match dark palette. |
| Figure with attribution | Custom `_includes/figure.html` partial. Called with Liquid include tags in post content. |
| Featured post designation | `featured: true` front-matter flag on one post. Landing page uses Liquid `where` filter to find it. |
| Research sessions filtering | Tag-based: posts tagged `research-session` surfaced on the Research Sessions page via Liquid tag filter. |
| Bilingual post format | `lang: bilingual` front-matter + `---` horizontal rule divider between Spanish and English sections. |
| GitHub Pages gem compatibility | Use `github-pages` gem bundle OR explicit safe gems list in Gemfile. Jekyll 4 is supported. |

---

## Phase 1: Design & Contracts

*See [data-model.md](./data-model.md), [contracts/](./contracts/), and [quickstart.md](./quickstart.md).*

### Design System: Dark Minimal

| Token | Value | Usage |
|-------|-------|-------|
| `--bg` | `#0d0d0d` | Page background |
| `--surface` | `#1a1a1a` | Cards, code blocks |
| `--border` | `#2a2a2a` | Dividers, borders |
| `--text-primary` | `#e8e8e8` | Body text |
| `--text-secondary` | `#888888` | Metadata, captions |
| `--accent` | `#7c6af7` | Links, highlights (muted purple) |
| `--code-bg` | `#141414` | Inline code background |
| `--font-body` | `'Inter', system-ui, sans-serif` | Prose |
| `--font-mono` | `'JetBrains Mono', 'Fira Code', monospace` | Code, metadata |

### Implementation Phases

**Phase A — Foundation** (must complete before anything else)
1. `Gemfile` + `_config.yml` with correct baseurl, excludes, and theme
2. GitHub Actions deploy workflow (`.github/workflows/deploy.yml`)
3. SCSS entry point + variables partial

**Phase B — Design System**
4. Base dark styles (`_base.scss`, `_layout.scss`)
5. Syntax highlighting overrides (`_syntax.scss`)
6. Component styles (`_components.scss`: nav, figure, blockquote, FAQ)

**Phase C — Layouts & Includes**
7. `_layouts/default.html` — dark shell with nav + footer slots
8. `_layouts/post.html` — post-specific layout
9. `_layouts/page.html` — static page layout
10. `_includes/header.html` — navigation links
11. `_includes/footer.html` — minimal footer
12. `_includes/figure.html` — attributed figure partial

**Phase D — Pages**
13. `index.md` — landing page with featured post
14. `research-sessions.md` — tag-filtered sessions list
15. `about.md` — author bio and blog purpose
16. `faq.md` — Q&A pairs
17. `404.md` — custom 404 page

**Phase E — Mocked Content**
18. Featured post (English, demonstrates code block + figure + README excerpt)
19. Research session 1 (Spanish, `research-session` tag)
20. Research session 2 (bilingual, `research-session` tag, demonstrates code block)
21. Research session 3 (English, `research-session` tag)
