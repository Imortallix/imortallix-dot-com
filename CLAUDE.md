# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Personal project showcase for Gavin Frings — built with Astro and React islands,
deployed on Cloudflare (Workers Builds / Pages, static output in `dist/`).

## Commands

| Command                 | Action                                              |
| :----------------------- | :--------------------------------------------------- |
| `npm run dev`            | Start local dev server at `localhost:4321`           |
| `npm run build`          | Build the production site to `./dist/`               |
| `npm run preview`        | Preview the production build locally                 |

When starting the dev server, use background mode:

```
astro dev --background
```

Manage the background server with `astro dev stop`, `astro dev status`, and `astro dev logs`.

There is no test suite or linter configured in this repo.

## Architecture

- `src/content.config.ts` — defines the two content collections (`projects`, `notes`)
  and their Zod schemas. This is the source of truth for what frontmatter fields
  are valid/required on content files.
- `src/content/projects/*.md`, `src/content/notes/*.md` — one Markdown file per
  project or post. Adding a project or note is just a new Markdown file with
  frontmatter matching the schema in `content.config.ts` — no other code changes
  needed for it to be routed and rendered.
- `src/pages/projects/[...slug].astro`, `src/pages/notes/[...slug].astro` — dynamic
  routes that statically generate one page per content entry via `getStaticPaths`.
  `src/pages/projects/index.astro` / `notes/index.astro` render the listing pages.
- `src/pages/index.astro` — homepage; pulls `projects` where `featured: true`,
  sorted by `order`.
- `src/layouts/BaseLayout.astro` — shared shell (nav, footer, meta/OG tags). All
  pages wrap their content in this.
- `src/components/ProjectCard.astro`, `Prose.astro` — the only shared components;
  `Prose` wraps rendered Markdown content for typographic styling.
- `public/_headers` — Cloudflare response headers (security headers), served as-is.
- `wrangler.jsonc` — Cloudflare Workers Builds config; serves the static `dist/`
  output with SPA-style 404 handling.

Project frontmatter's `status` field (`demo` | `video` | `writeup` | `in-progress`)
describes how a project is currently *presented* on the site, not literally
whether the underlying project is finished — see the comment in
`content.config.ts`.

## Design direction

`design/homepage-direction.md` documents the settled-on homepage design
direction ("Field Terminal"). Consult it before making homepage layout/visual
changes.

## Documentation

Full documentation: https://docs.astro.build

Consult these guides before working on related tasks:

- [Adding pages, dynamic routes, or middleware](https://docs.astro.build/en/guides/routing/)
- [Working with Astro components](https://docs.astro.build/en/basics/astro-components/)
- [Using React, Vue, Svelte, or other framework components](https://docs.astro.build/en/guides/framework-components/)
- [Adding or managing content](https://docs.astro.build/en/guides/content-collections/)
- [Adding styles or using Tailwind](https://docs.astro.build/en/guides/styling/)
- [Supporting multiple languages](https://docs.astro.build/en/guides/internationalization/)
