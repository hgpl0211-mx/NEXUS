# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static landing page for **Nexus Intelligent Partners (NIP)** — a process consulting and digital transformation firm targeting micro and SMEs in Latin America. The entire site is a single self-contained file: `index.html`.

## Dev server

```bash
python -m http.server 3000
```

The `.claude/launch.json` is already configured so `preview_start` with name `"NIP Landing Page"` launches this automatically on port 3000.

## Architecture

`index.html` is the entire codebase — no build step, no bundler, no dependencies to install. It contains:

- **`<style>`** — all CSS, organized with section comments (`/* ── Hero */`, `/* ── Services */`, etc.)
- **`<body>`** — semantic HTML sections: `#inicio` → `#servicios` → `#soluciones` → `#tecnologias` → `#nosotros` → `#proceso` → `#contacto` → footer
- **`<script>`** — vanilla JS at the bottom; each feature block is comment-delimited:
  - Solutions-by-area tab system (data-driven, renders cards via JS)
  - Phone country picker (custom dropdown with 22 LATAM countries)
  - Contact form (Formspree AJAX, action URL contains `YOUR_FORM_ID` placeholder)
  - Calendly placeholder (`showCalendlyModal` function)
  - Navbar scroll effect, mobile menu, scroll-to-top, IntersectionObserver animations

## Key placeholders to activate

| Location in file | What to replace | With |
|---|---|---|
| `<form action="https://formspree.io/f/YOUR_FORM_ID"` | `YOUR_FORM_ID` | Real Formspree form ID |
| `function showCalendlyModal` | `alert(...)` stub | Calendly widget embed |

## Design tokens

All colors are CSS custom properties on `:root`:

```
--teal-dark: #2D7468   (primary brand)
--teal-mid:  #3D9688
--teal-light:#5BB8AA
--teal-pale: #E8F5F3   (light backgrounds)
--teal-ultra:#F2FAF9   (section backgrounds)
--charcoal:  #1A2E2C   (text / dark hero)
```

All icons are inline SVGs (Heroicons/Lucide style, `stroke-width: 1.7–1.8`). No emoji icons — the project moved away from those. Technology badge icons (Power Automate, Power BI, Zapier, SAP, Dynamics 365, Power Apps, MCP, IA) are 52×52 custom SVGs with brand colors.

## Solutions-by-area data

The tab section (`#soluciones`) is entirely data-driven. All 8 areas and 48 implementation cards are defined in the `AREAS` array inside the IIFE at the top of the `<script>`. To add/edit an area or card, modify that array — no HTML changes needed.

## Fonts

Loaded from Google Fonts CDN: `Inter` (body) and `Montserrat` (headings). No local font files.
