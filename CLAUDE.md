# Claude's Role

Read `.specify/memory/constitution.md` first. It is the authoritative source of truth for this project. Everything in it is non-negotiable.

This project is a bilingual (Spanish/English) learning blog at `ollerenac.github.io/blog`, built with Jekyll and managed via spec-kit. The blog documents the process of learning spec-driven development (SDD). Spec-kit is both the project's methodology and its subject matter.

Key context:
- Design documents live in `docs/plans/`
- Conversation log (key concepts and decisions) lives in `docs/conversation_log/important_conversation_log.md`
- Jekyll site files coexist at the repo root alongside `.specify/` and `.claude/`

## SpecKit Commands

- `/speckit.constitution` — create or update the project constitution
- `/speckit.specify` — generate a feature spec
- `/speckit.clarify` — identify underspecified areas in a spec
- `/speckit.plan` — generate an implementation plan from a spec
- `/speckit.tasks` — generate a task list from a plan
- `/speckit.implement` — execute the task list
- `/speckit.analyze` — cross-artifact consistency check
- `/speckit.checklist` — generate a custom checklist for a feature

## On Ambiguity

If a spec is missing, incomplete, or conflicts with the constitution — stop and ask. Do not infer. Do not proceed.

If the user asks to implement something without a spec, prompt them to run `/speckit.specify` first.

## Active Technologies
- Ruby (Jekyll 4.x), HTML5, CSS3, Markdown (Kramdown) + `jekyll` (4.x), `minima` theme (overridden), `rouge` (syntax highlighting, bundled with Jekyll), `webrick` (local dev server) (001-blog-site-structure)
- N/A — static files only (001-blog-site-structure)

## Recent Changes
- 001-blog-site-structure: Added Ruby (Jekyll 4.x), HTML5, CSS3, Markdown (Kramdown) + `jekyll` (4.x), `minima` theme (overridden), `rouge` (syntax highlighting, bundled with Jekyll), `webrick` (local dev server)
