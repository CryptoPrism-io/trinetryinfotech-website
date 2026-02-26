# Trinetry Infotech — Landing Page Design
**Date:** 2026-02-26
**Status:** Approved

## Overview

Replace the existing "Coming Soon" page with a polished, single-page landing site for Trinetry Infotech — an IT services and consulting company specialising in AI, ML, quantitative systems, and tech projects.

## Aesthetic Direction

**Style:** White Space Luxury — editorial, refined, boutique quant firm meets art direction.

### Palette
- Background: `#F5F2EC` (warm parchment)
- Primary text: `#1A1A18` (warm near-black)
- Muted / secondary: `#8A8880`
- Ink texture overlay: 4% opacity noise across full page

### Typography
- **Display / Headlines:** DM Serif Display (Google Fonts)
- **Body / Labels:** DM Sans (Google Fonts)
- Oversized section numbers as watermarks: DM Serif Display, ~10–12rem, ~8% opacity

### Layout
- Full-width sections, generous vertical padding (120–160px)
- Max content width: 1100px, centered
- Thin horizontal rule lines between sections
- Whitespace-driven — no heavy borders or boxes

## Sections

### 1. Hero
- Full-viewport height
- Headline (DM Serif Display, large): *"Intelligence, Engineered."*
- Subline (DM Sans, muted): *"AI · ML · Quantitative Systems · Consulting"*
- Thin horizontal rule below
- No CTA buttons

### 2. Services (01–05)
Ordered as specified:
1. AI/ML Model Development
2. Quantitative Trading Systems
3. Data Engineering & Analytics
4. Custom Software / Tech Consulting
5. Research & Prototyping

Layout: Two-column staggered grid (desktop), single column (mobile).
Each row: oversized watermark number + bold service label + one-line descriptor.
Hover: subtle lift with ink shadow.

### 3. About
- 2–3 sentence paragraph about the company (placeholder, user to swap)
- Left-aligned with left vertical rule accent
- Wide inner margins

### 4. Contact
- Centered layout
- Small-caps label: *"START A CONVERSATION"*
- Email address in large monospace type
- Nothing else

### 5. Footer
- Single line: domain + copyright year
- Minimal, muted

## Technical Constraints
- Pure HTML/CSS/JS — no framework
- Static site hosted on Firebase Hosting
- Single file: `public/index.html`
- Google Fonts loaded via `<link>` (DM Serif Display + DM Sans)
- No build step required

## Out of Scope
- Multi-page routing
- Contact form / backend
- CMS integration
- Analytics
