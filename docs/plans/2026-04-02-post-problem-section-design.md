# Design: Post Problem Section

**Date:** 2026-04-02  
**Status:** Approved

## Summary

Add a `problem:` front-matter field to every post. When present, the post layout renders it as a styled callout box above the post body. Each post's problem statement is specific to what that post addresses — not a generic blog-wide motivation.

## Motivation

Posts currently jump straight into content with no framing of *why* the topic matters. Adding a problem statement gives readers immediate context and forces the author to articulate the gap being addressed before explaining the solution.

## Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Where the field lives | Front-matter (`problem: "..."`) | Keeps prose out of the body; enables potential future use in feeds or filtering |
| Rendering | Layout-driven (`_layouts/post.html`) | Single place to maintain; automatic for any post that sets the field |
| Implementation | `{% if page.problem %}` conditional | Posts without the field are unaffected |
| Visual style | Callout box with accent left border | Consistent with dark minimal aesthetic; visually distinct from body text |

## Front-matter Convention

```yaml
problem: "1-3 sentences describing what was broken or missing before this post's approach existed."
```

Optional field. Posts without it render normally.

## Layout Change

In `_layouts/post.html`, before `{{ content }}`:

```liquid
{%- if page.problem -%}
<div class="problem-callout">
  <span class="problem-callout__label">Problem</span>
  <p>{{ page.problem }}</p>
</div>
{%- endif -%}
```

## Component Style

In `_sass/_components.scss`, add `.problem-callout`:

- Background: `var(--surface)`
- Border: `1px solid var(--border)` + `3px solid var(--accent)` left border
- Label: `var(--font-mono)`, uppercase, `font-size: 0.7rem`, `var(--text-secondary)`
- Text: `var(--text-primary)`, `var(--text-base)`
- Margin: `var(--space-xl) 0` (sits between post header and body)

## Scope

All 6 existing posts receive a `problem:` field. Each problem statement is authored specifically for that post's topic.

## Files Affected

- `_layouts/post.html` — add conditional callout block
- `_sass/_components.scss` — add `.problem-callout` styles
- `_posts/*.md` — add `problem:` field to all 6 posts
