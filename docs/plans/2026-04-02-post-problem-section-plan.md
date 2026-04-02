# Post Problem Section Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add a `problem:` front-matter field to every post that renders as a styled callout box between the post header and body.

**Architecture:** Layout-driven — `_layouts/post.html` conditionally renders a `.problem-callout` div when `page.problem` is set. Styles live in `_sass/_components.scss`. All 6 existing posts get a `problem:` field authored for their specific topic.

**Tech Stack:** Jekyll 4.x, Liquid templating, SCSS with CSS custom properties

---

### Task 1: Add `.problem-callout` styles to `_components.scss`

**Files:**
- Modify: `_sass/_components.scss` (append at end of file)

**Step 1: Append the component styles**

Add this block at the end of `_sass/_components.scss`:

```scss
// ---- Problem callout ----

.problem-callout {
  margin: var(--space-xl) 0;
  padding: var(--space-md) var(--space-lg);
  background: var(--surface);
  border: 1px solid var(--border);
  border-left: 3px solid var(--accent);
  border-radius: var(--border-radius);

  .problem-callout__label {
    display: block;
    font-family: var(--font-mono);
    font-size: 0.7rem;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--text-secondary);
    margin-bottom: var(--space-sm);
  }

  p {
    margin: 0;
    color: var(--text-primary);
    font-size: var(--text-base);
    line-height: 1.6;
  }
}
```

**Step 2: Build to verify no SCSS errors**

```bash
bundle exec jekyll build
```

Expected: `done in X seconds.` with no errors.

**Step 3: Commit**

```bash
git add _sass/_components.scss
git commit -m "feat: add .problem-callout component styles"
```

---

### Task 2: Update `_layouts/post.html` to render the callout

**Files:**
- Modify: `_layouts/post.html`

**Step 1: Add the conditional block**

In `_layouts/post.html`, insert this block between `</header>` and `<div class="post-content">`:

```liquid
  {%- if page.problem -%}
  <div class="problem-callout">
    <span class="problem-callout__label">Problem</span>
    <p>{{ page.problem }}</p>
  </div>
  {%- endif -%}
```

The full file should look like:

```html
---
layout: default
---
<article class="post">
  <header class="post-header">
    <h1 class="post-title">{{ page.title }}</h1>
    <div class="post-meta">
      <time datetime="{{ page.date | date_to_xmlschema }}">
        {{ page.date | date: "%B %-d, %Y" }}
      </time>
      {%- if page.lang -%}
        <span class="lang-badge lang-badge--{{ page.lang }}">{{ page.lang }}</span>
      {%- endif -%}
    </div>
  </header>

  {%- if page.problem -%}
  <div class="problem-callout">
    <span class="problem-callout__label">Problem</span>
    <p>{{ page.problem }}</p>
  </div>
  {%- endif -%}

  <div class="post-content">
    {{ content }}
  </div>

  {%- if page.tags and page.tags.size > 0 -%}
  <div class="post-tags">
    {%- for tag in page.tags -%}
      {%- unless tag contains 'lang-' -%}
        <span class="tag">{{ tag }}</span>
      {%- endunless -%}
    {%- endfor -%}
  </div>
  {%- endif -%}
</article>
```

**Step 2: Build to verify**

```bash
bundle exec jekyll build
```

Expected: `done in X seconds.` with no errors.

**Step 3: Commit**

```bash
git add _layouts/post.html
git commit -m "feat: render problem callout in post layout when problem: field is set"
```

---

### Task 3: Add `problem:` field to all 6 posts

**Files:**
- Modify: `_posts/2026-03-30-welcome-to-learning-sdd.md`
- Modify: `_posts/2026-03-28-sdd-workflow-with-claude-code.md`
- Modify: `_posts/2026-03-30-sdd-levels-diagrams.md`
- Modify: `_posts/2026-03-25-session-01-speckit-constitution.md`
- Modify: `_posts/2026-03-20-session-02-plan-workflow.md`
- Modify: `_posts/2026-03-15-session-03-tasks-and-implement.md`

**Step 1: Add `problem:` to each post front-matter (after `excerpt:`)**

`2026-03-30-welcome-to-learning-sdd.md`:
```yaml
problem: "Working on serious projects with Claude Code without a systematic methodology meant every session started from scratch. There was no persistent artifact — spec, decisions, rationale — carrying context between conversations."
```

`2026-03-28-sdd-workflow-with-claude-code.md`:
```yaml
problem: "Jumping directly into code with an AI agent produces working prototypes but leaves no record of why decisions were made. When requirements shift, there is nothing to update — context lives only in the chat history."
```

`2026-03-30-sdd-levels-diagrams.md`:
```yaml
problem: "The term 'spec-driven development' is used loosely across tools and articles, making it hard to compare approaches. Without a shared vocabulary for the levels of SDD, evaluating tools like Kiro or spec-kit becomes guesswork."
```

`2026-03-25-session-01-speckit-constitution.md`:
```yaml
problem: "Starting a project with Claude Code requires establishing ground rules that every future session must respect. Without a persistent constitution, each conversation can drift away from the project's principles."
```

`2026-03-20-session-02-plan-workflow.md`:
```yaml
problem: "Writing a spec is not enough — translating it into a concrete build plan requires explicit design decisions about architecture, technology, and trade-offs that the spec itself does not capture."
```

`2026-03-15-session-03-tasks-and-implement.md`:
```yaml
problem: "A plan without granular tasks is too abstract for an AI agent to execute reliably. The gap between 'how to build it' and 'what to do next' causes drift and missed requirements."
```

**Step 2: Build to verify**

```bash
bundle exec jekyll build
```

Expected: `done in X seconds.` with no errors.

**Step 3: Commit**

```bash
git add _posts/
git commit -m "content: add problem field to all 6 posts"
```

---

### Task 4: Push and verify on live site

**Step 1: Push to main**

```bash
git push origin main
```

**Step 2: Verify deployment**

Wait ~60 seconds for GitHub Actions to deploy, then open:
`https://ollerenac.github.io/blog/2026/03/30/welcome-to-learning-sdd/`

Expected: Purple left-bordered callout box appears between the post title/date and the post body, with "PROBLEM" label and the problem text.

**Step 3: Check a post without `problem:` (none currently — all 6 are updated)**

If you add a future post without `problem:`, verify the callout does not appear and the layout renders normally.
