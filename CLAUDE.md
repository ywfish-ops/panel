# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this project is

`ywfish-ops/panel` is a personal AI-investment decision panel (个人 AI 决策面板):
a **single static `index.html`** with no build step, no dependencies, and no
backend. All CSS and JS are inline in that one file. It is served by
**Cloudflare Pages**, which auto-deploys on every push to `main` — pushing to
`main` is what publishes the site.

The page is four tabs of the same workflow: 🌡️ 温度计 (thermometer / theme
on-off switch) → 🔻 漏斗 (the 6-sieve screening funnel + scorecard) → ✅ 结果
(funnel output table + waiting list) → 🗺️ 产业链 (candidate-pool chip map).
Tab switching and the thermometer fill are the only JS, at the bottom of the file.

## Division of responsibility

Data analysis and judgment (stock prices, market reads, verdicts, stage calls)
come from **claude.ai**, not from Code. Claude Code's job is **only** to land the
given new data into the page as code changes and push it. **Never invent or
estimate stock prices, quotes, stages, or market judgments** — only transcribe
the values you are explicitly given.

## Update workflow

The single source of truth for mutable data is the **数据区 / DATA BLOCK** HTML
comment at the **very top of `index.html`** (the `<!-- ... -->` block before
`<html>`). To make an update:

1. Edit the DATA BLOCK comment first to record the new data and the update date.
2. Then sync every corresponding spot further down the page to match (a single
   value often appears in several places — see below).
3. Commit and push directly to `main`; Cloudflare Pages deploys automatically.

### Where each piece lives in `index.html`

- **Update date** appears in **three** spots that must stay in sync: the DATA
  BLOCK header, the header `.updated` line, and the `<footer>`.
- **Thermometer / verdict** (温度计 tab): the percentage is set in **two** places
  — the DATA BLOCK note and the JS at the bottom (`getElementById('fill').style.height='88%'`,
  the element has `class="thermo-fill"`). The status label is the `.verdict-status`
  text (e.g. 加速期 / ACCELERATING) and is also described in the `.verdict-body`
  paragraph and the `.scale` legend.
- **Capex / validation / sentiment cards** (温度计 tab): the `.card` blocks inside
  the three `.layer` sections (01 需求源头 / 02 中转验证 / 03 泡沫情绪).
- **Screening-result table** (结果 tab): `class="resp-table"`, one `<tr>` per
  instrument. On narrow screens columns 2/3/5/7 are hidden via CSS — keep the
  full 8 columns populated regardless.
- **Waiting list** (当前等待清单 heading in the 结果 tab): the `.card` elements in
  the `.grid-3` immediately below that `.section-rule`.
- **Industry-chain pool** (产业链 tab): `.chip` elements grouped by `.chain-sec`;
  classes `pick` / `hot` / `watch` color them (precision/上游, 过热慎追, 纯监控).

## Hard constraints

- Keep it a **single, pure-static file**. Do not introduce external
  dependencies (the Google Fonts `<link>` is the only remote asset — do not add
  more), frameworks, or a build system.
- **Do not change** styling, layout, fonts, color scheme, or the dark-mode
  lock-ins — only data.

## Git workflow

- Default branch: `main`; pushing to `main` triggers the Cloudflare Pages deploy.
- Active development branch for this scaffolding/docs work: `claude/claude-md-docs-p3TPx`.
- Do not open pull requests unless explicitly asked.
