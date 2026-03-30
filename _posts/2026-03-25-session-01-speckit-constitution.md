---
layout: post
title: "Sesión 01: Creando la Constitución con spec-kit"
date: 2026-03-25
tags: [spec-kit, sdd, lang-es, research-session]
lang: es
featured: false
excerpt: "Primera sesión documentando cómo crear una constitución de proyecto con spec-kit. La constitución es el primer artefacto — define los principios no negociables antes de cualquier código."
---

## Objetivo de la sesión

Entender qué es la constitución en spec-kit y por qué es el primer paso obligatorio antes de cualquier especificación.

## Qué es la constitución

La constitución es un documento Markdown que vive en `.specify/memory/constitution.md`. Define los principios no negociables del proyecto. Cada spec, plan y tarea debe cumplir con ella — hay una compuerta de "Verificación Constitucional" en la plantilla del plan que lo exige.

La plantilla viene con tokens de relleno:

```yaml
# .specify/memory/constitution.md (plantilla vacía)
# [PROJECT_NAME] Constitution
## Core Principles
### I. [PRINCIPLE_1_NAME]
[PRINCIPLE_1_DESCRIPTION]
```

El comando `/speckit.constitution` rellena esos tokens según el contexto del proyecto.

## Principios de este blog

La constitución de este blog define cinco principios:

| # | Nombre | Regla central |
|---|--------|--------------|
| I | Content-First | Cada decisión debe servir a la escritura/publicación de posts |
| II | Static & Simple | Solo Jekyll + minima, YAGNI estricto |
| III | Spec-Driven Development | Flujo completo de spec-kit obligatorio antes de cualquier código |
| IV | Bilingual by Convention | Campo `lang` en front-matter, español primero |
| V | Open & Transparent | Comentarios Giscus + log de conversación mantenido |

## Aprendizaje clave

La constitución no es documentación opcional — es una compuerta real. Si una spec viola un principio constitucional, el plan debe documentar la justificación antes de proceder. Esto obliga a pensar en las consecuencias antes de comprometerse con una decisión técnica.

La versión semántica de la constitución también es importante: eliminar o redefinir un principio es un cambio MAJOR. Añadir uno es MINOR. Correcciones de redacción son PATCH.
