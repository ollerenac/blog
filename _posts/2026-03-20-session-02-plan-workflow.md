---
layout: post
title: "Session 02: The Plan Workflow — From Spec to Architecture"
date: 2026-03-20
tags: [spec-kit, sdd, lang-en, research-session]
lang: en
featured: false
excerpt: "Documenting how /speckit.plan transforms a spec into a concrete implementation plan — with research, data models, contracts, and a design system."
problem: "Writing a spec is not enough — translating it into a concrete build plan requires explicit design decisions about architecture, technology, and trade-offs that the spec itself does not capture."
---

## Session goal

Understand what `/speckit.plan` produces and why the research phase matters before any implementation decisions are made.

## What the plan command does

`/speckit.plan` reads the approved spec and produces a set of design documents:

```bash
specs/001-blog-site-structure/
├── plan.md        # Architecture, tech context, constitution check
├── research.md    # Technical decisions with rationale
├── data-model.md  # Entity schemas
├── contracts/     # Interface contracts
└── quickstart.md  # Local dev setup
```

Each file serves a different audience. `research.md` captures *why* a decision was made — something that gets lost the moment you move to implementation without recording it.

## The constitution check gate

Before Phase 0 research even begins, the plan must pass a constitution check. For this blog, that meant verifying all five principles:

> *"Principle II: The site MUST remain a static Jekyll site deployable via GitHub Actions to GitHub Pages with no server-side runtime. Dependencies MUST be kept to an absolute minimum."*

The plan documents each principle as PASS or FAIL. A FAIL halts the plan until the violation is justified or the approach is changed.

## Key decision recorded in research.md

One decision that research.md captured for this blog:

> *GitHub Pages compatibility: Use Jekyll 4.x in the Gemfile directly (not the `github-pages` gem). The GitHub Actions workflow handles building and deploying. This is already the chosen deployment method per the constitution.*

Without recording this in research.md, a future contributor (or future me) would re-discover this constraint the hard way — by deploying and watching it fail.

## What I'd do differently

The data-model.md is the most underrated artifact. Defining the post front-matter schema before writing any posts meant every mocked content file had consistent structure from day one. That consistency is what makes Liquid filters work reliably.
