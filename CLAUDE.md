# CLAUDE.md

Personal portfolio site for **Jeremy Hsu**. Quarto → GitHub Pages, served from `docs/`.
Live at https://mrjerm.github.io

**This repo is public.** Anything committed here is published. See the content policy
below before writing any performance figure into any file.

If an untracked `HANDOFF.md` is present in the repo root, read it first — it carries
the full background on the redesign, the reasoning behind these rules, and the open
questions. It is deliberately gitignored and must stay that way.

## Commands

```bash
quarto preview        # live reload while editing
quarto render         # rebuild docs/ (required before committing)
```

`docs/` is generated output. Never hand-edit files in it. Always `quarto render`
before committing, or the deployed site will lag the source.

## Who this site is for

Recruiters, for **Summer 2027 internships** in three lanes: general SWE, quant dev,
and quant research. Every content decision should be judged against "does this make a
recruiter in one of those three lanes want to interview him."

Jeremy is a Penn State CS sophomore (B.S. Computer Science only — **not** a Statistics
double major; an older version of this site said that and it was wrong. Started
Aug 2025, graduating Dec 2028).

## Content policy — read before touching any performance number

Weaver Capital LP is **Jeremy's own 506(c) fund**, not an employer. That makes this
site's performance claims a compliance question, not just an editorial one.

- **Publish only simulated/backtest figures, and label them as such.** Every metric
  tile and paragraph citing a number must make clear it is a backtest.
- **Do not publish live fund performance**, pending sign-off from whoever handled the
  Reg D filing. This repo is public — the figures must not appear in any tracked file
  (including this one), any rendered page, or `resume.pdf`.
- **`resume.pdf` must be the variant with live figures removed.** Jeremy stripped them
  in Aug 2026 specifically so the site's withholding decision holds end to end. If a
  resume is ever swapped in, check it first — a full version with live performance in
  it silently undoes the whole policy, because the PDF is linked from the nav and
  served at a stable public URL.
- The **footer disclaimer** in `_quarto.yml` is load-bearing. Do not remove or shorten
  it.
- Stating the *fact* of deployment ("live since April 2026") is fine. Stating what it
  earned is not.

If Jeremy says counsel has cleared live figures, that changes — but it takes him
saying so explicitly, not an inference.

## Signal detail is not published either

Separate from the performance question: the strategy pages describe **engineering and
methodology precisely, and signal construction only in general terms.** Jeremy asked
for this directly — the earlier drafts gave away too much of the edge.

- **Safe, and the actual selling point:** the one-decision-function invariant, T+1
  shifting, data-quality gates, the 47 pytest tests, dual-series routing, walk-forward
  folds, block bootstrap, slippage stress. This is what gets an interview. Keep it
  specific.
- **Not published:** the particular state variables and indicators, the named macro
  series, thresholds, and *which* regimes a sleeve is filtered in. Fifth Sanctuary's
  short-sleeve finding is the clearest example — the story that a component was losing
  structurally and got filtered rather than tuned is worth telling; naming the
  conditions is not.
- Each strategy page carries a `.note-strip` saying the specifics are withheld and
  offered in an interview. That framing is deliberate — it reads as discretion rather
  than vagueness. Keep it if you rewrite these pages.

**`resume.pdf` still enumerates all of it** — the regime tree and its indicators, the
named macro series, and the filtered regimes — and it is linked from the nav at a
stable public URL. Same end-to-end hole the live figures had. Until the PDF is
updated, the site's restraint is undone one click away.

## Editorial voice

The site deliberately publishes numbers that cut against the strategies, because that
is what reads as credible to a quant audience:

- Rime's page shows Sharpe 1.58 excluding 2020 next to the headline 1.86, and explains
  that the gap *is* the finding.
- Fifth Sanctuary's page states plainly that a 42% win rate means it is wrong more
  often than it is right.

Keep that. Do not "improve" these pages by removing the unflattering framing — it is
the point. Project writeups lead with engineering (the one-decision-function
invariant, T+1 shifting for lookahead safety, the 47 pytest tests, dual-series
routing), not with returns.

## Structure

