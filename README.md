# kpatelis.com

[![Netlify Status](https://api.netlify.com/api/v1/badges/84978100-8670-4c87-9bd7-b0504beb1274/deploy-status)](https://app.netlify.com/sites/silver-tulumba-34ca65/deploys)

Source for **[www.kpatelis.com](https://www.kpatelis.com/)** — the personal site of [Konstantinos Patelis](https://www.linkedin.com/in/kospatelis/), a Quantitative Analyst at UBS working on Combined Stress Testing models and GenAI products (LangGraph + Azure OpenAI). The site collects long-form technical write-ups and applied data-science projects across machine learning, `tidymodels`, GenAI, and data products in finance.

## What's on the site

- **About** — background, focus areas, contact: [/](https://www.kpatelis.com/)
- **Blog** — long-form posts: [/blog.html](https://www.kpatelis.com/blog.html)
- **Portfolio** — applied projects: [/portfolio.html](https://www.kpatelis.com/portfolio.html)
- **Certifications** — professional certifications, skills covered, and downloadable proof: [/certifications.html](https://www.kpatelis.com/certifications.html)

Most recent post: [*Classification modeling workflow using tidymodels*](https://www.kpatelis.com/posts/classification-modeling-workflow-using-tidymodels/) — end-to-end pipeline with `workflowsets`, parallel hyperparameter tuning via `future`, and a multinomial ensemble via `stacks`.

## How it's built

| Layer | Choice |
|---|---|
| Content | [Quarto](https://quarto.org/) literate documents (`.qmd` — prose + executable R / Python) |
| Compute | `knitr` with committed `_freeze/` snapshots, so long-running fits stay reproducible across deploys without needing R in CI |
| Comments | [giscus](https://giscus.app/) on top of GitHub Discussions |
| Theme | Quarto `cosmo` / `darkly` with theme-aware code blocks via custom `styles.css` |
| Certifications | Custom Quarto listing template (`_templates/certification-card.ejs`) renders skill chips on each card. See [`certifications/README.md`](certifications/README.md) |
| Search & feed | Built-in Quarto overlay search + full-text RSS at `/blog.xml` |
| Hosting | [Netlify](https://www.netlify.com/) — auto-deploys on push to `main` |
| CI | GitHub Actions → `quarto-dev/quarto-actions/publish@v2` (single workflow file) |
| Toolchain | [uv](https://docs.astral.sh/uv/) pinning Python 3.13.1 plus the Quarto CLI |

## Run locally

```bash
uv sync                  # install pinned toolchain
uv run quarto preview    # live-reload dev server
uv run quarto render     # build _site/
```

- **Prose-only edit** → `quarto render` reuses the frozen snapshot, no R needed.
- **Code edit** → render the specific post (`quarto render posts/<slug>/index.qmd`), then commit both the `.qmd` and the refreshed `_freeze/posts/<slug>/`.

## Repo layout

```
.
├── _quarto.yml          # site config (navbar, theme, search, feed, resources)
├── index.qmd            # about / landing
├── blog.qmd             # blog listing — auto-discovers posts/
├── portfolio.qmd        # portfolio listing — auto-discovers projects/
├── certifications.qmd   # certifications listing — auto-discovers certifications/
├── 404.qmd              # branded not-found page
├── posts/               # one folder per post
├── projects/            # one folder per project
├── certifications/      # one folder per cert — see certifications/README.md
├── documents/           # static PDFs (certificate proofs); copied to _site/ via resources:
├── _templates/          # custom Quarto listing templates (.ejs partials)
├── _freeze/             # committed compute snapshots (required for CI)
├── styles.css           # site-wide overrides
└── .github/workflows/   # Quarto → Netlify publish workflow
```

## Contact

- LinkedIn — [in/kospatelis](https://www.linkedin.com/in/kospatelis/)
- Email — [kpatelis@outlook.com](mailto:kpatelis@outlook.com)
- GitHub — [@patelis](https://github.com/patelis)
