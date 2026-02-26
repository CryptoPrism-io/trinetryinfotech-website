# Nav + Projects Section Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add a fixed navigation bar with anchor links and a Projects section (Gyanmarg + Pratyaksha) to the existing single-page landing site.

**Architecture:** All changes are inline in `public/index.html` — CSS appended to the `<style>` block, HTML inserted into `<body>`, JS merged into the existing `<script>` block before `</body>`. No new files. Section `id` attributes are added to enable smooth-scroll anchoring.

**Tech Stack:** HTML5, CSS3, vanilla JS (IntersectionObserver already in use), existing DM Serif Display + DM Sans fonts.

---

## Context

Current file: `public/index.html` (370 lines)
- CSS: lines 12–263 inside `<style>`
- Hero section: lines 268–276
- Services section: lines 278–327
- About section: lines 329–340
- Contact section: lines 342–348
- Footer: lines 350–355
- Script block: lines 357–368

---

### Task 1: Add Section IDs for Anchor Navigation

**Files:**
- Modify: `public/index.html`

**Step 1: Add `id` attributes to sections**

Make these 4 exact edits:

Change `<section class="hero">` → `<section class="hero" id="home">`

Change `<section class="services" aria-labelledby="services-heading">` → `<section class="services" id="services" aria-labelledby="services-heading">`

Change `<section class="about" aria-labelledby="about-heading">` → `<section class="about" id="about" aria-labelledby="about-heading">`

Change `<section class="contact" aria-labelledby="contact-heading">` → `<section class="contact" id="contact" aria-labelledby="contact-heading">`

**Step 2: Also adjust hero top padding to account for nav height (56px)**

Change `.hero` CSS from:
```css
.hero {
  min-height: 100svh;
  display: flex;
  align-items: center;
  padding-top: clamp(4rem, 10vw, 8rem);
  padding-bottom: clamp(4rem, 10vw, 8rem);
}
```
To:
```css
.hero {
  min-height: 100svh;
  display: flex;
  align-items: center;
  padding-top: clamp(5rem, 12vw, 10rem);
  padding-bottom: clamp(4rem, 10vw, 8rem);
}
```

**Step 3: Commit**
```bash
cd /c/cpio_db/trinetryinfotech-website
git add public/index.html
git commit -m "feat: add section IDs for anchor navigation"
```

---

### Task 2: Navigation Bar — HTML + CSS

**Files:**
- Modify: `public/index.html`

**Step 1: Add nav HTML**

Insert the following immediately after `<body>` (before the `<!-- ── HERO -->` comment):

```html
<!-- ── NAV ───────────────────────────────────────────── -->
<nav class="site-nav" aria-label="Main navigation">
  <div class="nav__inner container">
    <a class="nav__logo" href="#home">trinetryinfotech.com</a>
    <ul class="nav__links" role="list">
      <li><a class="nav__link" href="#services">Services</a></li>
      <li><a class="nav__link" href="#projects">Projects</a></li>
      <li><a class="nav__link" href="#about">About</a></li>
      <li><a class="nav__link" href="#contact">Contact</a></li>
    </ul>
    <button class="nav__hamburger" aria-label="Open menu" aria-expanded="false">
      <span></span><span></span><span></span>
    </button>
  </div>
</nav>

<!-- ── NAV OVERLAY (mobile) ──────────────────────────── -->
<div class="nav__overlay" aria-hidden="true">
  <ul class="nav__overlay-links" role="list">
    <li><a class="nav__overlay-link" href="#services">Services</a></li>
    <li><a class="nav__overlay-link" href="#projects">Projects</a></li>
    <li><a class="nav__overlay-link" href="#about">About</a></li>
    <li><a class="nav__overlay-link" href="#contact">Contact</a></li>
  </ul>
</div>
```

**Step 2: Add nav CSS**

Append inside `<style>` block, before the `/* ── Hero */` comment:

```css
/* ── Nav ────────────────────────────────────────────────── */
.site-nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: var(--z-nav);
  background: rgba(245,242,236,0.92);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  transition: border-color 0.3s ease;
  border-bottom: 1px solid transparent;
}
.site-nav.nav--scrolled {
  border-bottom-color: var(--rule);
}
.nav__inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 56px;
}
.nav__logo {
  font-family: var(--font-sans);
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: var(--muted);
  text-decoration: none;
  transition: color 0.2s ease;
}
.nav__logo:hover,
.site-nav.nav--scrolled .nav__logo {
  color: var(--ink);
}
.nav__links {
  display: flex;
  align-items: center;
  gap: 2.5rem;
  list-style: none;
}
.nav__link {
  font-family: var(--font-sans);
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--muted);
  text-decoration: none;
  transition: color 0.2s ease;
}
.nav__link:hover,
.nav__link.active {
  color: var(--ink);
}
.nav__hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
}
.nav__hamburger span {
  display: block;
  width: 22px;
  height: 1px;
  background: var(--ink);
  transition: transform 0.3s ease, opacity 0.3s ease;
}
.nav__hamburger.open span:nth-child(1) { transform: translateY(6px) rotate(45deg); }
.nav__hamburger.open span:nth-child(2) { opacity: 0; }
.nav__hamburger.open span:nth-child(3) { transform: translateY(-6px) rotate(-45deg); }

/* ── Nav Overlay (mobile) ─────────────────────────────── */
.nav__overlay {
  position: fixed;
  inset: 0;
  top: 56px;
  background: var(--bg);
  z-index: calc(var(--z-nav) - 1);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
}
.nav__overlay.open {
  opacity: 1;
  pointer-events: auto;
}
.nav__overlay-links {
  list-style: none;
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
}
.nav__overlay-link {
  font-family: var(--font-serif);
  font-size: 2.2rem;
  color: var(--ink);
  text-decoration: none;
  letter-spacing: -0.01em;
}
.nav__overlay-link:hover {
  color: var(--muted);
}
```

