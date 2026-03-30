# Tasks: Blog Site Structure & Pages

**Input**: Design documents from `/specs/001-blog-site-structure/`
**Prerequisites**: plan.md ✅ | spec.md ✅ | research.md ✅ | data-model.md ✅ | contracts/ ✅

**Organization**: Tasks grouped by user story for independent implementation and testing.
**Tests**: Not requested — no test tasks included.

## Format: `[ID] [P?] [Story?] Description`

- **[P]**: Can run in parallel (different files, no dependencies on incomplete tasks)
- **[Story]**: Which user story this task belongs to (US1–US5)

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Jekyll project scaffolding — must be in place before any content or styling work.

- [x] T001 Create `Gemfile` with Jekyll 4.x, minima theme, and webrick gem at repo root
- [x] T002 Create `_config.yml` with baseurl `/blog`, url, title, description, lang, highlighter, kramdown, and exclude list (`.specify/`, `.claude/`, `specs/`, `docs/`, `CLAUDE.md`) at repo root
- [x] T003 [P] Create `.github/workflows/deploy.yml` GitHub Actions workflow (checkout → jekyll build → deploy to GitHub Pages)
- [x] T004 [P] Create `assets/css/main.scss` SCSS entry point and `_sass/` directory structure (empty partials: `_variables.scss`, `_base.scss`, `_layout.scss`, `_syntax.scss`, `_components.scss`)
- [x] T005 [P] Create `.gitignore` excluding `_site/`, `.bundle/`, `.jekyll-cache/`, `vendor/`

**Checkpoint**: `bundle install` succeeds and `bundle exec jekyll build --dry-run` runs without errors.

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Design system and layout infrastructure that ALL user stories depend on. No page work can begin until this phase is complete.

**⚠️ CRITICAL**: No user story work can begin until this phase is complete.

- [x] T006 Create `_sass/_variables.scss` with full dark minimal design token set: `--bg: #0d0d0d`, `--surface: #1a1a1a`, `--border: #2a2a2a`, `--text-primary: #e8e8e8`, `--text-secondary: #888888`, `--accent: #7c6af7`, `--code-bg: #141414`, `--font-body: 'Inter', system-ui, sans-serif`, `--font-mono: 'JetBrains Mono', 'Fira Code', monospace`
- [x] T007 Create `_sass/_base.scss` with dark reset: `body` background `var(--bg)`, text `var(--text-primary)`, font-family `var(--font-body)`, link color `var(--accent)`, base responsive typography scale
- [x] T008 [P] Create `_sass/_layout.scss` with page and post layout: max-width container, responsive padding, header/footer regions, post content width constraints
- [x] T009 [P] Create `_sass/_syntax.scss` overriding Rouge `.highlight` defaults: code block background `var(--code-bg)`, dark palette for keywords (purple), strings (green), numbers (orange), comments (grey), functions (blue), matching design token colors
- [x] T010 [P] Create `_sass/_components.scss` with styles for: nav links, `figure.post-figure` + `figcaption`, `.attribution` span, blockquote (README excerpt style), FAQ question/answer pairs
- [x] T011 Update `assets/css/main.scss` to import all five SCSS partials in correct order (variables → base → layout → syntax → components)
- [x] T012 Create `_layouts/default.html` — base dark layout shell with `<head>` (meta, CSS link, title), `<header>` slot for nav include, `<main>` content slot, `<footer>` slot
- [x] T013 [P] Create `_layouts/post.html` — extends default, adds post header (title, date, lang badge, tags), post body content, bilingual divider handling
- [x] T014 [P] Create `_layouts/page.html` — extends default, adds page title heading, page body content
- [x] T015 Create `_includes/header.html` — site name/logo link + navigation links to: Home (`/blog/`), Research Sessions (`/blog/research-sessions/`), About (`/blog/about/`), FAQ (`/blog/faq/`)
- [x] T016 [P] Create `_includes/footer.html` — minimal dark footer with site name and year
- [x] T017 Create `_includes/figure.html` — attributed figure partial per `contracts/figure-include.md`: accepts `src`, `alt`, `caption`, `source_name`, `source_url`; renders `<figure>` with `<img>` and `<figcaption>` containing caption + attribution with all fallback cases handled

**Checkpoint**: `bundle exec jekyll serve` starts, site loads at `localhost:4000/blog` with dark background. No pages have content yet — that's expected.

---

## Phase 3: User Story 1 — First-Time Visitor Discovers the Blog (P1) 🎯 MVP

**Goal**: Landing page with one featured post that communicates the blog's purpose and stands out visually.

