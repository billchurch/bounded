# CLAUDE.md

## What this is

**Bounded** is a free-will exercise: a self-contained web page built by a Claude
agent given a single open-ended prompt and nothing else.

> For historical reasons, the original prompt was: `Build whatever you want,
> however you want.`

The result is `bounded.html` — *Bounded: A Strange Attractor Observatory*, an
animated exploration of strange attractors rendered entirely in the browser.

Treat the creative intent as the author's. If you're asked to extend or modify
it, preserve the voice and aesthetic of the existing work rather than
overwriting it with generic conventions.

## Repository shape

This is intentionally minimal — there is no build system and no dependencies to
install.

- `bounded.html` — the entire project. One self-contained file (HTML + inline
  CSS + inline JS). The only external dependency is Google Fonts loaded via CDN.
- `.github/workflows/deploy-gh-pages.yml` — publishes to GitHub Pages.
- `README.md` — human-facing overview and live URL.

There is no `package.json`, no `node_modules`, no bundler. Do not add a build
pipeline unless the work genuinely outgrows a single file.

## Working on the page locally

No install step. Just open the file:

```bash
open bounded.html
```

Or serve it (useful for testing with a real origin):

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/bounded.html
```

All edits happen directly in `bounded.html`. Keep it self-contained — inline any
new CSS/JS rather than splitting into separate files, so the single-file deploy
model keeps working.

## Publishing / updating

The live site is <https://billchurch.github.io/bounded/>.

Deployment is automatic via GitHub Actions:

1. Commit changes to `bounded.html` and push to `main`.
2. The `deploy-gh-pages` workflow copies `bounded.html` → `index.html`, uploads
   it as a Pages artifact, and deploys it.
3. The site updates within a minute or two.

The workflow triggers only when `bounded.html` or the workflow file itself
changes. You can also run it manually from the **Actions** tab (workflow
dispatch).

To watch a deploy from the CLI:

```bash
gh run watch "$(gh run list --limit 1 --json databaseId --jq '.[0].databaseId')" --exit-status
```

To verify the live site after a deploy:

```bash
curl -s -o /dev/null -w "%{http_code}\n" https://billchurch.github.io/bounded/
```

## Conventions worth keeping

- **Pin GitHub Actions to commit SHAs**, not mutable tags (e.g.
  `actions/checkout@11bd719... # v4.2.2`). When bumping a version, resolve the
  tag to its SHA and update the trailing comment.
- **Single self-contained file.** The deploy assumes everything lives in
  `bounded.html`.
- **Pages source is "GitHub Actions"** (Settings → Pages), already configured.
  Do not switch it to branch-based deploys.
