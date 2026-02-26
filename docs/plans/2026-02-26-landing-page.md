# Landing Page Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Replace the "Coming Soon" page with a polished single-page landing site for Trinetry Infotech (IT/AI/ML/Quant consulting).

**Architecture:** All content lives in a single `public/index.html` file — inline `<style>` block for CSS, inline `<script>` for any JS micro-interactions. No build step, no framework. Google Fonts loaded via CDN `<link>`. Firebase Hosting serves the static file as-is.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, animations), vanilla JS, Google Fonts (DM Serif Display + DM Sans), Firebase Hosting.

---

## Reference

Design doc: `docs/plans/2026-02-26-landing-page-design.md`

---

### Task 1: Base HTML Shell + Fonts + CSS Reset

**Files:**
- Modify: `public/index.html` (full rewrite)

**Step 1: Replace the entire file content**

Replace `public/index.html` with the following shell. This sets up the document structure, loads fonts, and defines CSS variables and the global reset. Do NOT add section content yet.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Trinetry Infotech — AI · ML · Quantitative Systems · Consulting</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&display=swap" rel="stylesheet" />
  <style>
    /* ── Variables ─────────────────────────────────────── */
    :root {
      --bg:        #F5F2EC;
      --ink:       #1A1A18;
      --muted:     #8A8880;
      --rule:      rgba(26,26,24,0.12);
      --max-w:     1100px;
      --pad-x:     clamp(1.5rem, 6vw, 5rem);
      --pad-y:     clamp(5rem, 10vw, 9rem);
      --font-serif: 'DM Serif Display', Georgia, serif;
      --font-sans:  'DM Sans', system-ui, sans-serif;
    }

    /* ── Reset ─────────────────────────────────────────── */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      background: var(--bg);
      color: var(--ink);
      font-family: var(--font-sans);
      font-size: 1rem;
      line-height: 1.7;
      -webkit-font-smoothing: antialiased;
      position: relative;
      overflow-x: hidden;
    }

    /* ── Ink texture overlay ───────────────────────────── */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='300' height='300' filter='url(%23n)' opacity='1'/%3E%3C/svg%3E");
      opacity: 0.04;
      pointer-events: none;
      z-index: 1000;
    }

    /* ── Layout helpers ────────────────────────────────── */
    .container {
      max-width: var(--max-w);
      margin: 0 auto;
      padding: 0 var(--pad-x);
    }
    section {
      padding: var(--pad-y) 0;
    }
    hr.rule {
      border: none;
      border-top: 1px solid var(--rule);
    }
  </style>
</head>
<body>

  <!-- Sections will be added in subsequent tasks -->

</body>
</html>
```

**Step 2: Verify in browser**

Open `public/index.html` directly in a browser (file:// or `firebase serve`). Expected: blank parchment page, no errors in console.

**Step 3: Commit**

```bash
git add public/index.html
git commit -m "feat: base HTML shell, CSS variables, ink texture overlay"
```

---

### Task 2: Hero Section

**Files:**
- Modify: `public/index.html` — add hero HTML inside `<body>`, add hero CSS inside `<style>`

**Step 1: Add hero HTML**

Replace the `<!-- Sections will be added in subsequent tasks -->` comment with:

```html
<!-- ── HERO ──────────────────────────────────────────── -->
<section class="hero">
  <div class="container">
    <p class="hero__eyebrow">trinetryinfotech.com</p>
    <h1 class="hero__headline">Intelligence,<br><em>Engineered.</em></h1>
    <p class="hero__sub">AI &middot; ML &middot; Quantitative Systems &middot; Consulting</p>
  </div>