**Step 3: Add nav responsive CSS**

Inside the existing `@media (max-width: 700px)` block, append:

```css
  .nav__links { display: none; }
  .nav__hamburger { display: flex; }
```

**Step 4: Commit**
```bash
git add public/index.html
git commit -m "feat: add fixed navigation bar with mobile overlay"
```

---

### Task 3: Navigation Bar — JavaScript

**Files:**
- Modify: `public/index.html` — merge into existing `<script>` block before `</body>`

**Step 1: Add nav JS to the existing script block**

The existing script block ends with:
```js
    document.querySelectorAll('.fade-up').forEach(el => observer.observe(el));
  </script>
```

Replace that closing with the following (add the new code before `</script>`):

```js
    document.querySelectorAll('.fade-up').forEach(el => observer.observe(el));

    // Nav scroll border
    const nav = document.querySelector('.site-nav');
    window.addEventListener('scroll', () => {
      nav.classList.toggle('nav--scrolled', window.scrollY > 60);
    }, { passive: true });

    // Active nav link via IntersectionObserver
    const sections = document.querySelectorAll('section[id]');
    const navLinks = document.querySelectorAll('.nav__link');
    const sectionObserver = new IntersectionObserver((entries) => {
      entries.forEach(e => {
        if (e.isIntersecting) {
          navLinks.forEach(l => l.classList.remove('active'));
          const active = document.querySelector(`.nav__link[href="#${e.target.id}"]`);
          if (active) active.classList.add('active');
        }
      });
    }, { threshold: 0.4 });
    sections.forEach(s => sectionObserver.observe(s));

    // Hamburger menu
    const hamburger = document.querySelector('.nav__hamburger');
    const overlay = document.querySelector('.nav__overlay');
    const overlayLinks = document.querySelectorAll('.nav__overlay-link');
    hamburger.addEventListener('click', () => {
      const open = hamburger.classList.toggle('open');
      hamburger.setAttribute('aria-expanded', open);
      overlay.classList.toggle('open', open);
      overlay.setAttribute('aria-hidden', !open);
    });
    overlayLinks.forEach(link => {
      link.addEventListener('click', () => {
        hamburger.classList.remove('open');
        hamburger.setAttribute('aria-expanded', false);
        overlay.classList.remove('open');
        overlay.setAttribute('aria-hidden', true);
      });
    });
  </script>
```

**Step 2: Verify**

Open `public/index.html` in browser. Expected:
- Nav bar visible at top on parchment background
- Scroll down > 60px → hairline border appears under nav
- Active link highlights as you scroll through sections
- On mobile (resize to < 700px): hamburger appears, links hidden
- Click hamburger → full-screen overlay with large serif links

**Step 3: Commit**
```bash
git add public/index.html
git commit -m "feat: add nav scroll, active highlighting, and hamburger JS"
```

---

### Task 4: Projects Section — HTML + CSS

**Files:**
- Modify: `public/index.html`

**Step 1: Add projects HTML**

Insert after `<hr class="rule" />` (the one after the services section, line 327), before `<!-- ── ABOUT -->`:

```html
<!-- ── PROJECTS ──────────────────────────────────────── -->
<section class="projects" id="projects" aria-labelledby="projects-heading">
  <div class="container">
    <h2 class="section-label" id="projects-heading">Projects</h2>
    <div class="projects__grid">

      <!-- Gyanmarg -->
      <article class="project-card fade-up">
        <div class="project-card__header">
          <p class="project-card__sanskrit">ज्ञानमार्ग</p>
          <h3 class="project-card__name">Gyanmarg</h3>
          <p class="project-card__tagline"><em>Transform ancient wisdom into modern mastery</em></p>
        </div>
        <hr class="project-card__rule" />
        <p class="project-card__desc">Gamified learning platform with spaced repetition, active recall, and 10 curated knowledge modules drawn from 45+ books.</p>
        <ul class="project-card__pills" aria-label="Features">
          <li>Spaced Repetition</li>
          <li>XP &amp; Levels</li>
          <li>PWA</li>
          <li>45+ Ebooks</li>
        </ul>
        <p class="project-card__stack">React 19 &middot; TypeScript &middot; Vite &middot; GCP Cloud Run</p>
        <a class="project-card__link" href="https://gyanmarg-963362833537.us-central1.run.app" target="_blank" rel="noopener noreferrer">View Project &rarr;</a>
      </article>

      <!-- Pratyaksha -->
      <article class="project-card fade-up">
        <div class="project-card__header">
          <p class="project-card__sanskrit">प्रत्यक्ष</p>
          <h3 class="project-card__name">Pratyaksha</h3>
          <p class="project-card__tagline"><em>See Your Mind. Clearly.</em></p>
        </div>
        <hr class="project-card__rule" />
        <p class="project-card__desc">Cognitive journaling dashboard with a 4-agent AI pipeline for emotion mapping, theme detection, and actionable insights.</p>
        <ul class="project-card__pills" aria-label="Features">
          <li>AI Insights</li>
          <li>Emotion Mapping</li>
          <li>Theme Detection</li>
          <li>Airtable Sync</li>
        </ul>
        <p class="project-card__stack">React &middot; Express &middot; GPT-4o &middot; GCP Cloud Run</p>
        <a class="project-card__link" href="https://pratyaksha-963362833537.asia-south1.run.app" target="_blank" rel="noopener noreferrer">View Project &rarr;</a>
      </article>

    </div>
  </div>
</section>
<hr class="rule" />
```

