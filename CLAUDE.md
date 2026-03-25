# CLAUDE.md

This file provides guidance when working with this repository.

## What This Is

A plain static site deployed to GitHub Pages.

## Common Commands

```bash
# Preview locally
python3 -m http.server 8000
```

## Site Structure

- `index.html` contains the page markup.
- `styles.css` contains the styling.
- `CNAME` preserves the custom domain for GitHub Pages.

## Deployment

Hosted on GitHub Pages with a custom domain (`triathenum.com`). Deployment is automatic on push to `main` via `.github/workflows/deploy.yml`. The workflow uploads the repository root directly as the Pages artifact and deploys it using the official GitHub Pages Actions.

Before the custom domain works, GitHub repo settings → Pages must have the custom domain set, and DNS must have A records pointing to GitHub's servers (`185.199.108-111.153`).
