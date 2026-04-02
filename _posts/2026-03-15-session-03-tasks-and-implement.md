---
layout: post
title: "Sesión 03: Tareas e Implementación / Session 03: Tasks and Implementation"
date: 2026-03-15
tags: [spec-kit, sdd, lang-bilingual, research-session]
lang: bilingual
featured: false
excerpt: "Cómo /speckit.tasks convierte un plan en pasos ejecutables — y por qué la organización por historia de usuario importa. / How /speckit.tasks converts a plan into executable steps — and why user story organization matters."
problem: "A plan without granular tasks is too abstract for an AI agent to execute reliably. The gap between 'how to build it' and 'what to do next' causes drift and missed requirements."
---

## Generando tareas desde el plan

El comando `/speckit.tasks` lee el plan aprobado y genera un archivo `tasks.md` organizado por historia de usuario. Cada tarea tiene un ID (`T001`), un marcador de paralelismo opcional (`[P]`), y la historia de usuario a la que pertenece (`[US1]`).

La organización por historia de usuario no es cosmética. Significa que cada historia puede implementarse y validarse de forma independiente. El MVP es siempre la Historia de Usuario 1 — puedes parar ahí si necesitas entregar algo funcionando rápidamente.

### Formato de tarea

```markdown
- [ ] T012 [P] [US1] Crear `_layouts/post.html` en el directorio de layouts
```

- `[ ]` — checkbox de progreso
- `T012` — ID de tarea, en orden de ejecución
- `[P]` — puede ejecutarse en paralelo (archivos distintos, sin dependencias)
- `[US1]` — traza a la Historia de Usuario 1 en la spec

---

## Generating tasks from the plan

The `/speckit.tasks` command reads the approved plan and generates a `tasks.md` file organized by user story. Each task has an ID (`T001`), an optional parallelism marker (`[P]`), and the user story it belongs to (`[US1]`).

The user story organization is not cosmetic. It means each story can be implemented and validated independently. The MVP is always User Story 1 — you can stop there if you need to deliver something working quickly.

### What makes a good task

A good task is specific enough that an LLM can complete it without additional context. Compare:

❌ Too vague:
```
- [ ] T005 Create stylesheet
```

✅ Specific enough:
```
- [ ] T005 Create `_sass/_syntax.scss` overriding Rouge `.highlight` defaults
  with dark palette: keywords #c792ea, strings #c3e88d, numbers #f78c6c
```

The file path is required. The expected content is specified. There's no ambiguity about what "done" means.

### The implement command

`/speckit.implement` reads `tasks.md` and executes each task in order, respecting dependencies and running parallel tasks together. After each phase, it marks tasks complete in the file and reports progress.

The key insight: the implementation command is only as good as the tasks it receives. Vague tasks produce vague implementations. The discipline lives in the task generation step, not the execution step.
