# Certifications

This folder backs the `/certifications` page on the site. Each subfolder is one certification; the listing page at the root (`certifications.qmd`) auto-discovers them, sorts by `date desc`, and renders each as a card via a **custom Quarto listing template**.

## Why this is a custom solution (and not a Quarto extension)

Quarto's stock grid listing template only renders a fixed set of fields (title, image, date, categories, description). To surface a row of **skill chips** on each card without overloading `categories` (which doubles as the filter UI), we need a custom `.ejs` template that reads an arbitrary `skills:` frontmatter field. This is the mechanism documented at <https://quarto.org/docs/websites/website-listings-custom.html>.


## How the moving parts fit together

| File | Role |
|---|---|
| `../certifications.qmd` | Listing page in the navbar. Points `listing.template:` at the EJS partial below. |
| `../_templates/certification-card.ejs` | Custom card markup. Reads standard fields plus the custom `skills:` and `issuer:` from each cert's frontmatter. |
| `./<slug>/index.qmd` | One per certification — frontmatter drives the card, body drives the detail page. |
| `./<slug>/badge.png` | The badge image (the `image:` field). Used as the card thumbnail. |
| `../documents/<slug>.pdf` | The downloadable certificate PDF. Linked from the detail page. The top-level `documents/` folder is declared under `project.resources` in `_quarto.yml` so it is copied into `_site/` on render. |
| `../styles.css` | Holds `.skill-chip`, `.certification-skills`, and `.certification-badge` rules. Reuses existing CSS variables for dark/light theme support. |

## Adding a new certification

1. Create a folder `certifications/<slug>/` (kebab-case slug, e.g. `aws-saa-associate`).
2. Drop the badge image at `certifications/<slug>/badge.png` (PNG or JPG, transparent background looks best).
3. Drop the certificate PDF at `documents/<slug>.pdf`.
4. Create `certifications/<slug>/index.qmd` with this frontmatter:

   ```yaml
   ---
   title: "AWS Certified Solutions Architect — Associate"
   issuer: "Amazon Web Services"
   date: "2024-08-15"
   image: "badge.png"
   categories: [cloud, aws]
   skills: ["EC2", "VPC", "IAM", "S3", "High Availability"]
   pdf: "/documents/aws-saa-associate.pdf"
   verify-url: "https://www.credly.com/badges/..."   # optional
   ---
   ```

   And a body roughly like:

   ```markdown
   [Download certificate (PDF)](/documents/aws-saa-associate.pdf){.btn .btn-primary}
   [Verify on Credly](https://www.credly.com/badges/...)

   ## Skills covered

   - EC2, VPC, IAM, S3
   - Designing resilient, high-availability architectures

   ## Issued

   Amazon Web Services — 2024-08-15
   ```

5. Run `uv run quarto preview` and confirm the card appears with the badge, issuer, date, **skill chips**, and broad category pills.

## Field conventions

- **`title`** — the certification's official name.
- **`issuer`** — issuing organization (custom field; rendered as the card subtitle).
- **`date`** — ISO date (`YYYY-MM-DD`). Drives the `date desc` sort on the listing.
- **`image`** — relative path to the badge image inside this cert's folder.
- **`categories`** — **broad** facets only (e.g. `cloud`, `aws`, `ml`). These render as filter pills under the listing's search bar.
- **`skills`** — fine-grained list. Rendered only on the card as chips by the custom EJS template. Keep these short and concrete (single tokens like `S3`, `VPC`, `MLOps`). These do **not** appear in the filter UI.
- **`pdf`** — root-relative URL to the certificate PDF in `/documents/`.
- **`verify-url`** — optional external link to the digital badge / verifier (Credly, Microsoft Learn, etc.).

## Why `skills` and `categories` are separate

`categories` is wired up to Quarto's listing filter UI: each unique value becomes a clickable filter pill above the grid. If we put fine-grained skills (e.g. 6–8 per cert × N certs) into `categories`, the filter row balloons into dozens of pills and the page becomes noisy. Keeping `categories` broad and `skills` separate keeps the filter usable while still surfacing the substance on each card.
