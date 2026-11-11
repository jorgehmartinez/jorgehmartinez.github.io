# Sitio personal — Jorge Huanca Martinez

Sitio bilingüe (español e inglés) hecho con [Quarto](https://quarto.org): portada con trayectoria, blog, proyectos, "Sobre mí" y recursos. Se publica solo en GitHub Pages con cada `push` a `main`.

## Estructura

```
_quarto.yml                     Configuración general (título, menú, pie, tema)
index.qmd                       Portada en español (incluye los datos de la trayectoria)
sobre-mi.qmd, recursos.qmd      Páginas en español
proyectos/proyectos.yml         Proyectos en español  ─┐ actualiza
en/projects/projects.yml        Proyectos en inglés   ─┘ ambos
proyectos/img/                  Miniaturas de los proyectos (compartidas)
en/                             Versión en inglés (index, about, resources, blog, projects)
blog/posts/<nombre>/index.qmd   Una carpeta por entrada (aparece en ambos blogs)
_freeze/                        Resultados de código ya calculados (se sube al repo)
styles/custom.scss              Colores, tipografía y estilo visual
includes/head.html              Fuente y script de visitas (GoatCounter)
includes/site.html              Traducción del menú, botón ES/EN y línea de tiempo
.github/workflows/publish.yml   Publicación automática
```

## Uso diario

```bash
quarto preview     # vista previa local con recarga automática
quarto render      # genera el sitio completo en _site/
```

## Entradas del blog

Crea `blog/posts/AAAA-MM-DD-nombre/index.qmd` con este encabezado:

```yaml
---
title: "Título"
description: "Una frase para el listado."
date: 2026-11-15
lang: es            # o en: define el idioma del menú en esa entrada
categories: [R, psicometría]
image: portada.jpg  # opcional
---
```

Cada entrada se escribe en un solo idioma y aparece en el blog en español y en el de inglés.

## Código R o Python

- Los resultados se guardan en `_freeze/` (`execute: freeze: auto`). Renderiza en tu equipo y **sube `_freeze/`**: así GitHub Actions no necesita R ni Python.
- La entrada *Working Memory, Mathematical Anxiety* (2023) se migró con sus resultados originales y tiene `freeze: true`. Para volver a ejecutarla, instala R y los paquetes `pacman`, `broom`, `ggpubr`, `tidyverse`, `readr` y `car`, y cambia a `freeze: auto`.

## Bilingüe

- El menú se define en español en `_quarto.yml`. En las páginas con `lang: en`, `includes/site.html` traduce las etiquetas y ajusta los enlaces.
- Si creas una página nueva con versión en inglés, agrégala al mapa `ES2EN` de `includes/site.html` para que el botón ES/EN lleve a su equivalente.
- La trayectoria de la portada está en un bloque JSON dentro de `index.qmd` y `en/index.qmd`. Al cambiar de puesto, actualiza ambos.

## Publicar en GitHub Pages (una sola vez)

1. Renombra el repositorio a `jorgehmartinez.github.io` (Settings → General → Repository name). Tus otros sitios (`/jb-python-course`, `/Decision-Lab`, `/repositorio_alternativo`, etc.) siguen funcionando.
2. Haz `git push`.
3. En GitHub: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
4. El flujo de la pestaña **Actions** publica el sitio en `https://jorgehmartinez.github.io`.

## Visitas con GoatCounter

El script ya está activo en `includes/head.html` con el código `jorgehmartinez`.
Las visitas se ven en <https://jorgehmartinez.goatcounter.com>. Para usar otro código,
cambia `jorgehmartinez` en ese archivo. GoatCounter no cuenta las visitas desde `localhost`.

## Cambiar el estilo

- Color de acento: `$link-color` y `--accent` en `styles/custom.scss`.
- Colores de la trayectoria: variables `--s-*` en `styles/custom.scss`.
- Tipografía: Inter, cargada desde Google Fonts en `includes/head.html`.
