# Northbyte — Landing Page

A single-page marketing / landing website for a (fictional) custom software development company, **Northbyte**.

🔗 **Live site:** https://kennethkong-eng.github.io/softwaredevelopment/

## About

Built with **plain HTML, CSS, and vanilla JavaScript** — no frameworks, no build step, no package manager, no dependencies. The only external resource is Google Fonts (Inter + Space Grotesk), loaded via CDN with a system-font fallback so the page degrades gracefully offline.

Everything lives in a single self-contained [`index.html`](index.html):

- **`<style>`** — all CSS. A `:root` block defines the design tokens (colors, radius, shadow, container width, fonts). The layout is mobile-first, progressively enhanced at `640px` and `992px` breakpoints. Re-theme the whole page by editing the variables in `:root`.
- **`<body>`** — semantic sections: sticky header navbar → hero (`#home`) → `#services` → `#testimonials` → `#contact` (enquiry form) → footer. Smooth in-page scrolling is handled in CSS.
- **`<script>`** — an IIFE handling the enquiry form. Validation is data-driven via a `FIELDS` array (required flags + regex rules); errors are surfaced accessibly with `role="alert"` and `aria-invalid`. On success it logs the form data and shows a confirmation banner. A commented-out `fetch()` marks where a real backend call goes.

## Accessibility

Built in intentionally: every input has a `<label>`, errors use `aria-describedby` + `role="alert"`, focus is managed in JS, and there's a `prefers-reduced-motion` guard.

## Running locally

There's nothing to build — just open the file in a browser:

```sh
open index.html        # macOS
```

Any change is reflected by reloading the page.

## Deployment

Hosted on **GitHub Pages**, deployed automatically via GitHub Actions ([`.github/workflows/deploy.yml`](.github/workflows/deploy.yml)) on every push to `main`.
