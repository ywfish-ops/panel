# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Current state

This repository (`ywfish-ops/panel`) is currently an empty scaffold. As of this writing it contains only:

- `README.md` — a single-line title (`# panel`)
- This `CLAUDE.md`

There is no application code, build system, dependency manifest, test suite, or CI configuration yet. There are also no other AI-assistant rule files (`.cursor/rules/`, `.cursorrules`, `.github/copilot-instructions.md`).

## Guidance for future instances

Because the project has no established structure yet, the early decisions you make will set its conventions. When the first real code lands:

- **Update this file.** Replace this section with the actual build, lint, test, and run commands (including how to run a single test), and document the high-level architecture once it spans more than one file.
- **Establish conventions deliberately** — the choice of language, package manager, directory layout, and formatting/linting tooling has no precedent here, so pick deliberately and document it.
- Do not invent commands or structure that don't exist; keep this file in sync with what is actually in the repo.

## Git workflow

- Default branch: `main`.
- Active development branch for this work: `claude/claude-md-docs-p3TPx`.
- Push with `git push -u origin <branch-name>`; do not open pull requests unless explicitly asked.
