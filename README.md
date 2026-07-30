# imortallix.com

Personal project showcase for Gavin Frings — built with [Astro](https://astro.build)
and React islands, deployed on Cloudflare Pages.

## Structure

```
src/
  content.config.ts        content collection schemas (projects, notes)
  content/
    projects/               one .md per project
    notes/                  one .md per post
  layouts/BaseLayout.astro  shared nav/footer/meta
  components/                ProjectCard, Prose
  pages/                     index, /projects, /notes, dynamic routes, 404
public/_headers             Cloudflare Pages response headers
```

Adding a project or a note is one Markdown file in `src/content/` — no other
code changes needed.

## Commands

| Command           | Action                                      |
| :----------------- | :------------------------------------------- |
| `npm install`       | Install dependencies                          |
| `npm run dev`       | Start local dev server at `localhost:4321`    |
| `npm run build`     | Build the production site to `./dist/`        |
| `npm run preview`   | Preview the production build locally          |

## Deploy

Pushes to `main` auto-deploy via Cloudflare Pages (build command `npm run build`,
output directory `dist`).
