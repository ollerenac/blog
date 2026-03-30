---
layout: page
title: About
permalink: /about/
lang: en
---

<div class="about-bio">
  <h2 class="bio-name">Oscar Llerena</h2>
  <p class="bio-role">Researcher · Learning SDD with Claude Code</p>
  <p>
    I'm a researcher exploring how spec-driven development changes the way we build software with AI coding assistants. This blog is my working notes — a record of what I try, what works, and what doesn't.
  </p>
</div>

## What this blog is

Every post here documents a real learning session. The blog is itself managed using spec-kit — the same methodology I'm writing about. That means every feature you see was specced before it was built.

The focus is narrow: **implementing SDD methodologies with Claude Code**. Not AI in general. Not software development in general. Just this specific intersection — what happens when you impose a structured spec-driven workflow on an AI coding assistant.

## What is spec-driven development?

SDD is a workflow where every feature begins with a written specification before any code is written. The specification defines *what* the feature should do — in plain language, for any reader. A separate plan then defines *how* to implement it.

The workflow this blog follows:

1. **Constitution** — defines the project's non-negotiable principles
2. **Spec** — defines what a feature does (user stories, requirements, success criteria)
3. **Plan** — defines how to implement it (technical context, architecture, design decisions)
4. **Tasks** — breaks the plan into specific, executable steps
5. **Implement** — executes the tasks

Each step gates the next. No implementation without tasks. No tasks without a plan. No plan without a spec.

## What is spec-kit?

[spec-kit](https://github.com/github/spec-kit) is a scaffolding tool by GitHub that installs the SDD workflow into any project. It adds templates, scripts, and Claude Code slash commands that enforce the workflow.

## Why bilingual?

Because I think in both Spanish and English, and the learning happens in both. Posts marked `lang: bilingual` contain both — Spanish first, English second. Posts marked `lang: es` or `lang: en` are in one language only.
