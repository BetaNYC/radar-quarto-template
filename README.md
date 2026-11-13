# RADAR Report

A [Quarto](https://quarto.org) report template for BetaNYC's Research and Data Assistance Request (RADAR) service published using GitHub Pages.

## What's changed

[`WHATS-CHANGED.md`](WHATS-CHANGED.md) lists the changes a reader would notice, newest first, including any correction to a published number. The site shows it at [https://betanyc.github.io/radar-quarto-template/whats-changed.html](https://betanyc.github.io/radar-quarto-template/whats-changed.html).

- `_quarto.yml` builds `whats-changed.qmd` from it before every render (`pre-render`). Edit `WHATS-CHANGED.md`, never `whats-changed.qmd`. `scripts/whats_changed.py` is a copy of BetaNYC's shared script: do not edit it here.
- Never rewrite a published entry. Add a dated `- **Update YYYY-MM-DD:**` line instead. The `What's changed` workflow checks this on every pull request.
- The footer link to the page lives in `radar-footer.html`. Pages rendered before it was added (everything except the What's changed page itself) show the link only after their next full `quarto render`.
- A new entry is dated the day it goes live. If the pull request that adds one merges on a later day, its last commit before merge changes the date to the merge day and re-renders the page (`quarto render whats-changed.qmd`).
- **Starting a new report from this template?** Replace the entries in `WHATS-CHANGED.md` with one for your report's first publication, set **History begins** and the intro for your report, and change `--repo-url` in the `pre-render` line of `_quarto.yml` to your report's repository. The workflow in `.github/workflows/whats-changed.yml` needs no change. If you make that switch in a pull request, add a line `Whats-changed-edit: new report from the template` to its commit message, because the check otherwise refuses removed entries.

## Requirements

- [R](https://cran.r-project.org) and [Quarto](https://quarto.org/docs/get-started/)
- [Docker](https://www.docker.com/products/docker-desktop/), only if the report uses the PostGIS database in `compose.yaml`

The setup chunk in `index.qmd` installs any missing R packages.

## Setup

Copy `.Renviron.example` to `.Renviron` and fill in any credentials the report uses. `.Renviron` is gitignored.

## Render

```sh
quarto render
```

This writes the site to `docs/`. Commit `docs/` along with your changes.

## Publish

In the repo's **Settings → Pages**, deploy from the `main` branch, `/docs` folder.

## Files

| Path | Purpose |
|---|---|
| `index.qmd` | The report |
| `_quarto.yml` | Site and format options |
| `cil_table.R` | `cil_table()`, for tables in the CIL style |
| `style/`, `fonts/`, `images/` | Theme, typefaces, logos |
| `radar-header.html`, `radar-footer.html` | Page header and footer. Update the source code link in the footer for each report. |

## License

All original content is Copyright, Creative Commons 4.0 Attribution-ShareAlike.
