# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A personal portfolio website for a game programmer. It is a **static, zero-dependency single-page application** built with vanilla HTML, CSS, and JavaScript — no frameworks, no build tools, no package manager.

## Development & Deployment

- **No build step** — edit files directly and open `index.html` in a browser.
- **No npm/package.json** — there are no install or build commands.
- **Deployment**: Pushing to `main` triggers a GitHub Actions workflow (`.github/workflows/static.yml`) that deploys the entire repo to GitHub Pages.
- **External dependency**: Font Awesome 6 loaded via CDN script tag.

## Architecture

### Single-file SPA

All HTML lives in one file (`index.html`, ~1600 lines). Sections are defined as `<div class="page-section section--{name}">` blocks. Only one section is visible at a time, controlled by toggling the `.section--active` CSS class.

### Routing

Custom client-side routing using the History API with query parameters (`?page={sectionName}`):

- Elements with class `section-trigger` and a `data-section="{name}"` attribute trigger navigation.
- `history.pushState()` updates the URL; `popstate` listener handles back/forward.
- On page load, the URL is parsed to restore the active section.
- The `body` element tracks homepage state via the `.isHome` class (controls visibility of the floating home button and other UI).

### Current sections/pages

- `home` — hero, about, skills, education
- `RMG` — detailed project showcase with video

To add a new project page: add a new `.page-section.section--{name}` block in the HTML, add a `.section-trigger[data-section="{name}"]` link, and add corresponding styles.

### Styling

All styles in `style.css`. Key details:

- **Color scheme**: Dark background (`#111111`), light text (`#e2f0f0`), sage green accent (`#71946c`), red accent (`#6b1919`/`#a02626`).
- **Font**: Montserrat.
- **Responsive breakpoints**: 768px, 786px, 1200px, 1216px (mobile-first).
- **Information sections** use a negative-margin trick to extend backgrounds full-width beyond the content wrapper.

### Assets

All media files (videos, images, PDF) are in the `Assets/` directory, referenced directly from HTML. Videos use `autoplay`, `loop`, `muted`, `playsinline` attributes.
