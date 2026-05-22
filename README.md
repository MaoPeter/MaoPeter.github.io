# Personal website

Source for [maopeter.github.io](https://maopeter.github.io), built with [Quarto](https://quarto.org).

## Working locally

```sh
quarto preview      # live-reloading dev server
quarto render       # one-shot build into _site/
```

## How it's deployed

On every push to `main`, the workflow at `.github/workflows/publish.yml`:

1. Installs Quarto and Python on a GitHub-hosted runner.
2. Runs `quarto render`, reusing cached computational output from `_freeze/`.
3. Publishes the rendered `_site/` to the `gh-pages` branch.

GitHub Pages serves whatever is on `gh-pages`.

## Computational content

Cells with `{python}` / `{r}` etc. are executed at render time. To avoid the cost (and fragility) of installing Sage in CI:

- Set `execute: freeze: auto` in `_quarto.yml` (already done).
- Render locally in a Sage-aware Python environment.
- Commit the resulting `_freeze/` directory.

CI then reuses the frozen output instead of re-executing.

## Publications

Edit `publications.bib`. Entries appear automatically on the [Research](research.qmd) page via `nocite: "@*"`.

## First-time GitHub Pages setup

After the first push and successful workflow run:

1. Repository → Settings → Pages.
2. Source: **Deploy from a branch**.
3. Branch: **`gh-pages` / (root)**. Save.