</section>
<hr class="rule" />
```

**Step 2: Add hero CSS**

Append inside the `<style>` block (before `</style>`):

```css
/* ── Hero ──────────────────────────────────────────────── */
.hero {
  min-height: 100svh;
  display: flex;
  align-items: center;
  padding-top: clamp(4rem, 10vw, 8rem);
  padding-bottom: clamp(4rem, 10vw, 8rem);
}
.hero__eyebrow {
  font-family: var(--font-sans);
  font-size: 0.7rem;
  font-weight: 500;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: var(--muted);
  margin-bottom: 2.5rem;
}
.hero__headline {
  font-family: var(--font-serif);
  font-size: clamp(3.8rem, 10vw, 8.5rem);
  font-weight: 400;
  line-height: 1.05;
  letter-spacing: -0.02em;
  color: var(--ink);
  margin-bottom: 2rem;
}
.hero__headline em {
  font-style: italic;
  color: var(--muted);
}
.hero__sub {
  font-family: var(--font-sans);
  font-size: clamp(0.85rem, 1.5vw, 1rem);
  font-weight: 300;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--muted);
}
```

**Step 3: Verify**

Reload browser. Expected: full-viewport hero with large serif headline "Intelligence, *Engineered.*" on parchment background. Italic "Engineered." in muted tone. Subline with dot separators.

**Step 4: Commit**

```bash
git add public/index.html
git commit -m "feat: add hero section"
```

---

### Task 3: Services Section

**Files:**
- Modify: `public/index.html` — add services HTML after hero `<hr>`, add services CSS

**Step 1: Add services HTML**

After the hero `<hr class="rule" />`, add:

```html
<!-- ── SERVICES ───────────────────────────────────────── -->
<section class="services">
  <div class="container">
    <h2 class="section-label">Services</h2>
    <div class="services__grid">

      <article class="service-item">
        <span class="service-item__num">01</span>
        <div class="service-item__body">
          <h3 class="service-item__title">AI/ML Model Development</h3>
          <p class="service-item__desc">End-to-end design, training, and deployment of machine learning models tailored to your domain.</p>
        </div>
      </article>

      <article class="service-item">
        <span class="service-item__num">02</span>
        <div class="service-item__body">
          <h3 class="service-item__title">Quantitative Trading Systems</h3>
          <p class="service-item__desc">Research-grade algorithmic strategies, backtesting infrastructure, and live execution pipelines.</p>
        </div>
      </article>

      <article class="service-item">
        <span class="service-item__num">03</span>
        <div class="service-item__body">
          <h3 class="service-item__title">Data Engineering & Analytics</h3>
          <p class="service-item__desc">Scalable data pipelines, warehousing, and intelligence layers that turn raw data into decisions.</p>
        </div>
      </article>

      <article class="service-item">
        <span class="service-item__num">04</span>
        <div class="service-item__body">
          <h3 class="service-item__title">Custom Software & Tech Consulting</h3>
          <p class="service-item__desc">Bespoke engineering solutions and strategic technology advisory for complex business problems.</p>
        </div>
      </article>

      <article class="service-item">
        <span class="service-item__num">05</span>
        <div class="service-item__body">
          <h3 class="service-item__title">Research & Prototyping</h3>
          <p class="service-item__desc">Rapid experimentation and proof-of-concept development at the frontier of AI and quantitative methods.</p>
        </div>
      </article>

    </div>
  </div>
</section>
<hr class="rule" />
```

**Step 2: Add services CSS**

Append inside `<style>`:

```css
/* ── Section label ─────────────────────────────────────── */
.section-label {
  font-family: var(--font-sans);
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: var(--muted);
  margin-bottom: 4rem;
}

