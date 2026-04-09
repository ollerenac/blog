---
layout: post
title: "Welcome to Learning SDD"
date: 2026-03-30
tags: [sdd, spec-kit, claude-code, lang-en]
lang: en
featured: true
excerpt: "This blog documents my process of learning spec-driven development — writing specs before code, using Claude Code as the implementation engine."
problem: "Working on serious projects with Claude Code without a systematic methodology meant every session started from scratch. There was no persistent artifact — spec, decisions, rationale — carrying context between conversations."
---

I am pretty sure that many low-or-medium-expert-level Claude-Code users, until now, has not dominated the dynamics of developing long-run-bank-memory demanding projects.

The premise is simple: before writing a single line of code, write a specification. The spec defines *what* the feature should do. Then a plan defines *how*. Then tasks break the plan into executable steps. Only then does implementation begin.

The current trend is SDD. The guys from GitHub have created a framework for SDD implementation that can be locally installed and run via claude-code terminal command. This workflow is enforced by [spec-kit](https://github.com/github/spec-kit) — a scaffolding tool that installs the full SDD workflow into any project.

This blog is a learning log. Every post here documents something I explored, built, or understood while learning to implement **spec-driven development (SDD)** with Claude Code.

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

<figure class="post-figure">
<div style="font-family: var(--font-mono); font-size: 0.8rem; padding: 1.5rem; background: var(--surface); border: 1px solid var(--border); border-radius: 6px; overflow-x: auto;">
  <div style="display: flex; align-items: center; gap: 0; flex-wrap: nowrap; min-width: max-content;">
    <div style="background: var(--bg); border: 1px solid var(--accent); color: var(--accent); padding: 0.4rem 0.8rem; border-radius: 4px; white-space: nowrap;">Constitution</div>
    <div style="color: var(--text-secondary); padding: 0 0.4rem;">→</div>
    <div style="background: var(--bg); border: 1px solid var(--border); color: var(--text-primary); padding: 0.4rem 0.8rem; border-radius: 4px; white-space: nowrap;">Spec</div>
    <div style="color: var(--text-secondary); padding: 0 0.4rem;">→</div>
    <div style="background: var(--bg); border: 1px solid var(--border); color: var(--text-primary); padding: 0.4rem 0.8rem; border-radius: 4px; white-space: nowrap;">Plan</div>
    <div style="color: var(--text-secondary); padding: 0 0.4rem;">→</div>
    <div style="background: var(--bg); border: 1px solid var(--border); color: var(--text-primary); padding: 0.4rem 0.8rem; border-radius: 4px; white-space: nowrap;">Tasks</div>
    <div style="color: var(--text-secondary); padding: 0 0.4rem;">→</div>
    <div style="background: var(--bg); border: 1px solid var(--border); color: var(--text-primary); padding: 0.4rem 0.8rem; border-radius: 4px; white-space: nowrap;">Implement</div>
  </div>
  <div style="margin-top: 0.8rem; color: var(--text-secondary); font-size: 0.72rem;">Each phase gates the next. No implementation without tasks. No tasks without a plan.</div>
</div>
<figcaption>The spec-kit workflow. Each phase gates the next. <span class="attribution">Source: <a href="https://github.com/github/spec-kit">spec-kit documentation</a></span></figcaption>
</figure>

The constitution is the first artifact. It defines principles that every spec, plan, and task must comply with. This blog's constitution has five principles — Content-First, Static & Simple, Spec-Driven Development, Bilingual by Convention, and Open & Transparent.

Every post you read here was built following that chain.