**Step 2: Add projects CSS**

Append inside `<style>` block, after the `/* ── About */` block:

```css
/* ── Projects ──────────────────────────────────────────── */
.projects__grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
}
.project-card {
  border: 1px solid var(--rule);
  padding: 2.5rem;
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.project-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 40px rgba(26,26,24,0.08);
}
.project-card__sanskrit {
  font-family: var(--font-sans);
  font-size: 0.72rem;
  letter-spacing: 0.1em;
  color: var(--muted);
  margin-bottom: 0.35rem;
}
.project-card__name {
  font-family: var(--font-serif);
  font-size: 2rem;
  font-weight: 400;
  color: var(--ink);
  line-height: 1.1;
  letter-spacing: -0.02em;
}
.project-card__tagline {
  font-family: var(--font-serif);
  font-size: 0.95rem;
  color: var(--muted);
  line-height: 1.5;
}
.project-card__rule {
  border: none;
  border-top: 1px solid var(--rule);
}
.project-card__desc {
  font-size: 0.9rem;
  color: var(--muted);
  line-height: 1.65;
}
.project-card__pills {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  list-style: none;
}
.project-card__pills li {
  font-family: var(--font-sans);
  font-size: 0.65rem;
  font-weight: 500;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--ink);
  border: 1px solid var(--rule);
  padding: 0.25rem 0.65rem;
}
.project-card__stack {
  font-family: 'Courier New', Courier, monospace;
  font-size: 0.72rem;
  color: var(--muted);
  letter-spacing: 0.02em;
  margin-top: auto;
}
.project-card__link {
  font-family: var(--font-sans);
  font-size: 0.72rem;
  font-weight: 500;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--ink);
  text-decoration: none;
  border-bottom: 1px solid var(--ink);
  padding-bottom: 0.1em;
  align-self: flex-start;
  transition: opacity 0.2s ease;
}
.project-card__link:hover {
  opacity: 0.5;
}
```

**Step 3: Add projects responsive CSS**

Inside the existing `@media (max-width: 700px)` block, append:

```css
  .projects__grid { grid-template-columns: 1fr; }
  .project-card { padding: 1.8rem; }
```

**Step 4: Add project card transition to prefers-reduced-motion block**

In the existing `@media (prefers-reduced-motion: reduce)` block, add:
```css
  .project-card { transition: none; }
  .project-card__link { transition: none; }
```

**Step 5: Commit**
```bash
git add public/index.html
git commit -m "feat: add projects section with Gyanmarg and Pratyaksha cards"
```

---

### Task 5: Final Verification + Deploy

**Step 1: Visual check (desktop)**
Open `public/index.html` in browser. Confirm:
- Nav bar at top, scrolled border appears correctly
- Hero headline visible below nav (not hidden behind it)
- Services section with anchor link scrolls correctly
- Projects section appears between Services and About
- Both cards render with correct content, pills, stack, live links
- Hover on cards: subtle lift + shadow
- "View Project →" links open in new tab

**Step 2: Visual check (mobile)**
Resize to 390px. Confirm:
- Hamburger button visible, nav links hidden
- Overlay opens/closes correctly
- Project cards stacked single column

**Step 3: Deploy**
```bash
cd /c/cpio_db/trinetryinfotech-website
git add public/index.html
git push origin master
```
GitHub Actions auto-deploys in ~30s.

**Step 4: Verify live**
Visit https://trinetryinfotech.web.app — confirm all sections visible and nav works.

---

## Summary

| # | Task | Commit |
|---|------|--------|
| 1 | Section IDs + hero padding | `feat: add section IDs for anchor navigation` |
| 2 | Nav HTML + CSS | `feat: add fixed navigation bar with mobile overlay` |
| 3 | Nav JavaScript | `feat: add nav scroll, active highlighting, and hamburger JS` |
| 4 | Projects section HTML + CSS | `feat: add projects section with Gyanmarg and Pratyaksha cards` |
| 5 | Verify + deploy | push to master → auto-deploy |