**Independent Test**: Open `localhost:4000/blog` — one featured post is visible with title, excerpt, and "read more" link. Design is dark and distinct from default minima.

- [x] T018 [US1] Create `_posts/2026-03-30-welcome-to-learning-sdd.md` — featured post: `featured: true`, `lang: en`, `tags: [sdd, spec-kit, claude-code, lang-en]`, content includes a brief intro to the blog's purpose, one code block (YAML front-matter example), and an `{% include figure.html %}` call with a mocked image path and attribution
- [x] T019 [US1] Create `index.md` — landing page using `layout: page`; Liquid logic to find the featured post (`where: "featured", true | first`, fallback to `site.posts.first`); renders featured post card (title, date, excerpt, "Read more →" link); below featured: short site description stating blog focus (SDD with Claude Code)

**Checkpoint**: Homepage shows featured post card. Clicking "Read more" loads the full post with dark styling, code block highlighted, and figure rendered with attribution.

---

## Phase 4: User Story 2 — Visitor Reads a Post with Rich Content (P2)

**Goal**: A post that demonstrates all rich content types: syntax-highlighted code, attributed figure, quoted README excerpt, and bilingual format.

**Independent Test**: Open the rich-content demo post — code block has syntax colors, figure shows caption + attribution link, README blockquote is visually distinct, bilingual divider separates Spanish and English sections.

- [x] T020 [US2] Create `_posts/2026-03-28-sdd-workflow-with-claude-code.md` — bilingual demo post: `lang: bilingual`, `tags: [sdd, claude-code, lang-bilingual, research-session]`, `featured: false`; content includes: (a) Spanish intro paragraph, (b) `---` bilingual divider, (c) English section with a fenced code block (YAML, labelled), (d) `{% include figure.html %}` with mocked image, caption, source_name and source_url, (e) a blockquote styled as a README excerpt with a source credit below it

**Checkpoint**: Post renders with all four rich content types visible and correctly styled. No layout breaks on mobile.

---

## Phase 5: User Story 3 — Visitor Explores Research Sessions (P3)

**Goal**: Research Sessions page listing all posts tagged `research-session`, ordered newest first, each showing title, date, and description.

**Independent Test**: Navigate to `/blog/research-sessions/` — multiple session entries listed in reverse chronological order, each with title, date, and excerpt. Clicking an entry loads the full post.

- [x] T021 [US3] Create `research-sessions.md` — page using `layout: page`, `permalink: /research-sessions/`; Liquid logic: `{% assign sessions = site.posts | where_exp: "p", "p.tags contains 'research-session'" %}`; renders each session as a card (title, date, excerpt, link); shows count of sessions; empty state message if no sessions found
- [x] T022 [P] [US3] Create `_posts/2026-03-25-session-01-speckit-constitution.md` — research session: `lang: es`, `tags: [spec-kit, sdd, lang-es, research-session]`; Spanish-language content documenting what was learned setting up the spec-kit constitution; includes a short code block (YAML constitution example)
- [x] T023 [P] [US3] Create `_posts/2026-03-20-session-02-plan-workflow.md` — research session: `lang: en`, `tags: [spec-kit, sdd, lang-en, research-session]`; English content documenting the plan workflow; includes a Bash code block and a README excerpt blockquote with source credit
- [x] T024 [P] [US3] Create `_posts/2026-03-15-session-03-tasks-and-implement.md` — research session: `lang: bilingual`, `tags: [spec-kit, sdd, lang-bilingual, research-session]`; bilingual content with `---` divider; Spanish summary first, English detail second

