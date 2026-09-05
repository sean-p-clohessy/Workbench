# Toolkit

Toolkit is the front door for a growing collection of practical education tools. Each tool remains an independent application and repository; this site provides a shared identity, catalogue, and update feed.

## Local development

This is a dependency-free static site. Serve the repository root with any local web server, for example `python -m http.server 8080`, then open `http://localhost:8080`.

## Adding a tool

Add one object to `assets/js/config.js`. The card grid is generated from that central configuration. Each tool supports a title, category, description, URL, repository, accent colour, icon, explicit status tags, CTA text, and optional visual variant.

If the repository should appear in the update feed, also add its display name and repository name to the `tools` array in `scripts/fetch-updates.mjs`.

## Automatic updates

`.github/workflows/update-feed.yml` runs every six hours and can also be triggered manually. It uses the repository-scoped GitHub Actions token on the server, retrieves recent public commits for each configured tool, removes merge/dependency noise, and writes the ten newest meaningful entries to `data/updates.json`. It commits only when the generated file changes. No GitHub credential is exposed to the browser.

The homepage reads this static JSON and displays a graceful empty state before the first successful aggregation.

## GitHub Pages deployment

`.github/workflows/pages.yml` deploys the static site on each push to `main`. In the repository settings, set **Pages → Build and deployment → Source** to **GitHub Actions** if it is not selected automatically.

## Custom domain

The intended custom domain is **edutools.uk**. When the domain is ready, add it in **Repository settings → Pages → Custom domain**, then configure the DNS records GitHub provides. GitHub will create a `CNAME` file in the repository. Enable **Enforce HTTPS** after DNS has propagated. The repository remains named `Workbench` until its deployment configuration is migrated separately.
