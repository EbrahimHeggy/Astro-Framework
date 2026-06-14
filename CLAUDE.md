# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev       # Start dev server at localhost:4321
npm run build     # Production build to dist/
npm run preview   # Preview production build locally
```

No test runner is configured. Playwright is installed as a dev dependency but no test files exist yet.

## Architecture

This is the **ITechSolutions** marketing landing page — a single-page Astro 6 site with no UI framework (no React, Vue, or Svelte). All components are `.astro` files.

**Page composition** (`src/pages/index.astro`):
```
Layout (src/layouts/Layout.astro)
└── Header   → fixed nav with scroll-blur + mobile burger menu
└── Hero     → split-grid with animated dashboard card
└── About    → (about section)
└── Services → (services section)
└── ContactForm → client-side validated form with toast notification
└── Footer
```

**Styling model:**
- Global CSS custom properties (design tokens) and utility classes (`.container`, `.btn`, `.btn-primary`, `.btn-outline`, `.section-label`) are defined in `Layout.astro`'s `<style is:global>` block — this is the single source of truth for the design system.
- Each component uses a scoped `<style>` block for its own styles; they consume the tokens via `var(--token-name)`.
- Do not add a CSS framework or preprocessor unless explicitly asked.

**Design tokens (from `:root` in `Layout.astro`):**
- Colors: `--primary` (#2563EB), `--secondary` (#7C3AED), `--dark`, `--muted`, `--border`, `--surface`, `--white`
- Gradients: `--gradient` (blue→purple), `--gradient-soft`
- Radii: `--radius-sm/md/lg/xl`
- Shadows: `--shadow-sm/md/lg`
- Fonts: Inter (body) + Plus Jakarta Sans (headings), loaded from Google Fonts in `Layout.astro`

**Interactivity:** Vanilla JS in `<script>` tags inside `.astro` files. TypeScript is supported (strict mode via `astro/tsconfigs/strict`). The ContactForm uses client-side validation and a simulated submit (1.4 s timeout, no real backend endpoint).

**Navigation:** All nav links use hash anchors (`#home`, `#about`, `#services`, `#contact`) for single-page scroll behavior.
