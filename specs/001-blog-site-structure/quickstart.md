# Quickstart: Local Development

**Feature**: `001-blog-site-structure`

---

## Prerequisites

- Ruby 3.x (`ruby --version`)
- Bundler (`gem install bundler`)

## Setup

```bash
# From repo root
bundle install
```

## Run locally

```bash
bundle exec jekyll serve --livereload
```

Site available at: `http://localhost:4000/blog`

## Build only (no server)

```bash
bundle exec jekyll build
```

Output goes to `_site/`. This folder is gitignored.

## Validate build (no output written)

```bash
bundle exec jekyll build --dry-run
```

Use this to check for front-matter errors and broken Liquid tags before committing.

## Exclude spec-kit files

The `_config.yml` `exclude:` list prevents Jekyll from processing `.specify/`, `specs/`, `docs/`, and `CLAUDE.md`. If you add new top-level non-Jekyll directories, add them to `exclude:` too.

## Deployment

Push to `main`. The GitHub Actions workflow (`.github/workflows/deploy.yml`) builds and deploys automatically to `https://ollerenac.github.io/blog`.
