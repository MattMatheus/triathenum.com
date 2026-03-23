# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A [Hugo](https://gohugo.io/) static site using the [Congo theme](https://jpanther.github.io/congo/) (tracked as a git submodule at `themes/congo` from the `stable` branch).

## Common Commands

```bash
# Start local dev server with drafts visible
hugo server -D

# Build the site to ./public/
hugo

# Create a new content file using the archetype
hugo new content/posts/my-new-post.md
```

## Configuration Architecture

Hugo config is split across two locations:

- `hugo.toml` — root config, contains only `baseURL`
- `config/_default/` — all real site config:
  - `hugo.toml` — theme, pagination, output formats, privacy settings
  - `params.toml` — all Congo theme parameters (color scheme, layout, feature flags)
  - `languages.en.toml` — site title, author info, section definitions
  - `menus.en.toml` — main nav menus
  - `markup.toml`, `module.toml`, `taxonomies.toml` — supporting config

When modifying site behavior, edit files in `config/_default/` rather than the root `hugo.toml`.

## Theme Customization

The Congo theme lives in `themes/congo/` as a git submodule. **Do not edit files inside `themes/congo/`** — override them instead by creating matching files in the root of this repo (Hugo's file precedence means root files take priority over theme files). For example:

- Override a layout: create `layouts/partials/my-partial.html`
- Override theme CSS: create `assets/css/custom.css`
- The homepage uses `layout = "profile"` (`config/_default/params.toml`)
- `layouts/_partials/functions/warnings.html` is overridden to patch a Congo incompatibility with Hugo 0.158 (`.Site.Author` field was removed)

## Content

Content goes in `content/`. The default archetype (`archetypes/default.md`) sets `draft = true`, so new content won't appear in production builds until `draft` is removed or set to `false`.

The `mainSections` in `config/_default/languages.en.toml` controls which content sections appear on the homepage recent list (set to `["posts"]`).

## Deployment

Hosted on GitHub Pages with a custom domain (`triathenum.com`). Deployment is automatic on push to `main` via `.github/workflows/deploy.yml`. The workflow checks out submodules recursively, builds with `hugo --minify`, and deploys using the official GitHub Pages Actions.

`public/` is gitignored — never commit it; the CI build produces it.

Before the custom domain works, GitHub repo settings → Pages must have the custom domain set, and DNS must have A records pointing to GitHub's servers (`185.199.108-111.153`).
