# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

`denniscual.github.io` — a personal site served directly by GitHub Pages from the `main` branch of `denniscual/denniscual.github.io`. There is no build step, no package manager, no dependencies, and no tests. Every file in the repo is exactly what the browser receives.

## Working on it

- **Preview:** open the `.html` file directly in a browser, or `python3 -m http.server` from the repo root (root-absolute links like `/redev/` only resolve correctly under a server, not `file://`).
- **Deploy:** push to `main`. GitHub Pages publishes within a minute or so.
- `.nojekyll` disables Jekyll processing — keep it. Without it, Pages would try to build the repo as a Jekyll site.

## Structure and conventions

Pages are directories with an `index.html` so URLs are extensionless (`/redev/`, `/redev/privacy`). Add a new page as `<slug>/index.html`, not `<slug>.html`.

Each page is **fully self-contained**: one HTML file with an inline `<style>` block, no shared stylesheet, no JS, no external assets or fonts. This duplication is deliberate — do not extract a shared CSS file or add a build step to deduplicate it.

Consequently, the design system lives as a copy-pasted `:root` block at the top of every page's `<style>`. When changing a token, change it in **all** pages:

```
--bg: #0d1117    --panel: #161b22    --text: #e6edf3
--dim: #8b949e   --accent: #4cc2c4   --border: #30363d
```

Shared conventions across pages: dark theme only (no light-mode media query), system font stack, `main { max-width: 640–720px }` centered, `--accent` for links and hover borders, `--dim` for secondary text.

Every page needs `<title>` and `<meta name="description">` — these are the only SEO surface, since there's no metadata framework.

## Content notes

- `/redev/` is the product page for Redev, a Chrome extension (source: `github.com/denniscual/redev`). Its Chrome Web Store ID is `ojiiafcaodjlfegglkfgokgebgcfdjia` and appears in two links on that page.
- `/redev/privacy` is the privacy policy the Chrome Web Store listing points at. It makes specific factual claims (no servers, no telemetry, credentials stored locally, interaction recording off by default). Only change these to match actual extension behavior, and bump the "Last updated" date when you do.
