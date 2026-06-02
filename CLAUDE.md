# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

French-language tabletop RPG (jeu de rôle) campaign book built with [mdBook](https://rust-lang.github.io/mdBook/). Content is Markdown under `src/`; the rendered static site is committed under `docs/` for GitHub Pages hosting (repo: `remifabas/jdr`).

## Commands

```bash
make build   # mdbook build -d docs .   (outputs to ./docs)
make serve   # mdbook serve -d docs --open  (live reload on localhost)
```

Both commands require `mdbook`, `mdbook-admonish`, and `mdbook-catppuccin` on `PATH`. The build output dir `docs/` is intentionally committed (not gitignored) — `.gitignore` only excludes `book/` (the default mdBook output).

## Architecture

- `book.toml` — mdBook config. Two preprocessors: `admonish` (callout boxes) and `catppuccin` (theme). Custom CSS in `theme/` + `mdbook-admonish.css` at root. Default light theme `latte`, dark `frappe`.
- `src/SUMMARY.md` — table of contents. **Every new chapter must be linked here** or mdBook ignores the file.
- `src/` layout mirrors in-fiction structure, not technical concerns:
  - `game/` — rules, character creation, alignment
  - `univers/` — world / setting (Magtherai Isle, Mordheim)
  - `pj/` — player characters (PJ = personnage joueur) + `patron.md` (patron/sponsor mechanic)
  - `pnj/` — non-player characters
  - `story/` — campaign arcs split by act (`1_act.md` + `act1/N_chap.md`)
- `theme/index.hbs` — custom Handlebars template overriding mdBook default.

## Conventions

- Content is **French**. Match existing tone and vocabulary (PJ, PNJ, patron, alignement, etc.) when editing.
- Commit prefixes used so far: `feat(story:act-X)`, `feat`, `fix` — keep this style.
- Story chapters follow the pattern `src/story/actN/M_chap.md` and are referenced from `SUMMARY.md` with the `Chapitre M` label.
- Run `make build` before committing structural changes so the committed `docs/` stays in sync with `src/`.
