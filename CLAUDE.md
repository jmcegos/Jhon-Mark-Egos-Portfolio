# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal portfolio site for Jhon Mark Egos (Software Engineer at ActiveSystems Software Inc.). It is a single static page with no build step, package manager, linter, or tests.

To preview, open `index.html` directly in a browser or serve the folder (for example `python -m http.server`).

## Architecture

- **Everything lives in `index.html`.** The CSS sits in a `<style>` block in `<head>`, the markup follows, and a `<script>` block at the end of `<body>` holds all the behavior. External dependencies are limited to Google Fonts (Instrument Serif, Geist, Geist Mono). There is no framework and no Bootstrap.
- **`style.css`, `script.js`, and most of the PNGs are leftovers from the pre-redesign site** (commit `b020af0` replaced it). `index.html` does not reference them. The new page only uses `picture.png` (portrait and favicon) and the certificate images `DICT-WD001.png`, `DICT-WD002.png`, and `ZUITT.png`. Don't edit the legacy files expecting the page to change.
- **Theming:** design tokens are CSS custom properties on `:root`. Dark mode is defined in two places that must stay in sync: under `:root[data-theme="dark"]` (manual toggle) and under `@media (prefers-color-scheme: dark)` with `:root:not([data-theme="light"])` (system preference). The theme button sets `data-theme` on `<html>` and saves it to `localStorage` under the `theme` key.
- **Sections** are anchored by id: `top`, `about`, `experience`, `work`, `services`, `certificates`, `contact`. Nav links target these ids. `scroll-padding-top` offsets them for the fixed nav.
- **JS hooks on markup conventions:**
  - Elements with the `.reveal` class fade in through an IntersectionObserver, which adds `.in`.
  - Certificate cards are `<button class="cert" data-src="...">`. Clicking one opens the shared `#lightbox`.
  - `#year` in the footer is filled with the current year.

When you add content, reuse these classes and tokens rather than introducing new colors or inline scripts.