/* ── Services ──────────────────────────────────────────── */
.services__grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0;
}
.service-item {
  display: grid;
  grid-template-columns: 5rem 1fr;
  gap: 0 1.5rem;
  padding: 2.5rem 0;
  border-top: 1px solid var(--rule);
  position: relative;
  transition: background 0.25s ease;
  cursor: default;
}
.service-item:nth-child(odd) {
  padding-right: 3rem;
}
.service-item:nth-child(even) {
  padding-left: 3rem;
  border-left: 1px solid var(--rule);
}
.service-item:hover {
  background: rgba(26,26,24,0.025);
}
.service-item__num {
  font-family: var(--font-serif);
  font-size: 3.5rem;
  font-weight: 400;
  color: var(--ink);
  opacity: 0.07;
  line-height: 1;
  padding-top: 0.1rem;
  user-select: none;
}
.service-item__title {
  font-family: var(--font-serif);
  font-size: 1.2rem;
  font-weight: 400;
  color: var(--ink);
  margin-bottom: 0.5rem;
  line-height: 1.3;
}
.service-item__desc {
  font-size: 0.9rem;
  color: var(--muted);
  line-height: 1.65;
}
```

**Step 3: Verify**

Reload. Expected: two-column grid of services, each with a large faint number watermark, serif title, and muted descriptor. Odd items on left, even on right with a dividing rule.

**Step 4: Commit**

```bash
git add public/index.html
git commit -m "feat: add services section with two-column staggered grid"
```

---

### Task 4: About Section

**Files:**
- Modify: `public/index.html` — add about HTML after services `<hr>`, add about CSS

**Step 1: Add about HTML**

After the services `<hr class="rule" />`, add:

```html
<!-- ── ABOUT ──────────────────────────────────────────── -->
<section class="about">
  <div class="container">
    <h2 class="section-label">About</h2>
    <div class="about__inner">
      <p class="about__text">
        Trinetry Infotech is a specialist technology firm at the intersection of artificial intelligence, quantitative research, and software engineering. We partner with organisations to build intelligent systems that are rigorous, scalable, and grounded in first principles.
      </p>
    </div>
  </div>
</section>
<hr class="rule" />
```

**Step 2: Add about CSS**

Append inside `<style>`:

```css
/* ── About ─────────────────────────────────────────────── */
.about__inner {
  border-left: 2px solid var(--ink);
  padding-left: 2.5rem;
  max-width: 680px;
}
.about__text {
  font-family: var(--font-serif);
  font-size: clamp(1.15rem, 2.2vw, 1.45rem);
  font-weight: 400;
  line-height: 1.65;
  color: var(--ink);
}
```

**Step 3: Verify**

Reload. Expected: a clean section with a left ink rule, large serif paragraph text. Elegant and editorial.

**Step 4: Commit**

```bash
git add public/index.html
git commit -m "feat: add about section with editorial left-rule layout"
```

---

### Task 5: Contact Section + Footer

**Files:**
- Modify: `public/index.html` — add contact + footer HTML, add CSS

**Step 1: Add contact + footer HTML**

After the about `<hr class="rule" />`, add:

```html
<!-- ── CONTACT ────────────────────────────────────────── -->
<section class="contact">
  <div class="container contact__inner">
    <p class="contact__label">Start a Conversation</p>
    <a class="contact__email" href="mailto:hello@trinetryinfotech.com">hello@trinetryinfotech.com</a>
  </div>
</section>

<!-- ── FOOTER ─────────────────────────────────────────── -->
<footer class="footer">
  <div class="container">
    <p>&copy; 2026 trinetryinfotech.com &mdash; All rights reserved.</p>
  </div>
</footer>
```

> **Note:** Replace `hello@trinetryinfotech.com` with the actual contact email before deploying.

**Step 2: Add contact + footer CSS**

Append inside `<style>`:

```css
/* ── Contact ───────────────────────────────────────────── */
.contact__inner {
  text-align: center;
}
.contact__label {
  font-family: var(--font-sans);
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: var(--muted);
  margin-bottom: 1.5rem;
}
.contact__email {
  display: inline-block;
  font-family: 'Courier New', Courier, monospace;
  font-size: clamp(1.1rem, 3vw, 1.8rem);
  font-weight: 400;
  color: var(--ink);
  text-decoration: none;
  border-bottom: 1px solid var(--ink);
  padding-bottom: 0.15em;
  transition: opacity 0.2s ease;
  letter-spacing: -0.01em;
}
.contact__email:hover {
  opacity: 0.5;
}

