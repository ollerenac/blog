---
layout: default
title: Home
---

{% assign featured = site.posts | where: "featured", true | first %}
{% assign featured = featured | default: site.posts.first %}

{% if featured %}
<div class="featured-card">
  <span class="featured-label">Featured</span>

  <h2 class="featured-title">
    <a href="{{ featured.url | relative_url }}">{{ featured.title }}</a>
  </h2>

  <div class="featured-meta">
    <time datetime="{{ featured.date | date_to_xmlschema }}">
      {{ featured.date | date: "%B %-d, %Y" }}
    </time>
    {% if featured.lang %}
      <span class="lang-badge lang-badge--{{ featured.lang }}">{{ featured.lang }}</span>
    {% endif %}
  </div>

  <p class="featured-excerpt">
    {{ featured.excerpt | strip_html | truncate: 280 }}
  </p>

  <a href="{{ featured.url | relative_url }}" class="read-more">Read more</a>
</div>
{% endif %}

<div class="site-intro">
  <span class="intro-label">About this blog</span>
  <p>
    A learning log documenting the process of implementing
    <strong>spec-driven development</strong> with Claude Code.
    Each post explores a methodology, decision, or workflow
    from real sessions — written before the code, not after.
  </p>
</div>
