# Contract: Post Front-Matter

**Type**: Content authoring contract
**Applies to**: All files in `_posts/`

---

## Required Fields

| Field | Type | Valid Values | Example |
|-------|------|-------------|---------|
| `layout` | string | `post` | `layout: post` |
| `title` | string | Any non-empty string | `title: "What is SDD"` |
| `date` | date | `YYYY-MM-DD` | `date: 2026-03-30` |
| `tags` | array | See tag vocabulary | `tags: [sdd, lang-en]` |
| `lang` | string | `es`, `en`, `bilingual` | `lang: en` |

## Optional Fields

| Field | Type | Default | Example |
|-------|------|---------|---------|
| `featured` | boolean | `false` | `featured: true` |
| `excerpt` | string | Auto-generated | `excerpt: "A short summary..."` |

## Tag Vocabulary

Every post MUST include exactly one language tag:

| Tag | Meaning |
|-----|---------|
| `lang-es` | Spanish-only post |
| `lang-en` | English-only post |
| `lang-bilingual` | Bilingual post (Spanish first, then English after `---`) |

Content tags (use as applicable):

| Tag | Meaning |
|-----|---------|
| `sdd` | Spec-driven development topic |
| `spec-kit` | spec-kit tool topic |
| `research-session` | Marks post as a research session (appears on Research Sessions page) |
| `claude-code` | Claude Code topic |

## Invariants

1. `lang` value and the `lang-*` tag must agree (e.g., `lang: bilingual` requires `lang-bilingual` tag)
2. Exactly one post in `_posts/` should have `featured: true` at any time
3. Bilingual posts: Spanish content comes first; a `---` Markdown divider separates sections; English follows
4. Post filename format: `YYYY-MM-DD-slug.md`
