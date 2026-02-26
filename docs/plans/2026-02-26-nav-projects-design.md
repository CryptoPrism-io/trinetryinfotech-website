# Nav + Projects Section Design
**Date:** 2026-02-26
**Status:** Approved

## Overview
Add a fixed navigation bar and a Projects section to `public/index.html`. No new files — all inline in the single HTML file.

## Navigation Bar

### Structure
- Fixed top bar, full width, `z-index: var(--z-nav)` (200)
- Left: domain name in small-caps eyebrow style
- Right: anchor links — Services · Projects · About · Contact

### Behaviour
- Background: `var(--bg)` at 92% opacity + `backdrop-filter: blur(12px)`
- On load: no bottom border
- On scroll > 60px: hairline `1px solid var(--rule)` fades in via JS class toggle
- Active section highlighting via IntersectionObserver (ink colour, others muted)
- Mobile < 700px: links hidden, hamburger `☰` button shown → full-width overlay menu

### CSS
- `.site-nav`: fixed, top 0, full width, flex, space-between, backdrop-filter
- `.nav__logo`: small-caps, 0.7rem, letter-spacing 0.22em, var(--muted) → var(--ink) on scroll
- `.nav__links`: flex, gap, uppercase, 0.68rem, letter-spacing 0.18em
- `.nav__link`: color var(--muted), transition; `.nav__link.active`: color var(--ink)
- `.nav--scrolled`: adds border-bottom
- `.nav__hamburger`: hidden on desktop, visible on mobile
- `.nav__overlay`: full-screen overlay menu for mobile

## Projects Section

### Position
Between Services and About sections.

### Layout
- Two cards in a CSS grid (1fr 1fr), gap 2rem, stacked on mobile
- Section label: "Projects" in same `.section-label` style
- Each card: `1px solid var(--rule)` border, padding 2.5rem, hover: translateY(-4px) + subtle shadow

### Card Structure (per product)
1. Sanskrit script label (small, muted, DM Sans)
2. Product name (DM Serif Display, ~2rem)
3. Tagline (italic, muted)
4. Horizontal rule
5. One-line description (DM Sans, 0.9rem, muted)
6. Feature pills (3–4 small outlined tags)
7. Tech stack (tiny monospace labels)
8. "View Project →" link (bottom, ink colour, underline on hover)

### Products

**Gyanmarg**
- Sanskrit: ज्ञानमार्ग
- Tagline: "Transform ancient wisdom into modern mastery"
- Description: Gamified learning platform with spaced repetition, active recall, and 10 curated knowledge modules
- Features: Spaced Repetition · XP & Levels · PWA · 45+ Ebooks
- Stack: React 19 · TypeScript · Vite · GCP Cloud Run
- URL: https://gyanmarg-963362833537.us-central1.run.app

**Pratyaksha**
- Sanskrit: प्रत्यक्ष
- Tagline: "See Your Mind. Clearly."
- Description: Cognitive journaling dashboard with a 4-agent AI pipeline for emotion, theme, and insight analysis
- Features: AI Insights · Emotion Mapping · Theme Detection · Airtable Sync
- Stack: React · Express · GPT-4o · GCP Cloud Run
- URL: https://pratyaksha-963362833537.asia-south1.run.app

## Technical Notes
- Single `public/index.html` file — all CSS inline in `<style>`, JS inline before `</body>`
- Nav scroll behaviour via small JS snippet (adds `.nav--scrolled` class)
- Active nav link via existing IntersectionObserver pattern
- Mobile hamburger: pure JS toggle, no dependencies
- Sections need `id` attributes added: `#services`, `#projects`, `#about`, `#contact`
- Hero `min-height: 100svh` adjusted to account for nav height (~56px)
