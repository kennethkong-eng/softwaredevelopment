# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A single-page marketing/landing website for a (fictional "Northbyte") custom software development company. It is built with **plain HTML, CSS, and vanilla JavaScript** — no frameworks, no build step, no package manager, no tests. The only external resource is **Google Fonts** (Inter + Space Grotesk), loaded via CDN `<link>` with a system-font fallback, so the page degrades gracefully offline.

## Running

There is nothing to build. Open the file directly in a browser:

```sh
open index.html        # macOS
```

Any change is reflected by reloading the page in the browser.

## Architecture

Everything lives in **`index.html`** — a single self-contained file with three inline parts:

- **`<style>` in `<head>`** — all CSS. A `:root` block defines the design tokens (color palette `--bg`/`--surface`/`--primary`/`--accent`/`--text`, plus `--radius`, `--shadow`, `--container`, font stacks). The layout is **mobile-first**: base styles target small screens, and `@media (min-width: …)` queries (`640px`, `992px`) progressively enhance to multi-column. Edit tokens in `:root` to re-theme the whole page.
- **`<body>`** — semantic sections in order: sticky `header` navbar → `main` containing `#home` (hero), `#services`, `#testimonials`, `#contact` (enquiry form) → `footer`. Navbar links and the hero CTA are in-page anchors; smooth scrolling is handled in CSS (`scroll-behavior` + `scroll-padding-top` to clear the sticky nav).
- **`<script>` before `</body>`** — an IIFE handling the enquiry form. Validation is **data-driven**: the `FIELDS` array declares which fields are required and their regex rules, and `validate()` iterates it to set/clear inline `role="alert"` error spans and `aria-invalid`. On success it collects a form-data object, `console.log`s it, shows the confirmation banner, and resets. A **commented-out `fetch()` POST** marks where a real backend call goes. Each `FIELDS` entry also gets an `input` listener that clears its error the moment the user starts correcting it, and the footer's `#year` is filled in by JS.

## Conventions

- **Keep it dependency-free and single-file** unless explicitly asked to split into `styles.css` / `script.js`. The whole point is copy-paste-and-open with no tooling.
- **Theme via CSS variables** in `:root`, not hard-coded colors scattered through rules.
- **Accessibility is intentional**: every input has a `<label>`, errors use `aria-describedby` + `role="alert"`, focus is managed in JS (CTA focuses the first field; success moves focus to the banner), and there is a `prefers-reduced-motion` guard. Preserve these when editing.
- To add a validated form field, append a rule to the `FIELDS` array rather than writing bespoke validation.
