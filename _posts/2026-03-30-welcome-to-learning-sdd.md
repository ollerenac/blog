---
layout: post
title: "Welcome to Learning SDD"
date: 2026-03-30
tags: [sdd, spec-kit, claude-code, lang-en]
lang: en
featured: true
excerpt: "This blog documents my process of learning spec-driven development — writing specs before code, using Claude Code as the implementation engine."
---

This blog is a learning log. Every post here documents something I explored, built, or understood while learning to implement **spec-driven development (SDD)** with Claude Code.

The premise is simple: before writing a single line of code, write a specification. The spec defines *what* the feature should do. Then a plan defines *how*. Then tasks break the plan into executable steps. Only then does implementation begin.

This workflow is enforced by [spec-kit](https://github.com/github/spec-kit) — a scaffolding tool that installs the full SDD workflow into any project.

## Why this blog exists

I wanted a way to track what I learn as I learn it — not just in notes, but in a form that forces clarity. Writing a blog post about a concept requires understanding it well enough to explain it. That constraint is the point.

The blog is also an example of SDD in action. Every feature — including this page — was specced before it was built.

## The workflow in practice

Here's the front-matter schema every post in this blog follows:

```yaml
---
layout: post
title: "Your title here"
date: 2026-03-30
tags: [sdd, spec-kit, lang-en]
lang: en        # es | en | bilingual
featured: false
---
```

The `lang` field is non-negotiable — it drives bilingual filtering across the site.

## What spec-kit installs

When you run `spec-kit init` in a project, you get:

- `.specify/memory/constitution.md` — the project's non-negotiable principles
- `.specify/templates/` — spec, plan, tasks, and checklist templates
- `.claude/commands/` — slash commands that drive the workflow in Claude Code

{% include figure.html
   src="/assets/images/speckit-workflow.png"
   alt="Diagram showing the spec-kit workflow: Constitution → Spec → Plan → Tasks → Implement"
   caption="The spec-kit workflow. Each phase gates the next."
   source_name="spec-kit documentation"
   source_url="https://github.com/github/spec-kit" %}

The constitution is the first artifact. It defines principles that every spec, plan, and task must comply with. This blog's constitution has five principles — Content-First, Static & Simple, Spec-Driven Development, Bilingual by Convention, and Open & Transparent.

Every post you read here was built following that chain.