**Checkpoint**: Research Sessions page shows 3 mocked sessions (T020's post also appears here since it carries the `research-session` tag — 4 total). All are ordered newest first.

---

## Phase 6: User Story 4 — Visitor Learns About the Blog (P4)

**Goal**: About page with mocked author bio and explanation of the blog's purpose (SDD with Claude Code).

**Independent Test**: Navigate to `/blog/about/` — author name/bio visible, blog purpose stated, SDD + Claude Code context explained.

- [x] T025 [US4] Create `about.md` — page using `layout: page`, `permalink: /about/`, `lang: en`; mocked content: author name (Oscar Llerena), brief bio (researcher learning SDD), blog purpose (documenting methodologies for implementing SDD with Claude Code), short description of what spec-kit is and why this blog exists

**Checkpoint**: About page renders cleanly with dark styling. Purpose of the blog is clear from reading the page.

---

## Phase 7: User Story 5 — Visitor Gets Answers on FAQ (P5)

**Goal**: FAQ page with at least 5 mocked Q&A pairs in a scannable format.

**Independent Test**: Navigate to `/blog/faq/` — at least 5 Q&A pairs visible, questions visually distinct from answers, easy to scan.

- [x] T026 [US5] Create `faq.md` — page using `layout: page`, `permalink: /faq/`, `lang: en`; front-matter `faqs:` array with 6 mocked Q&A pairs covering: (1) What is SDD?, (2) What is spec-kit?, (3) What is Claude Code?, (4) Why a bilingual blog?, (5) How are posts structured?, (6) What is a Research Session?; Liquid loop renders each as styled question + answer block using `.faq-item` component class from `_components.scss`

**Checkpoint**: FAQ page shows all 6 pairs. Questions are bold/distinct from answers. Page is scannable without reading everything.

---

## Phase 8: Polish & Cross-Cutting Concerns

**Purpose**: Final touches that affect the whole site.

- [x] T027 [P] Create `404.md` — custom 404 page using `layout: page`, `permalink: /404.html`; on-brand dark message ("Page not found"), link back to home, brief friendly text
- [x] T028 Run `bundle exec jekyll build --dry-run` and resolve any warnings or front-matter errors across all files
- [ ] T029 [P] Verify navigation links resolve correctly on all pages: Home, Research Sessions, About, FAQ all reachable in one click from any page
- [ ] T030 [P] Visual check at 375px width (mobile) and 1440px width (desktop) — no content overflow, no broken layout, all text readable

**Checkpoint**: `bundle exec jekyll build` succeeds with zero warnings. All pages render correctly at both breakpoints. Site is ready for deployment to GitHub Pages.

---

## Dependencies & Execution Order

### Phase Dependencies

- **Phase 1 (Setup)**: No dependencies — start immediately
- **Phase 2 (Foundational)**: Depends on Phase 1 — **BLOCKS all user stories**
- **Phase 3–7 (User Stories)**: All depend on Phase 2 completion
  - Can proceed sequentially (P1 → P2 → P3 → P4 → P5) or in priority order
- **Phase 8 (Polish)**: Depends on all desired user stories being complete

### User Story Dependencies

- **US1 (P1)**: Needs Phase 2 only. No story dependencies.
- **US2 (P2)**: Needs Phase 2 + `_includes/figure.html` (T017, in Phase 2). No story dependencies.
- **US3 (P3)**: Needs Phase 2. Benefits from US2 posts existing (they appear on the sessions page), but independently testable.
- **US4 (P4)**: Needs Phase 2 only. Fully independent.
- **US5 (P5)**: Needs Phase 2 only. Fully independent.

### Within Each Phase

- Foundation tasks: SCSS partials (T007–T010) can run in parallel after T006
- Layouts (T013, T014) can run in parallel after T012
- Mocked posts within a story (T022, T023, T024) can run in parallel
- Pages (T025, T026) are independent of each other

---

## Parallel Example: Phase 2 (Foundational)

```
# After T006 (_variables.scss), run in parallel:
T007: _layout.scss
T008: _syntax.scss
T009: _components.scss

# After T007–T010 and T011 (main.scss), run in parallel:
T013: _layouts/post.html
T014: _layouts/page.html

# After T012 (default.html), run in parallel:
T016: _includes/footer.html
T017: _includes/figure.html
```

## Parallel Example: Phase 5 (US3 Research Sessions)

```
# After T021 (research-sessions.md page), run in parallel:
T022: session-01 post (Spanish)
T023: session-02 post (English)
T024: session-03 post (bilingual)
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (**critical — blocks everything**)
3. Complete Phase 3: US1 (landing page + featured post)
4. **STOP and VALIDATE**: Site loads, featured post visible, dark design working
5. Deploy to GitHub Pages and confirm live URL works

### Incremental Delivery

1. Phase 1 + 2 → Foundation ready (dark site skeleton, no content)
2. + Phase 3 → MVP: working landing page ✅
3. + Phase 4 → Rich content rendering validated ✅
4. + Phase 5 → Research Sessions page live ✅
5. + Phase 6 + 7 → About + FAQ complete ✅
6. Phase 8 → Polish and deploy full site ✅

---

## Notes

- [P] tasks operate on different files with no blocking dependencies — safe to run in parallel
- [Story] labels map each task to its user story for traceability back to spec.md
- Each user story phase is independently deployable — the site is functional after each one
- Commit after each phase or logical group (e.g., after all SCSS partials, after all mocked posts)
- The `bundle exec jekyll build --dry-run` checkpoint after Phase 1 catches config errors early
- Total tasks: **30** across 8 phases
