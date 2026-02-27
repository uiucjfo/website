# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static HTML website for the **Jasmine Field Orchestra (JFO)** at UIUC. Hosted on GitHub Pages at `jfouiuc.org`. No build system, no JS framework -- just plain HTML with Tailwind CSS.

## Pages

- `index.html` -- Home page with video hero, about section, music divisions, join CTA
- `about.html` -- Story, core values, organizational structure, music divisions detail
- `charter.html` -- Governance charter document with table of contents, formula boxes, HIAL tier table

## Tailwind CSS v4 Build Process

The site uses **self-hosted Tailwind CSS v4** (not CDN). When HTML classes change, rebuild:

```bash
npm init -y
npm install -D tailwindcss @tailwindcss/cli
npx @tailwindcss/cli -i assets/css/input.css -o assets/css/tailwind.css --minify
```

The input file (`assets/css/input.css`) must contain:
```css
@import "tailwindcss" source("../../");
```

The `source("../../")` tells Tailwind to scan from project root for class usage across all HTML files.

After building, clean up build artifacts: `rm -rf node_modules package.json package-lock.json assets/css/input.css`

Only `assets/css/tailwind.css` should be committed.

## Design System

- **Theme**: Dark (`bg-gray-900` body, `bg-gray-800` alternating sections, `bg-black` footer)
- **Accent**: Pink -- `text-pink-400` (headings/links), `bg-pink-500` (buttons), `bg-pink-600` (hover)
- **Fonts**: Google Fonts -- `Lato` weight 700 (headings), `Open Sans` weights 400/500 (body)
- **Cards**: `bg-gray-800 p-6 rounded-lg` with `hover:scale-105 hover:bg-gray-700`
- **Buttons**: `bg-pink-500 hover:bg-pink-600 text-white font-bold py-3 px-8 rounded-full`
- **Nav breakpoint**: `xl` (not `lg`)
- **Mobile menu**: `bg-gray-800`
- **Active nav link**: `text-pink-400`
- **Header**: Fixed, transparent by default; `.header-scrolled` adds rgba(17,24,39,0.8) + backdrop-blur via JS scroll listener
- **Content max-width**: `max-w-4xl` for charter, `max-w-3xl` for about/index paragraphs

### Charter-specific CSS classes (defined in `<style>` block)

- `.charter-list` -- list items with pink markers
- `.formula-box` -- pink left border, pink-tinted background (for financial formulas)
- `.example-box` -- gray left border, gray-tinted background (for example calculations)
- `.toc-link` -- hover transitions to pink

## SEO Conventions

Each page includes:
- `<title>`, `<meta description>`, `<meta keywords>`, `<meta robots>`
- Canonical URL (`<link rel="canonical">`)
- Open Graph tags (`property="og:*"`)
- Twitter Card tags (`name="twitter:*"` -- use `name`, not `property`)
- JSON-LD structured data (`<script type="application/ld+json">`)
- Skip-to-content accessibility link

## Key Details

- **Domain**: `jfouiuc.org` (CNAME file)
- **Email**: `hello@jfouiuc.com` (intentionally `.com`, not `.org`)
- **Copyright year**: 2026
- **Music divisions**: Symphony, Modern Chinese Orchestra (not "Chinese Folk Music"), Choir, Live Band
- `sitemap.xml` and `robots.txt` are in the project root
