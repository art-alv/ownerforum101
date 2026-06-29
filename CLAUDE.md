# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev       # start dev server (localhost:4321)
npm run build     # build to dist/
npm run preview   # preview the build
```

## Project overview

Static site for **Hi-there.net** — a membership resource hub organized by US state and county. Built with Astro 7, no UI framework, no CMS.

Site URL: `https://hi-there.net`

## Page structure

Every page uses `BaseLayout` (Header + Footer wrapping a `<slot />`). Inside that slot, pages compose:

```
SubHeader       — hero banner (title, subtitle, optional background image)
.body-grid      — flex row:
  ContMenu      — left sidebar: state list nav (highlights activeState)
  ContContent   — center main area (accepts title prop + slot for body content)
  ContAdds      — right sidebar: ad placeholders (180px wide)
SubFooter       — strip with a CTA message
```

All pages share this same three-column layout; there is no separate layout variant for the blog vs. static pages.

## Routing

- `/` — home (About / Services / Join sections inside ContContent)
- `/blog` — state selector landing
- `/blog/[state]` — one page per US state, generated via `getStaticPaths()` in `src/pages/blog/[state].astro`
- `/faq`, `/contact`, `/join` — static pages

State slugs are lowercase, spaces replaced with hyphens (e.g. `new-york`). The slug → display name conversion happens inline in `[state].astro` by splitting on `-` and capitalizing each word.

## County drill-down (in progress)

`ContMenuCounty.astro` is a new component (currently Florida counties only) intended to replace `ContMenu` on state pages once a state is selected. CSV files in the repo root (`CAcounties.csv`, `FLcounties.csv`, `GAcounties.csv`, `NYcounties.csv`) and `src/FLcounties.csv` contain county data for future state→county routing. The next routing level will be `/blog/florida/[county]` (see `ScopeState.md`).

## Brand tokens

- Primary accent: `#e94560`
- Dark nav/header background: `#1a1a2e`
- SubHeader background: `#16213e`
- Body background: `#fff`, body text: `#222`
