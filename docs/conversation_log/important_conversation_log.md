# Important Conversation Log

This file records key concepts, decisions, and definitions established during learning sessions.

---

## Session 1 — 2026-03-30

### Project Setup

**What is this project?**
A learning blog at `ollerenac.github.io/blog` that documents the process of learning spec-driven development (SDD) using GitHub's spec-kit framework. The blog is itself managed using spec-kit — making the project simultaneously the subject and the vehicle of learning.

**Key decisions made:**
- Tech stack: Jekyll + minima theme (minimal, GitHub-native)
- Hosting: GitHub Pages via GitHub Actions deployment
- Bilingual content: Spanish (primary) + English, using `lang` front-matter field
- Comments: Giscus (GitHub Discussions-based)
- Repo: `ollerenac/blog` — spec-kit and Jekyll coexist in the same repository
- Conversation log location: `docs/conversation_log/important_conversation_log.md`

### What is Spec-Driven Development (SDD)?

SDD is a software development workflow proposed by GitHub (via the spec-kit framework) where every feature begins with a written specification before any code is written. The flow is:

1. **Constitution** — defines the project's non-negotiable principles
2. **Spec** (`/speckit.specify`) — defines WHAT a feature should do
3. **Plan** (`/speckit.plan`) — defines HOW to implement it
4. **Tasks** (`/speckit.tasks`) — breaks the plan into actionable steps
5. **Implement** (`/speckit.implement`) — executes the tasks

The goal is to reduce wasted implementation work by forcing clarity of intent before writing code.

### What is spec-kit?

spec-kit (v0.4.3) is a scaffolding tool by GitHub that sets up the SDD workflow inside a project. It installs:
- `.claude/commands/` — slash commands for Claude Code (speckit.specify, speckit.plan, speckit.tasks, speckit.implement, etc.)
- `.specify/` — templates, scripts, and memory (constitution.md)
- init-options.json — configuration for the spec-kit installation

### What is the Constitution in spec-kit?

The constitution (`.specify/memory/constitution.md`) is the first artifact created in any spec-kit project. It defines the **non-negotiable principles** that govern all development decisions. Every spec, plan, and task must comply with it — there is a "Constitution Check" gate in the plan template that enforces this.

The constitution template ships as a blank file with placeholder tokens (e.g. `[PROJECT_NAME]`, `[PRINCIPLE_1_NAME]`). The `/speckit.constitution` command fills it in based on the project context. This mirrors the workflow shown by Den Delimarsky (GitHub) in his spec-kit demo: you prompt the AI to "fill the constitution with bare minimum requirements" for your project type.

**This project's constitution (v1.0.0, ratified 2026-03-30) established 5 principles:**

| # | Name | Core rule |
|---|------|-----------|
| I | Content-First | Every decision must serve writing/publishing posts |
| II | Static & Simple | Jekyll + minima only, strict YAGNI, no server runtime |
| III | Spec-Driven Development | Full spec-kit workflow mandatory before any code |
| IV | Bilingual by Convention | `lang` front-matter field, Spanish first, no i18n plugin |
| V | Open & Transparent | Giscus comments enabled + conversation log maintained |

**Key insight**: The constitution is versioned (semantic versioning: MAJOR/MINOR/PATCH). Removing or redefining a principle is a MAJOR bump. Adding one is MINOR. Wording fixes are PATCH.

### The CLAUDE.md Gap in spec-kit