| File | What it is |
|---|---|
| `_quarto.yml` | Nav, theme wiring, OG/Twitter meta, footer disclaimer |
| `theme.scss` | Custom light theme — typography, all layout components |
| `theme-dark.scss` | Dark palette overrides only (light theme defines structure) |
| `index.qmd` | Home: hero, metrics, work grid, experience, education, skills |
| `about.qmd` | About |
| `rime.qmd` | Rime — daily ETF regime allocator (live) |
| `fifth-sanctuary.qmd` | Fifth Sanctuary — intraday gold vol expansion (live) |
| `robotics.qmd` | FTC #16468 Green Lemons Robotics |
| `project_kintoun.ipynb` | Kintoun ORB research notebook |
| `resume.pdf` | Linked from nav and hero |
| `favicon.svg` | Tab icon |
| `docs/` | **Generated. Do not edit.** |

Ordering on the home page is intentional: deployed strategies first, Kintoun (research,
not on the resume) third, robotics fourth. An earlier version featured Kintoun and
omitted the deployed work; that inversion was the main thing the redesign fixed.

## Conventions and gotchas

**Raw HTML must be fenced.** Every raw HTML block is wrapped in ` ```{=html} ` fences.
Without them Pandoc re-parses the HTML, and block-level constructs containing inline
elements (an `<a>` wrapping `<div>`s, as in the work cards) emit stray empty elements
into the output. If you add markup, fence it.

**`.md` files are not pages.** `_quarto.yml` sets an explicit `render:` scope of
`*.qmd` and `*.ipynb`. Without it Quarto renders every `.md` in the project root into
`docs/` — that published `CLAUDE.md` as a public page. Do not widen the render scope.

**Notebooks are never executed at build time.** `execute: enabled: false` in
`_quarto.yml`. Notebooks render from their saved outputs. If notebook code changes, run
the notebook manually so outputs are saved, then `quarto render`.

**Theme components** available in `theme.scss`: `.hero`, `.availability`, `.btn-jh` /
`.btn-jh-primary`, `.metrics` / `.metric` (`.metric-value`, `.metric-label`,
`.metric-note`), `.work-grid` / `.work-card` (`.work-status`, `.work-title`,
`.work-meta`, `.work-more`), `.xp` / `.xp-item` (`.xp-when`, `.xp-body`, `.xp-role`,
`.xp-org`), `.skills` / `.skill-row` / `.chips` / `.chip`, `.note-strip`,
`table.spec`, `.eyebrow`, `.lede`, `hr.rule`, and `.related` / `.related-label` /
`.related-link` (`.related-title`, `.related-note`, `.related-arrow`) for the
end-of-page "next" rail on project pages.

**Sections are numbered by CSS counters, not by hand.** `main.content h2` carries an
`01`, `02`, … prefix, mirrored in the TOC. Two consequences:

- **Never type a number into a heading.** The Kintoun notebook used to carry literal
  `## **1. Hypothesis**` prefixes; they had to be stripped when numbering landed, or
  every heading would have been numbered twice. Its headings were also wrapped in
  `**bold**`, which forces weight 700 inside an `h2` the theme deliberately sets to
  400 — don't reintroduce that either.
- The counter is scoped to `main.content`, which does *not* contain the TOC (that
  lives in `#quarto-margin-sidebar`), so the sidebar is numbered by its own counter.

**The rendered `description` in the title block is hidden.** Quarto prints the
front-matter `description` under the subtitle *and* emits it into `<head>` as
`meta name="description"` / `og:description`. On screen it just restated the subtitle,
so only the rendered copy is hidden — the head tags are untouched and OG still works.

Colors are CSS custom properties (`--jh-ink`, `--jh-paper`, `--jh-surface`,
`--jh-surface-2`, `--jh-muted`, `--jh-hairline`, `--jh-accent`, `--jh-accent-soft`)
defined in both theme files. Use those rather than hardcoding hex values, or dark mode
breaks.

**Design language is Palantir's.** Keep edits inside it rather than drifting back to a
generic Bootstrap look:

- One grotesque family — Inter Tight for display, Inter for text. **No serif anywhere.**
  These stand in for Palantir's proprietary Alliance No.2 / No.1.
- Hierarchy comes from **size and tracking, not weight.** Display type sits at 400–500
  and never 700; large type gets tight negative tracking (down to `-0.045em`), small
  caps get positive tracking (`+0.14em`).
- `border-radius: 0` essentially everywhere. The Bootstrap radius variables are zeroed
  in `scss:defaults` and Quarto's own components are overridden in `scss:rules`.
- Hairlines carry structure; shadows are tight hard rings, never soft glows.
- **Monochrome. There is no hue anywhere, and none should be added.** An audit of
  palantir.com across 1,535 elements finds exactly one designed text colour (`#1e2124`),
  white, and a grey ramp — the only chromatic values on the page are the browser's
  default unstyled-link blue and an error red. Their colour comes from photography,
  which this site does not have. `--jh-accent` is deliberately set equal to `--jh-ink`
  in both theme files; the token exists so components have one name for "emphasis", not
  so it can carry a colour.
