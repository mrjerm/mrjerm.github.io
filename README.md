# mrjerm.github.io

Personal site for Jeremy Hsu — built with [Quarto](https://quarto.org), served by
GitHub Pages from the `docs/` directory.

## Structure

| File | What it is |
|---|---|
| `_quarto.yml` | Site config: nav, theme, metadata, footer disclaimer |
| `theme.scss` | Custom light theme (typography, layout components) |
| `theme-dark.scss` | Dark-mode palette overrides |
| `index.qmd` | Home — hero, selected work, experience, education, skills |
| `about.qmd` | About page |
| `rime.qmd` | Rime project writeup |
| `fifth-sanctuary.qmd` | Fifth Sanctuary project writeup |
| `robotics.qmd` | FTC #16468 writeup |
| `project_kintoun.ipynb` | Kintoun research notebook (rendered from existing outputs) |
| `resume.pdf` | Linked from the nav and the hero |
| `favicon.svg` | Tab icon |
| `docs/` | **Generated output — do not edit by hand** |

## Working on it

```bash
quarto preview        # live reload
quarto render         # rebuild docs/
```

`execute: enabled: false` is set in `_quarto.yml`, so notebooks render from their
saved outputs and are never re-executed at build time. If you change the code in
`project_kintoun.ipynb`, run the notebook yourself first so the new outputs are
saved, then `quarto render`.

Commit `docs/` — GitHub Pages serves from it.

## Adding a project

Copy `rime.qmd` as a starting point, add it to the `Work` menu in `_quarto.yml`, and
add a card to the `work-grid` block in `index.qmd`.

## Theme components

`.hero`, `.availability`, `.btn-jh` / `.btn-jh-primary`, `.metrics` / `.metric`,
`.work-grid` / `.work-card`, `.xp` / `.xp-item`, `.skills` / `.skill-row` / `.chip`,
`.note-strip`, `table.spec`, `.eyebrow`, `hr.rule`.

Raw HTML blocks are wrapped in `` ```{=html} `` fences so Pandoc passes them through
untouched — keep that pattern when adding new markup, otherwise Pandoc re-parses the
HTML and emits stray elements.
