# Learning Blog — Design Document

**Date**: 2026-03-30
**Status**: Approved

## Overview

A bilingual (Spanish/English) learning blog documenting the process of learning spec-driven development (SDD) using GitHub's spec-kit framework. Built with Jekyll, hosted on GitHub Pages at `ollerenac.github.io/blog`, deployed via GitHub Actions. Managed using spec-kit from this same repository.

## 1. Repository

- **GitHub account**: ollerenac
- **Repo name**: `blog` (this repo, `learning-sdd`, pushed to `ollerenac/blog`)
- **Site URL**: `ollerenac.github.io/blog`
- **GitHub Pages source**: GitHub Actions (not legacy branch method)
- Jekyll ignores `.specify/` and `.claude/` dot-folders — spec-kit coexists cleanly at the root

## 2. Jekyll Site Structure

```
/
├── _posts/                   # blog posts (YYYY-MM-DD-title.md)
├── _includes/
│   └── comments.html         # Giscus embed partial
├── _layouts/                 # minimal overrides of minima theme
├── assets/css/               # custom styles
├── _config.yml               # site config (title, baseurl, lang, etc.)
├── index.md                  # home feed (chronological)
├── tags.md                   # browse posts by topic tag
└── docs/
    ├── plans/                # spec-kit design documents
    └── conversation_log/     # important_conversation_log.md
```

Each post uses front-matter:
```yaml
---
layout: post
title: "Qué es SDD / What is SDD"
date: 2026-03-30
tags: [sdd, spec-kit, concepts, lang-es]
lang: es   # es | en | bilingual
---
```

## 3. Bilingual Approach

- `lang` front-matter field: `es`, `en`, or `bilingual`
- Bilingual posts contain both languages in one file: Spanish first, English after a `---` divider
- Language tags (`lang-es`, `lang-en`) on every post allow filtering from the tags page
- No i18n plugin needed — convention-based, upgradeable later

## 4. GitHub Actions Deployment

File: `.github/workflows/deploy.yml`

- Trigger: push to `main`
- Steps: checkout → build with `actions/jekyll-build-pages` → deploy with `actions/deploy-pages`
- GitHub Pages configured to use "GitHub Actions" as source

## 5. Comments (Giscus)

- GitHub Discussions category "Blog Comments" created in `ollerenac/blog`
- Giscus embed snippet generated at giscus.app and placed in `_includes/comments.html`
- Included in the post layout; comments tied to posts via page URL
- Requires GitHub account to comment

## 6. Conversation Log

- Location: `docs/conversation_log/important_conversation_log.md`
- Tracked in git, visible in GitHub UI
- User indicates what to log; assistant writes entries
- Captures key concepts, decisions, and definitions from sessions