- **Interaction is expressed by inversion, not colour.** Hovering a work card, button,
  or chip swaps ink and paper. Because the hovers are written purely as
  `var(--jh-ink)` / `var(--jh-paper)` swaps, they invert correctly in dark mode with no
  per-component overrides — keep them that way.
- Status is encoded by *mark*, not colour: live work gets a filled square before the
  label, archived work an outlined one.
- Since links cannot be signalled by colour, inline links in `main.content` are always
  underlined. Do not remove that underline.

Note: do **not** reach for Blueprint here. It is Palantir's *product* design system and
is much bluer; the marketing site's language is the monochrome one above. An earlier
pass used Blueprint's palette and it read wrong.

Two specificity traps in the inversion hovers, both already handled — preserve them if
you touch `.work-card`:

- `.work-status.is-archive` ties `.work-card:hover .work-status` at (0,3,0) and wins on
  source order, so the hover block restates `.is-archive` explicitly. Without it the
  grey status text is stranded on the inverted background at ~1.6:1.
- Secondary text inside a hovered card is dimmed with `opacity`, not a second colour
  token, so it composites correctly over either ink or paper.

**Code block backgrounds need `$code-block-bg`, set per theme layer.** It is a separate
Quarto variable from Bootstrap's inline `$code-bg`. Left unset it falls back to a fixed
light grey, which renders near-white-on-light-grey — invisible — in dark mode.

**Do not use `<h3>` inside a work card** — use `.work-title`. Quarto's section-div
processing restructures headings found inside raw blocks.

**`h2` carries no rule, and `border-bottom: 0` must be stated explicitly.** Quarto's
own bootstrap layer sets `h2 { border-bottom: 1px; padding-bottom: .5rem }`, so simply
omitting the property from `theme.scss` leaves Quarto's rule in place — it has to be
zeroed. The reason it is zeroed: every section on the home page opens with a component
that already has a top hairline (`.work-grid`, `.awards`, the first `.xp-item` /
`.skill-row`), so a heading rule stacked a second line 34px below the first at every
boundary. With `hr.rule` above the heading too, section boundaries were showing four
parallel rules inside ~150px. Sections are now separated by the heading's top margin
and the counter prefix. `hr.rule` still exists as a component but is no longer used;
adding it back between sections reintroduces the doubling.

**Stop `quarto preview` before `quarto render`.** Both write into `docs/`. Running a
render while a preview server is up races it, and the render can silently leave stale
HTML on disk — a page's source was correct, the render reported success, and the
committed output still had the old markup. If output looks stale, stop the preview and
render again.

**New components with an `<a>` root must be added to the inline-link exclusion list.**
`main.content a:not(...)` underlines inline links (required, since a monochrome palette
cannot signal a link by colour). Any block/card affordance whose root element is an
anchor — `.btn-jh`, `.work-card`, `.chip`, `.related-link` — has to be excluded there or
it inherits the underline through its whole body.

**Quarto appends `caption-top table` to `table.spec`.** That pulls in Bootstrap's table
rules, two of which fight the component: `.table > :not(:first-child)` adds a 2px border
above `<tbody>` (a doubled hairline under the heading) and the striping shim paints a
background over the cells. Both are neutralised in `theme.scss`; keep those overrides if
you touch the spec table.

## Adding a project

1. Copy `rime.qmd` as the template.
2. Add it to the `Work` menu in `_quarto.yml`.
3. Add a `.work-card` to the `work-grid` block in `index.qmd` (inside the html fence).
4. `quarto render`, check both light and dark, commit `docs/`.

## Open items

- **Resume variants.** The "quant" and "engineering" PDFs Jeremy has are byte-identical.
  A genuinely engineering-flavored variant does not exist yet; the current site is
  built against the quant one.
- **GitHub is not presentable.** The site links to github.com/mrjerm. Kintoun should be
  a public repo with a real README before a recruiter clicks through.
- **No headshot.** The hero is text-only by design and works without one.
- **Custom domain** deferred; on `mrjerm.github.io` for now. Adding one means a `CNAME`
  file plus DNS records, and `site-url` in `_quarto.yml` must be updated to match or
  the OG tags will point at the wrong host.
- IMC Prosperity is listed as "Top 100 US, qualifiers" — that is accurate and
  deliberately not inflated. He did not place well in the round proper.
