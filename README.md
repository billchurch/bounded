# Bounded

A strange attractor observatory — a single self-contained HTML page that renders
animated strange attractors in the browser.

## Live site

<https://billchurch.github.io/bounded/>

## Local preview

The page is entirely self-contained (the only external dependency is Google
Fonts via CDN), so no build step is required. Open it directly:

```bash
open bounded.html
```

Or serve it locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/bounded.html
```

## Deployment

Pushing to `main` triggers the
[`deploy-gh-pages`](.github/workflows/deploy-gh-pages.yml) workflow, which copies
`bounded.html` to `index.html` and publishes it to GitHub Pages. You can also run
the workflow manually from the Actions tab (workflow dispatch).

One-time setup in the repository: **Settings → Pages → Build and deployment →
Source = GitHub Actions**.
