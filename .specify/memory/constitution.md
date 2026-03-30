<!--
SYNC IMPACT REPORT
==================
Version change: (none) → 1.0.0
Modified principles: N/A — initial ratification, all placeholders replaced
Added sections: Core Principles (I–V), Deployment Standards, Development Workflow, Governance
Removed sections: None
Templates checked:
  ✅ .specify/templates/plan-template.md — Constitution Check gate aligns with principles
  ✅ .specify/templates/spec-template.md — No constitution-specific constraints; compatible
  ✅ .specify/templates/tasks-template.md — Phase structure compatible with SDD principle
  ℹ️  .specify/templates/commands/ — Directory not present; .claude/commands/ used instead (no changes needed)
Deferred TODOs: None
-->

# Learning Blog Constitution

## Core Principles

### I. Content-First

Every decision MUST serve the creation and publication of blog content.
No feature, plugin, or configuration is added unless it directly enables
writing, publishing, or reading posts. UI enhancements and tooling are
secondary to the writing workflow.

### II. Static & Simple

The site MUST remain a static Jekyll site deployable via GitHub Actions
to GitHub Pages with no server-side runtime. Dependencies MUST be kept
to an absolute minimum (minima theme, standard GitHub Actions). YAGNI
applies strictly — no feature is built speculatively.

### III. Spec-Driven Development

Every feature MUST follow the full spec-kit workflow before any
implementation:
Constitution → Spec (`/speckit.specify`) → Plan (`/speckit.plan`) →
Tasks (`/speckit.tasks`) → Implement (`/speckit.implement`).
No code is written without an approved spec. This principle is both the
project's methodology and its subject matter.

### IV. Bilingual by Convention

Content MUST declare its language via the `lang` front-matter field
(`es`, `en`, or `bilingual`). Bilingual posts MUST present Spanish first,
followed by English after a `---` divider. Language filtering MUST be
achievable through tags (`lang-es`, `lang-en`) without requiring an i18n
plugin.

### V. Open & Transparent

The learning process MUST be documented openly. Comments MUST be enabled
via Giscus (GitHub Discussions). The conversation log at
`docs/conversation_log/important_conversation_log.md` MUST be kept
up-to-date with key concepts, decisions, and definitions from each
working session.

## Deployment Standards

- GitHub Actions MUST be used for all deployments (never the legacy
  branch-based Pages method).
- The `main` branch is the single source of truth for production content.
- The site MUST be accessible at `ollerenac.github.io/blog`.
- Jekyll build MUST succeed with zero warnings before any merge to `main`.

## Development Workflow

- All work MUST be tracked via spec-kit specs in `specs/` and tasks in
  the corresponding `tasks.md`.
- Design documents MUST be saved to `docs/plans/` before implementation
  begins.
- The conversation log MUST be updated at the end of each session with
  any new concepts or decisions introduced.
- Commits MUST reference the relevant spec or task where applicable.

## Governance

This constitution supersedes all other project guidelines. Any amendment
requires:
1. A documented reason for the change.
2. A version bump following semantic versioning:
   - MAJOR: removal or redefinition of a principle.
   - MINOR: new principle or section added.
   - PATCH: clarification or wording fix.
3. An updated `LAST_AMENDED_DATE`.

All specs and plans MUST verify compliance with this constitution before
proceeding to implementation (Constitution Check gate in plan.md).

**Version**: 1.0.0 | **Ratified**: 2026-03-30 | **Last Amended**: 2026-03-30
