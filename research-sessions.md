---
layout: page
title: Research Sessions
permalink: /research-sessions/
lang: en
---

{% assign sessions = site.posts | where_exp: "p", "p.tags contains 'research-session'" %}

{% if sessions.size > 0 %}
<p class="sessions-count">{{ sessions.size }} session{% if sessions.size != 1 %}s{% endif %} documented</p>

<ul class="session-list">
  {% for session in sessions %}
  <li class="session-item">
    <div class="session-meta">
      <time datetime="{{ session.date | date_to_xmlschema }}">
        {{ session.date | date: "%B %-d, %Y" }}
      </time>
      {% if session.lang %}
        <span class="lang-badge lang-badge--{{ session.lang }}">{{ session.lang }}</span>
      {% endif %}
    </div>

    <h2 class="session-title">
      <a href="{{ session.url | relative_url }}">{{ session.title }}</a>
    </h2>

    <p class="session-excerpt">
      {{ session.excerpt | strip_html | truncate: 200 }}
    </p>
  </li>
  {% endfor %}
</ul>
{% else %}
<p class="sessions-empty">No research sessions documented yet.</p>
{% endif %}
