# Homepage direction (exploration notes)

Design exploration for the homepage, done as artifact mockups (not yet built
into the site). Captured here so the decision survives past the chat session.

## Content scope

Only **OFM Bot** ships as a visible project for now. `Lazer77`,
`Oath Analysis`, and `Glorious Madness Analysis` stay in
`src/content/projects/` as scaffolding but are not meant to be linked from
the homepage or treated as featured yet.

The homepage should read as a general personal hub, not a single-project
landing page — there will eventually be a page for games Gavin plays and a
way of grouping projects by theme. Until then, the homepage should leave
visible room for those ("coming soon" style slots), not pretend they don't
exist.

## Settled direction: "Field Terminal — Unified Console"

Landed here after iterating through several directions (a dark dashboard, a
field-notebook/editorial style, a bold poster, and an arcade select screen)
and then hybridizing the dashboard and arcade directions. This variant kept
the arcade select-screen's layout skeleton but restyled it in the
dashboard's quieter, flatter mood, then merged its separate panels into one
bordered console frame.

**Concept.** The homepage frames OFM Bot as a two-player "select screen"
where P1 and P2 are *the same bot* — because it trains via self-play, not
by facing an opponent. Both slots use the identical accent color on
purpose (no red/blue rivalry coloring) to reinforce that it's one network
against its own last generation, not two competing things.

**Layout.** One continuous bordered "console" frame, not floating separate
cards:
- Row 1: P1 / VS / P2 slots (three-column grid, dividers via borders)
- Row 2: project brief — description, tech tags, repo link
- Row 3: two-up "roster" grid for the not-yet-built sections (Games I
  play, Project groups), styled as locked slots, plus Notes marked live

Top nav is a slim "marquee" bar (brand + Projects/Notes links). Everything
sits inside one `max-width` column, left/console-bordered rather than
scattered.

**Mood / palette.** Dark, quiet, monospace — no neon glow or CRT scanline
effects (those belong to the more playful arcade variants that were
explored but not chosen). Single accent color used sparingly (status
blips, links). Baseline palette from the mockup:
- `--bg: #0a0d12`, `--panel: #10151d`, `--panel-2: #0d1219`
- `--line: #232b38`
- `--text: #dfe6ee`, `--text-dim: #7c8a9c`, `--text-faint: #4b5766`
- `--accent: #8c6cff` (violet — swappable; a warm copper variant and a
  near-monochrome variant were also mocked up and are worth a look before
  committing)

**Texture.** A faint graph-paper/blueprint grid in the background
(`repeating-linear-gradient`, ~32px cells, accent color at very low
alpha) — this was the one thing pulled forward from an earlier
newsletter-inspired pass and is worth keeping regardless of which color
variant is picked.

**Type.** Display/headings in **Martian Mono** (800), body and data in
**IBM Plex Mono** (400/600). Both self-hosted as `@font-face` (Google
Fonts CSP-blocks in the artifact tool, but for the real site these can be
pulled in normally via `@fontsource` or local files).

**Not yet decided:** final accent color (violet vs. the warm/copper
variant vs. near-monochrome), and whether the left-aligned two-column
"split" reflow is worth adopting over the centered version.

## Status

Not implemented. `src/pages/index.astro` is still the original scaffold
(featured-project grid pulling from the content collection). Next step,
whenever picked back up, is to build this into `index.astro` +
`BaseLayout.astro`/`global.css` as real site tokens, and decide how (or
whether) to route `/projects` and `/notes` given the narrower homepage
scope.
