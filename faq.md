---
layout: page
title: FAQ
permalink: /faq/
lang: en
faqs:
  - question: "What is spec-driven development (SDD)?"
    answer: "SDD is a software development workflow where every feature begins with a written specification before any code is written. The spec defines what a feature should do — in plain language — and is separate from the plan that defines how to implement it. The goal is to reduce wasted work by forcing clarity of intent before implementation begins."

  - question: "What is spec-kit?"
    answer: "spec-kit is a scaffolding tool by GitHub that installs the SDD workflow into any project. It provides templates for specs, plans, tasks, and checklists — plus Claude Code slash commands (/speckit.specify, /speckit.plan, etc.) that guide you through each step of the workflow."

  - question: "What is Claude Code?"
    answer: "Claude Code is Anthropic's official CLI for Claude — an AI coding assistant that works directly in your terminal and editor. It can read your codebase, execute commands, write and edit files, and follow structured workflows like spec-kit. This blog documents using Claude Code as the implementation engine for the SDD workflow."

  - question: "Why is this blog bilingual?"
    answer: "The author thinks in both Spanish and English, and the learning process happens in both. Posts marked 'bilingual' contain both languages — Spanish first, English second. Single-language posts are marked 'es' or 'en'. No translation plugin is needed — it's a convention baked into the front-matter schema."

  - question: "What is a Research Session?"
    answer: "A Research Session is a blog post tagged 'research-session' that documents a specific learning experiment or methodology exploration. Rather than polished tutorials, these are working notes — what was tried, what was learned, and what would be done differently. They appear on the Research Sessions page and in the main post feed."

  - question: "What is a spec constitution?"
    answer: "The constitution is the first artifact created in any spec-kit project. It defines the non-negotiable principles that govern all development decisions. Every spec, plan, and task must comply with it — there's a 'Constitution Check' gate in the plan template that enforces this. This blog's constitution has five principles covering content priorities, static site constraints, SDD enforcement, bilingual conventions, and transparency."
---

<ul class="faq-list">
  {% for item in page.faqs %}
  <li class="faq-item">
    <p class="faq-question">{{ item.question }}</p>
    <p class="faq-answer">{{ item.answer }}</p>
  </li>
  {% endfor %}
</ul>
