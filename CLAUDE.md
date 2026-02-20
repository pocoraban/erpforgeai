# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

ERPforgeAI landing page — a static single-page marketing site for an AI-powered SAP ABAP code generation service. The entire site is a single `index.html` file with no build system, no dependencies, and no framework.

## Architecture

- **Single file**: Everything (HTML, CSS, JS) lives in `index.html` (~685 lines)
- **Deployment**: Vercel static hosting, configured via `vercel.json` (security headers, clean URLs)
- **No build step**: Edit `index.html` directly. No bundler, no npm, no compilation.

### Key sections within `index.html`

- **CSS** (lines 11–252): CSS custom properties in `:root` define the design system (colors: `--orange`, `--cyan`, `--bg*`, `--text*`). All styles are inlined in a `<style>` block. Mobile breakpoint at 768px.
- **HTML** (lines 254–568): Sections — launch banner, nav, hero with countdown/waitlist, code preview, how-it-works steps, system profiler download, comparison, pricing tiers (Report €99 / Interface €249 / Complex €499), order form, about, contact, legal pages (Impressum/Datenschutz), footer.
- **JavaScript** (lines 570–684):
  - `showPage(id)` / `showMain()` — toggles between legal pages and main content
  - Form submissions via `fetch` to Formspree (`https://formspree.io/f/xvzbbwka`) for waitlist, contact, and order forms
  - Countdown timer targeting `2026-04-01T09:00:00+02:00`
  - `STECKBRIEF` constant — embedded ABAP source code (~425 lines) for `Z_SYSTEM_STECKBRIEF.abap` that users download
  - `downloadSteckbrief()` — creates a Blob download of the ABAP source
  - **i18n system**: `T` object with `en` and `de` translation keys, applied via `data-i18n` attributes on HTML elements. `setLang(l)` switches language and persists to `localStorage`.
  - Scroll-triggered fade-in animations via `IntersectionObserver`

## Development

No commands needed. Open `index.html` in a browser to preview. Deploy by pushing to the Vercel-connected repository.

## Conventions

- Fonts: Space Grotesk (body), Syne (headings), JetBrains Mono (code/monospace)
- All translatable text uses `data-i18n="key"` attributes — update both `en` and `de` entries in the `T` object when changing copy
- CSS classes are short/abbreviated (e.g., `pc` = pricing card, `fg` = form group, `cmp` = comparison, `dl` = download)
- Forms use `autocomplete="new-password"` to prevent browser autofill