/* ── Footer ────────────────────────────────────────────── */
.footer {
  padding: 2.5rem 0;
  border-top: 1px solid var(--rule);
}
.footer p {
  font-size: 0.72rem;
  letter-spacing: 0.08em;
  color: var(--muted);
  text-align: center;
}
```

**Step 3: Verify**

Reload. Expected: centered section with small-caps label above a large monospaced email. Footer below with muted copyright line.

**Step 4: Commit**

```bash
git add public/index.html
git commit -m "feat: add contact and footer sections"
```

---

### Task 6: Responsive Mobile Styles

**Files:**
- Modify: `public/index.html` — add responsive CSS inside `<style>`

**Step 1: Add responsive CSS**

Append inside `<style>`:

```css
/* ── Responsive ────────────────────────────────────────── */
@media (max-width: 700px) {
  .services__grid {
    grid-template-columns: 1fr;
  }
  .service-item {
    grid-template-columns: 3.5rem 1fr;
    padding: 1.8rem 0;
  }
  .service-item:nth-child(odd) {
    padding-right: 0;
  }
  .service-item:nth-child(even) {
    padding-left: 0;
    border-left: none;
  }
  .service-item__num {
    font-size: 2.5rem;
  }
}
```

**Step 2: Verify on mobile viewport**

In browser DevTools, toggle device toolbar and test at 390px width (iPhone). Expected:
- Hero headline scales down cleanly
- Services stack to single column, no horizontal rules between left/right
- About text readable
- Email link wraps gracefully

**Step 3: Commit**

```bash
git add public/index.html
git commit -m "feat: add responsive mobile layout for services grid"
```

---

### Task 7: Entrance Animations

**Files:**
- Modify: `public/index.html` — add animation CSS + JS scroll observer

**Step 1: Add animation CSS**

Append inside `<style>`:

```css
/* ── Entrance animations ───────────────────────────────── */
.fade-up {
  opacity: 0;
  transform: translateY(28px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}
.fade-up.visible {
  opacity: 1;
  transform: translateY(0);
}
.fade-up:nth-child(2) { transition-delay: 0.1s; }
.fade-up:nth-child(3) { transition-delay: 0.2s; }
.fade-up:nth-child(4) { transition-delay: 0.3s; }
.fade-up:nth-child(5) { transition-delay: 0.4s; }
```

**Step 2: Add fade-up classes to HTML elements**

Add `class="fade-up"` to:
- `.hero__eyebrow` → `<p class="hero__eyebrow fade-up">`
- `.hero__headline` → `<h1 class="hero__headline fade-up">`
- `.hero__sub` → `<p class="hero__sub fade-up">`
- Each `.service-item` → `<article class="service-item fade-up">`
- `.about__inner` → `<div class="about__inner fade-up">`
- `.contact__inner` → `<div class="container contact__inner fade-up">`

**Step 3: Add IntersectionObserver JS**

Before `</body>`, add:

```html
<script>
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.12 });

  document.querySelectorAll('.fade-up').forEach(el => observer.observe(el));
</script>
```

**Step 4: Verify**

Reload page. Expected: elements fade up as they enter the viewport. Hero elements stagger in on load. Services animate as you scroll down.

**Step 5: Commit**

```bash
git add public/index.html
git commit -m "feat: add scroll-triggered fade-up entrance animations"
```

---

### Task 8: Final Polish & Deploy

**Files:**
- Modify: `public/index.html` — final tweaks

**Step 1: Update the contact email**

Find `hello@trinetryinfotech.com` (appears twice — in `href` and display text) and replace with the real contact email address. Ask the user for the correct email if unknown.

**Step 2: Full cross-browser review**

Check in:
- Chrome (desktop + mobile emulation)
- Firefox
- Safari (if available)

Look for: font loading, texture overlay, hover states, animation timing.

**Step 3: Deploy to Firebase**

```bash
firebase deploy --only hosting
```

Expected output: `Hosting URL: https://trinetryinfotech-website.web.app` (or custom domain).

**Step 4: Final commit**

```bash
git add public/index.html
git commit -m "feat: complete landing page — ready for production"
```

---

## Summary of Tasks

| # | Task | Commit message |
|---|------|---------------|
| 1 | Base shell, variables, texture | `feat: base HTML shell, CSS variables, ink texture overlay` |
| 2 | Hero section | `feat: add hero section` |
| 3 | Services section | `feat: add services section with two-column staggered grid` |
| 4 | About section | `feat: add about section with editorial left-rule layout` |
| 5 | Contact + footer | `feat: add contact and footer sections` |
| 6 | Mobile responsive | `feat: add responsive mobile layout for services grid` |
| 7 | Animations | `feat: add scroll-triggered fade-up entrance animations` |
| 8 | Polish + deploy | `feat: complete landing page — ready for production` |
