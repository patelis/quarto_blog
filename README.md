# kpatelis.com

[![Netlify Status](https://api.netlify.com/api/v1/badges/84978100-8670-4c87-9bd7-b0504beb1274/deploy-status)](https://app.netlify.com/sites/silver-tulumba-34ca65/deploys)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Built with Quarto](https://img.shields.io/badge/Built%20with-Quarto-39729E?logo=quarto&logoColor=white)](https://quarto.org/)
[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)](https://github.com/astral-sh/uv)
[![Python 3.13](https://img.shields.io/badge/python-3.13-blue.svg)](https://www.python.org/)

Source for **[www.kpatelis.com](https://www.kpatelis.com/)** — the personal site of [Konstantinos Patelis](https://www.linkedin.com/in/kospatelis/), a Quantitative Analyst based in Zurich working on stress-testing models and GenAI products. The site is built with [Quarto](https://quarto.org/) and deployed to [Netlify](https://www.netlify.com/) on every push to `main`.

## Sections

- **[Home](https://www.kpatelis.com/)** — short about page covering background, focus areas, and contact links.
- **[Portfolio](https://www.kpatelis.com/portfolio.html)** — applied projects, products, and technical deep-dives across data science, ML, and GenAI.
- **[Certifications](https://www.kpatelis.com/certifications.html)** — professional certifications with the skills each one covers and downloadable proof.
- **[Blog](https://www.kpatelis.com/blog.html)** — long-form write-ups and walkthroughs on `tidymodels`, GenAI, and other things worth sharing.

## Run it locally

The project uses [uv](https://docs.astral.sh/uv/) for the Python toolchain (pinned to 3.13.1) and the Quarto CLI for rendering.

```bash
# 1. Clone
git clone https://github.com/patelis/quarto_blog.git
cd quarto_blog

# 2. Install the pinned toolchain (includes the Quarto wrapper)
uv sync

# 3. Live-reload preview at http://localhost:4848
uv run quarto preview

# 4. Or build the static site into _site/
uv run quarto render
```

To add a post or project, drop a new folder under `posts/<slug>/` or `projects/<slug>/` with an `index.qmd` — the listing pages pick it up automatically.

## License

Released under the [MIT License](LICENSE). Site content (posts, images, write-ups) remains © Konstantinos Patelis.