As reported in [github/spec-kit#1983](https://github.com/github/spec-kit/issues/1983) by Arun Gupta, spec-kit v0.4.3 does not generate a `CLAUDE.md` file when initializing a project with `--ai claude`. This is a known bug.

**Why it matters**: Claude Code automatically reads `CLAUDE.md` at the start of every session (including after `/clear`). Without it, Claude starts each session with no awareness of the spec-kit methodology, the `.specify/` folder layout, or that `constitution.md` is the source of truth. The AI has to rediscover the project context every time.

**The fix**: Manually create `CLAUDE.md` at the repo root. It should not duplicate the constitution — it should point Claude at it and establish behavioral rules.

**This project's `CLAUDE.md` contains:**
1. **Claude's Role** — read the constitution first; project context summary (what the blog is, key file locations)
2. **SpecKit Commands** — all 8 `/speckit.*` commands listed for quick reference
3. **On Ambiguity** — if a spec is missing or conflicts with the constitution, stop and ask; never infer; prompt `/speckit.specify` before any implementation

**Key insight**: `CLAUDE.md` is the bridge between the AI agent and the project's spec-kit structure. The constitution defines the rules; `CLAUDE.md` tells Claude where to find them and how to behave.

### State of the Art: spec-kit vs. GSD ("Get Shit Done")

Research source: [github/gsd-build/get-shit-done](https://github.com/gsd-build/get-shit-done), surfaced via a Grok SOTA research on SDD trends in Claude Code (posted at x.com/OscarLlerenaCas).

GSD is a meta-prompting and context engineering framework for Claude Code by TÂCHES. It shares spec-kit's core philosophy (spec before code) but adds significant automation and engineering discipline on top.

**GSD workflow:**
1. `/gsd:new-project` — structured intake, parallel domain research, outputs `PROJECT.md`, `REQUIREMENTS.md`, `ROADMAP.md`, `STATE.md`
2. `/gsd:discuss-phase` — lock implementation decisions before planning (UI, API, content structure)
3. `/gsd:plan-phase` — multi-agent research + validation, outputs XML-structured atomic task plans
4. `/gsd:execute-phase` — parallel wave execution, each task gets a fresh 200k token context window, atomic git commit per task
5. `/gsd:verify-work` — automated user acceptance testing; failed tests spawn debug agents
6. `/gsd:ship` — create PR from verified work

**What GSD adds over spec-kit:**

| Feature | spec-kit | GSD |
|---------|----------|-----|
| Philosophy | Spec before code | Spec before code + context discipline |
| Execution | Manual, sequential | Multi-agent parallel waves |
| Context management | None built-in | Core feature (fresh 200k context per executor) |
| Verification | Manual | Automated with debug agents on failure |
| Git discipline | Not enforced | Atomic commit per task |
| Complexity | Low — good for learning | High — good for production scale |

**Key GSD concept — context rot**: As Claude fills its context window with conversation history, output quality degrades. GSD solves this by splitting work into tasks small enough for fresh subagent contexts, so no executor sees accumulated artifacts from prior steps.

**Should this project shift from spec-kit to GSD?**

No — for two reasons:
1. **Learning goal**: The purpose of this project is to learn spec-kit's manual workflow. GSD automates away exactly what we're trying to understand.
2. **Project scale**: A Jekyll blog does not need multi-agent parallel execution or context engineering.

**Key insight**: GSD and spec-kit represent two points on the same SDD spectrum. Both require a spec before code. spec-kit teaches the fundamentals manually; GSD automates them for production-scale complexity. The right path is: learn spec-kit first, then GSD will make sense as a natural evolution.

---

## Session 2 — 2026-03-30

### First Feature Spec: Blog Site Structure & Pages (`001-blog-site-structure`)

**What was specced:**
The full page structure of the research-learning blog — landing page, research sessions page, about page, and FAQ page — including rich content rendering requirements.

**Key decisions made during spec:**

1. **Blog purpose is specific**: The blog documents learning to implement SDD methodologies *with Claude Code* — not SDD in general. This scopes the audience (developers/researchers using AI-assisted coding workflows) and gives research sessions a clear content model.

2. **Rich content types required**: Posts and sessions will contain:
   - Code blocks with syntax highlighting
   - Figures with captions and source attribution (from external authors)
   - Quoted GitHub README excerpts with repository attribution
   - Bilingual text (Spanish first, English after divider)

3. **Markdown is the right approach**: Markdown with a custom Jekyll include partial (`_includes/figure.html`) handles all required content types within the Static & Simple constraint. MDX or a headless CMS would violate the constitution.

4. **Research Sessions = tagged posts (not a separate content type)**: Research sessions are regular blog posts tagged `research-session`. They reuse the standard post layout and `_posts/` collection. The Research Sessions page filters by that tag. This was chosen over a separate Jekyll collection for simplicity.

5. **Featured post is manually designated**: The landing page shows one manually chosen featured post — no algorithm.

**Spec file:** `specs/001-blog-site-structure/spec.md`
**Checklist:** `specs/001-blog-site-structure/checklists/requirements.md` — all items pass
**Next step:** `/speckit.plan`

---
