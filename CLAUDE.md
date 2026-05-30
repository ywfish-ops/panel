# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this project is

`ywfish-ops/panel` is a personal investment-decision panel: a **single static
`index.html`** with no build step, no dependencies, and no backend. It is
served by **Cloudflare Pages**, which auto-deploys on every push to `main` —
pushing to `main` is what publishes the site.

> **Current repo state:** as of this writing the repository contains only
> `README.md` and this `CLAUDE.md`. `index.html` is not committed yet. The
> conventions below describe how `index.html` is structured and maintained;
> follow them once the file is present, and delete this note when it lands.

## Division of responsibility

Data analysis and judgment (stock prices, market reads, verdicts) come from
**claude.ai**, not from Code. Claude Code's job is **only** to land the given
new data into the page as code changes and push it. **Never invent or estimate
stock prices, quotes, or market judgments** — only transcribe the values you
are explicitly given.

## Update workflow

The single source of truth for mutable data is the **数据区 / DATA BLOCK**
comment at the **top of `index.html`**. To make an update:

1. Edit the DATA BLOCK comment first to record the new data.
2. Then sync the corresponding spots further down the page to match.
3. Commit and push directly to `main`; Cloudflare Pages deploys automatically.

### Where each piece lives in `index.html`

- **Holdings table** — `class="resp-table"`; one row per instrument.
- **Waiting list** (等待清单) — `.card` elements under the **当前等待清单** heading.
- **Thermometer / verdict** — status text in `.verdict-status`; the fill height
  is driven by `thermo-fill` in the JavaScript at the bottom of the file.

## Hard constraints

- Keep it a **single, pure-static file**. Do not introduce external
  dependencies, frameworks, or a build system.
- **Do not change** styling, layout, fonts, or color scheme — only data.

## Git workflow

- Default branch: `main`; pushing to `main` triggers the Cloudflare Pages
  deploy.
- Active development branch for this scaffolding work: `claude/claude-md-docs-p3TPx`.
- Do not open pull requests unless explicitly asked.
