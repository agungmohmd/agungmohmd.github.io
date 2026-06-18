# Modernize Portfolio Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Upgrade the GitHub Pages portfolio from Bootstrap 4.5/jQuery to Bootstrap 5.3/vanilla JS with blue/teal/slate palette, add CV data, dark mode toggle.

**Architecture:** Single `index.html` with Bootstrap 5.3 CDN, custom `styles.css` for theme, vanilla JS `scripts.js` for interactivity (scrollspy, smooth scroll, dark mode). Single-page responsive layout with fixed sidebar nav.

**Tech Stack:** Bootstrap 5.3 CDN, Font Awesome 6.2 CDN, Google Fonts (Inter + Saira Extra Condensed), vanilla JavaScript, CSS custom properties for theming.

---

## File Structure

| File | Action | Responsibility |
|---|---|---|
| `index.html` | Heavy modify | Page structure, sections, content |
| `css/styles.css` | Rewrite | Bootstrap 5.3 theme, color system, dark mode, layout |
| `js/scripts.js` | Rewrite | Vanilla JS scrollspy, smooth scroll, dark mode toggle, nav collapse |
| `assets/` | No change | Images, favicon — untouched |

---

### Task 1: Replace CSS — Bootstrap 5.3 base + custom theme

**Files:**
- Modify: `css/styles.css` (full rewrite)

- [ ] **Step 1: Rewrite styles.css**

Replace the current 10,000+ line file (Bootstrap 4.5 bundled) with a clean custom stylesheet. This file will contain only custom styles since Bootstrap 5.3 CSS will be loaded from CDN.

```css
@charset "UTF-8";

:root {
  --bs-primary: #2563eb;
  --bs-primary-rgb: 37, 99, 235;
  --bs-secondary: #0ea5e9;
  --bs-teal: #14b8a6;
  --bs-dark: #0f172a;
  --bs-dark-rgb: 15, 23, 42;
  --bs-light: #f8fafc;
  --bs-body-color: #1e293b;
  --bs-body-bg: #f8fafc;
  --bs-body-font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  --bs-heading-font-family: 'Saira Extra Condensed', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  --bs-border-radius: 0.5rem;
  --bs-border-radius-lg: 0.75rem;
  --sidebar-width: 17rem;
  --transition-speed: 0.3s;
}

[data-bs-theme="dark"] {
  --bs-body-color: #e2e8f0;
  --bs-body-bg: #0f172a;
  --bs-light: #1e293b;
  --bs-dark: #f8fafc;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: var(--bs-body-font-family);
  color: var(--bs-body-color);
  background-color: var(--bs-body-bg);
  padding-top: 0;
  overflow-x: hidden;
}

h1, h2, h3, h4, h5, h6 {
  font-family: var(--bs-heading-font-family);
  font-weight: 700;
  text-transform: uppercase;
  color: var(--bs-body-color);
}

a {
  color: var(--bs-primary);
  transition: color var(--transition-speed) ease;
}
a:hover {
  color: var(--bs-secondary);
}

.text-primary { color: var(--bs-primary) !important; }

/* Sidebar Navigation */
#sideNav {
  position: fixed;
  top: 0;
  left: 0;
  width: var(--sidebar-width);
  height: 100vh;
  background-color: var(--bs-dark);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  z-index: 1030;
  border-right: 1px solid rgba(255, 255, 255, 0.1);
}
#sideNav .navbar-brand {
  display: flex;
  flex-direction: column;
  align-items: center;
}
#sideNav .navbar-brand .img-profile {
  max-width: 10rem;
  max-height: 10rem;
  border: 0.5rem solid rgba(255, 255, 255, 0.1);
}
#sideNav .navbar-nav {
  flex-direction: column;
  width: 100%;
}
#sideNav .navbar-nav .nav-link {
  font-weight: 600;
  letter-spacing: 0.05rem;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.55);
  padding: 0.5rem 1rem;
  transition: color var(--transition-speed) ease;
}
#sideNav .navbar-nav .nav-link:hover,
#sideNav .navbar-nav .nav-link.active {
  color: var(--bs-primary);
}
#sideNav .navbar-toggler {
  display: none;
}

/* Dark mode toggle */
#themeToggle {
  background: transparent;
  border: 1px solid rgba(255, 255, 255, 0.3);
  color: rgba(255, 255, 255, 0.7);
  border-radius: 50%;
  width: 2.5rem;
  height: 2.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all var(--transition-speed) ease;
}
#themeToggle:hover {
  color: var(--bs-primary);
  border-color: var(--bs-primary);
}

/* Main content area */
.container-fluid.p-0 {
  padding-left: var(--sidebar-width);
}

.resume-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 5rem 3rem;
  border-bottom: 1px solid rgba(0, 0, 0, 0.08);
}
[data-bs-theme="dark"] .resume-section {
  border-bottom-color: rgba(255, 255, 255, 0.08);
}
.resume-section:last-of-type {
  border-bottom: none;
}
.resume-section-content {
  max-width: 75rem;
  width: 100%;
}

/* Section headings */
.resume-section h2.mb-5 {
  font-size: 3.5rem;
  margin-bottom: 3rem !important;
}
.resume-section h3.mb-0 {
  font-size: 1.75rem;
}

.subheading {
  font-family: var(--bs-heading-font-family);
  font-weight: 500;
  font-size: 1.5rem;
  text-transform: uppercase;
  color: var(--bs-body-color);
  opacity: 0.7;
}

/* Experience items */
.experience-item {
  position: relative;
  padding-left: 1.5rem;
  border-left: 3px solid var(--bs-primary);
  margin-bottom: 3rem;
}
.experience-item p {
  margin-bottom: 0.25rem;
}

/* Skill cards */
.skill-card {
  background: var(--bs-body-bg);
  border: 1px solid rgba(0, 0, 0, 0.08);
  border-radius: var(--bs-border-radius-lg);
  padding: 1.5rem;
  height: 100%;
  transition: transform var(--transition-speed) ease, box-shadow var(--transition-speed) ease;
}
.skill-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
}
[data-bs-theme="dark"] .skill-card {
  border-color: rgba(255, 255, 255, 0.08);
  background: var(--bs-light);
}
[data-bs-theme="dark"] .skill-card:hover {
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
}
.skill-card h4 {
  font-size: 1.25rem;
  color: var(--bs-primary);
  margin-bottom: 1rem;
}
.skill-card .skill-tag {
  display: inline-block;
  background: var(--bs-primary);
  color: #fff;
  padding: 0.2rem 0.6rem;
  border-radius: 0.25rem;
  font-size: 0.8rem;
  margin: 0.15rem 0.25rem 0.15rem 0;
}
.skill-card .dev-icons {
  margin-top: 0.5rem;
}
.skill-card .dev-icons .list-inline-item {
  font-size: 1.5rem;
  color: var(--bs-body-color);
  margin-right: 0.75rem;
  margin-bottom: 0.5rem;
  transition: color var(--transition-speed) ease;
}
.skill-card .dev-icons .list-inline-item:hover {
  color: var(--bs-primary);
}

/* Social icons */
.social-icons .social-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 3.5rem;
  height: 3.5rem;
  border-radius: 50%;
  background-color: var(--bs-dark);
  color: #fff;
  font-size: 1.5rem;
  margin-right: 1rem;
  transition: background-color var(--transition-speed) ease;
}
.social-icons .social-icon:hover {
  background-color: var(--bs-primary);
  color: #fff;
  text-decoration: none;
}

/* Carousel */
.carousel {
  border-radius: var(--bs-border-radius);
  overflow: hidden;
}
.carousel-caption {
  background: rgba(0, 0, 0, 0.65);
  border-radius: 0.5rem;
  padding: 1rem;
}
.carousel-caption h5 {
  color: #fff;
  text-transform: none;
}
.carousel-caption p {
  color: var(--bs-secondary);
}

/* Divider */
hr.m-0 {
  margin: 0;
  border: 0;
  border-top: 1px solid rgba(0, 0, 0, 0.08);
}
[data-bs-theme="dark"] hr.m-0 {
  border-top-color: rgba(255, 255, 255, 0.08);
}

/* Responsive */
@media (max-width: 991.98px) {
  #sideNav {
    position: relative;
    width: 100%;
    height: auto;
    flex-direction: row;
    justify-content: space-between;
    padding: 0.75rem 1rem;
    border-right: none;
  }
  #sideNav .navbar-brand .img-profile {
    display: none;
  }
  #sideNav .navbar-nav {
    flex-direction: column;
  }
  #sideNav .navbar-toggler {
    display: block;
    background: rgba(255, 255, 255, 0.1);
    border: none;
  }
  .container-fluid.p-0 {
    padding-left: 0;
  }
  .resume-section {
    padding: 3rem 1.5rem;
    min-height: auto;
  }
  .resume-section h2.mb-5 {
    font-size: 2.5rem;
  }
}

@media (min-width: 992px) {
  .resume-section {
    padding: 5rem 3rem;
  }
}
```

- [ ] **Step 2: Verify file is correctly written**

Run: `Get-Content css/styles.css | Measure-Object -Line`
Expected: Clean CSS file (no Bootstrap 4 remnants)

- [ ] **Step 3: Commit**

```bash
git add css/styles.css
git commit -m "style: replace Bootstrap 4 CSS with Bootstrap 5.3 custom theme"
```

---

### Task 2: Rewrite scripts.js — vanilla JS

**Files:**
- Modify: `js/scripts.js` (full rewrite)

- [ ] **Step 1: Rewrite scripts.js**

Replace the jQuery-based scroll and scrollspy with vanilla JS. Add dark mode toggle with localStorage persistence.

```javascript
(function () {
  'use strict';

  const sideNav = document.getElementById('sideNav');
  const navLinks = document.querySelectorAll('#sideNav .nav-link');
  const sections = document.querySelectorAll('.resume-section');
  const themeToggle = document.getElementById('themeToggle');

  function initTheme() {
    const saved = localStorage.getItem('theme');
    const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
    if (saved === 'dark' || (!saved && prefersDark)) {
      document.documentElement.setAttribute('data-bs-theme', 'dark');
      if (themeToggle) {
        themeToggle.innerHTML = '<i class="fas fa-sun"></i>';
        themeToggle.title = 'Switch to light mode';
      }
    }
  }

  if (themeToggle) {
    themeToggle.addEventListener('click', function () {
      const current = document.documentElement.getAttribute('data-bs-theme');
      if (current === 'dark') {
        document.documentElement.removeAttribute('data-bs-theme');
        localStorage.setItem('theme', 'light');
        themeToggle.innerHTML = '<i class="fas fa-moon"></i>';
        themeToggle.title = 'Switch to dark mode';
      } else {
        document.documentElement.setAttribute('data-bs-theme', 'dark');
        localStorage.setItem('theme', 'dark');
        themeToggle.innerHTML = '<i class="fas fa-sun"></i>';
        themeToggle.title = 'Switch to light mode';
      }
    });
  }

  navLinks.forEach(function (link) {
    link.addEventListener('click', function (e) {
      e.preventDefault();
      var target = document.querySelector(this.getAttribute('href'));
      if (target) {
        target.scrollIntoView({ behavior: 'smooth' });
      }
      var collapse = document.querySelector('.navbar-collapse.show');
      if (collapse) {
        collapse.classList.remove('show');
      }
    });
  });

  var observerOptions = { rootMargin: '-50% 0px -50% 0px' };
  var observer = new IntersectionObserver(function (entries) {
    entries.forEach(function (entry) {
      if (entry.isIntersecting) {
        navLinks.forEach(function (link) {
          link.classList.remove('active');
          if (link.getAttribute('href') === '#' + entry.target.id) {
            link.classList.add('active');
          }
        });
      }
    });
  }, observerOptions);

  sections.forEach(function (section) {
    observer.observe(section);
  });

  initTheme();
})();
```

- [ ] **Step 2: Commit**

```bash
git add js/scripts.js
git commit -m "refactor: replace jQuery with vanilla JS, add dark mode toggle"
```

---

### Task 3: Update index.html — structure, CDN links, and new content

**Files:**
- Modify: `index.html`

This is the largest task. We'll update the `<head>`, navigation, add the Yellow.ai role, add the professional headline, update the phone, restructure the skills section, and switch to Bootstrap 5 markup.

- [ ] **Step 1: Update the `<head>` section**

Replace the `<head>` content (lines 1-19) with Bootstrap 5.3 CDN and Inter font.

Current lines 1-19 become:

```html
<!DOCTYPE html>
<html lang="en" data-bs-theme="light">

<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />
    <meta name="description" content="Portfolio of Mohammad Agung Perdana - Senior Customer Success Specialist & Technical Solution Architect" />
    <meta name="author" content="Mohammad Agung Perdana" />
    <title>Mohammad Agung Perdana — Portfolio</title>
    <link rel="icon" type="image/x-icon" href="assets/img/favicon.ico" />
    <script src="https://use.fontawesome.com/releases/v6.2.0/js/all.js" crossorigin="anonymous"></script>
    <link href="https://fonts.googleapis.com/css?family=Saira+Extra+Condensed:500,700" rel="stylesheet" type="text/css" />
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" />
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" />
    <link href="css/styles.css" rel="stylesheet" />
</head>
```

- [ ] **Step 2: Update the sidebar navigation**

Replace the nav (lines 22-42) with Bootstrap 5 markup. Add dark mode toggle button inside the nav. Use `data-bs-toggle`, `data-bs-target` (Bootstrap 5 syntax).

Replace lines 22-42 with:

```html
    <nav class="navbar navbar-expand-lg navbar-dark fixed-top" id="sideNav">
        <a class="navbar-brand" href="#page-top">
            <span class="d-block d-lg-none">Mohammad Agung Perdana</span>
            <span class="d-none d-lg-block"><img class="img-fluid img-profile rounded-circle mx-auto mb-2"
                    src="assets/img/profilepict.jpg" alt="Mohammad Agung Perdana" /></span>
        </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation"><span
                class="navbar-toggler-icon"></span></button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav">
                <li class="nav-item"><a class="nav-link active" href="#about">About</a></li>
                <li class="nav-item"><a class="nav-link" href="#experience">Experience</a></li>
                <li class="nav-item"><a class="nav-link" href="#education">Education</a></li>
                <li class="nav-item"><a class="nav-link" href="#skills">Skills</a></li>
                <li class="nav-item"><a class="nav-link" href="#interests">Interests</a></li>
                <li class="nav-item"><a class="nav-link" href="#portfolio">Portfolio</a></li>
            </ul>
        </div>
        <button id="themeToggle" title="Switch to dark mode" class="mt-3"><i class="fas fa-moon"></i></button>
    </nav>
```

- [ ] **Step 3: Update the About section**

Replace lines 46-71 (the about section). Add the professional headline and update the phone number.

```html
        <section class="resume-section" id="about">
            <div class="resume-section-content">
                <h1 class="mb-0">
                    Mohammad
                    <span class="text-primary">Agung</span>
                    Perdana
                </h1>
                <div class="subheading mb-3">Senior Customer Success Specialist | Technical Solution Architect</div>
                <div class="mb-5">
                    Jl. Swadaya No. 53 · Jakarta Barat, DKI Jakarta 11480 · (+62) 813-75675615 ·
                    <a href="mailto:mohmd.agung@gmail.com">mohmd.agung@gmail.com</a>
                </div>
                <p class="lead mb-5">Customer-focused IT professional with 5+ years of experience across software engineering and enterprise customer success. Managed 12+ enterprise accounts at Yellow.ai, where I have driven 20-30% faster implementation timelines and maintained a majority account renewal and expansion rate. Skilled at translating technical complexity into business value, managing escalations, and ensuring long-term client satisfaction.</p>
                <div class="social-icons">
                    <a class="social-icon" href="https://www.linkedin.com/in/agungmohmd/"><i
                            class="fab fa-linkedin-in"></i></a>
                    <a class="social-icon" href="https://github.com/agungmohmd"><i class="fab fa-github"></i></a>
                </div>
            </div>
        </section>
```

- [ ] **Step 4: Add Yellow.ai experience at the TOP of experience section**

Insert after the `<h2 class="mb-5">Experience</h2>` line, before the ADL Indonesia entry. This is the newest role from the CV.

```html
                <div class="experience-item">
                    <div class="d-flex flex-column flex-md-row justify-content-between mb-5">
                        <div class="flex-grow-1">
                            <h3 class="mb-0">Senior Customer Success Engineer</h3>
                            <div class="subheading mb-3">Yellow.ai</div>
                            <p>· Manage 12+ enterprise accounts as primary technical advisor, driving 20-30% reduction in implementation timelines through structured onboarding processes and proactive risk identification.</p>
                            <p>· Achieved majority account renewal and expansion rate (50%+) by consistently aligning solution delivery with client business objectives and maintaining high post-launch satisfaction.</p>
                            <p>· Resolved critical client escalations and prevented churn by coordinating cross-functional teams (engineering, product, QA) to deliver fixes within SLA, preserving key enterprise relationships.</p>
                            <p>· Translated complex client requirements into technical specifications and delivery roadmaps, reducing sprint rework and enabling engineering teams to deliver predictably.</p>
                        </div>
                        <div class="flex-shrink-0"><span class="text-primary">October 2023 - January 2026</span></div>
                    </div>
                </div>
```

- [ ] **Step 5: Wrap all existing experience entries in experience-item divs**

For each existing experience entry (ADL Indonesia through Computer Lab Assistant), wrap the content in `<div class="experience-item">...</div>` and keep the `d-flex flex-column flex-md-row justify-content-between mb-5` inside.

- [ ] **Step 6: Update the Skills section with categorized cards**

Replace the entire skills section (lines 229-270) with:

```html
        <section class="resume-section" id="skills">
            <div class="resume-section-content">
                <h2 class="mb-5">Skills</h2>
                <div class="row g-4">
                    <div class="col-lg-6">
                        <div class="skill-card">
                            <h4><i class="fas fa-users me-2"></i>Customer Success & Account Management</h4>
                            <span class="skill-tag">Stakeholder Management</span>
                            <span class="skill-tag">Client Onboarding</span>
                            <span class="skill-tag">Account Health Monitoring</span>
                            <span class="skill-tag">Churn Prevention</span>
                            <span class="skill-tag">Upsell & Renewal</span>
                            <span class="skill-tag">Escalation Management</span>
                            <span class="skill-tag">SLA Management</span>
                            <span class="skill-tag">NPS/CSAT</span>
                        </div>
                    </div>
                    <div class="col-lg-6">
                        <div class="skill-card">
                            <h4><i class="fas fa-tasks me-2"></i>Project & Delivery</h4>
                            <span class="skill-tag">Agile & Scrum</span>
                            <span class="skill-tag">SDLC</span>
                            <span class="skill-tag">Requirement Analysis</span>
                            <span class="skill-tag">Sprint Planning</span>
                            <span class="skill-tag">UAT Coordination</span>
                            <span class="skill-tag">Risk Management</span>
                            <span class="skill-tag">Technical Documentation</span>
                        </div>
                    </div>
                    <div class="col-lg-6">
                        <div class="skill-card">
                            <h4><i class="fas fa-code me-2"></i>Technical Proficiency</h4>
                            <ul class="list-inline dev-icons mb-3">
                                <li class="list-inline-item"><i class="fa-brands fa-golang"></i></li>
                                <li class="list-inline-item"><i class="fab fa-docker"></i></li>
                                <li class="list-inline-item"><i class="fab fa-js-square"></i></li>
                                <li class="list-inline-item"><i class="fab fa-node-js"></i></li>
                                <li class="list-inline-item"><i class="fab fa-html5"></i></li>
                                <li class="list-inline-item"><i class="fab fa-css3-alt"></i></li>
                                <li class="list-inline-item"><i class="fab fa-angular"></i></li>
                                <li class="list-inline-item"><i class="fab fa-vuejs"></i></li>
                                <li class="list-inline-item"><i class="fab fa-npm"></i></li>
                                <li class="list-inline-item"><i class="fab fa-php"></i></li>
                                <li class="list-inline-item"><i class="fab fa-laravel"></i></li>
                                <li class="list-inline-item"><i class="fas fa-database"></i></li>
                                <li class="list-inline-item"><i class="fas fa-server"></i></li>
                                <li class="list-inline-item"><i class="fab fa-linux"></i></li>
                                <li class="list-inline-item"><i class="fab fa-git"></i></li>
                            </ul>
                            <span class="skill-tag">RESTful & SOAP APIs</span>
                            <span class="skill-tag">System Integration</span>
                            <span class="skill-tag">SQL</span>
                            <span class="skill-tag">Postman</span>
                            <span class="skill-tag">Git</span>
                            <span class="skill-tag">Jira/Trello</span>
                            <span class="skill-tag">Conversational AI Platforms</span>
                        </div>
                    </div>
                    <div class="col-lg-6">
                        <div class="skill-card">
                            <h4><i class="fas fa-building me-2"></i>Domain Knowledge</h4>
                            <span class="skill-tag">B2B SaaS</span>
                            <span class="skill-tag">Enterprise Software</span>
                            <span class="skill-tag">Conversational AI</span>
                            <span class="skill-tag">ERP/HRIS</span>
                            <span class="skill-tag">Fintech</span>
                            <span class="skill-tag">B2B Marketplace</span>
                        </div>
                    </div>
                </div>
            </div>
        </section>
```

- [ ] **Step 7: Update the portfolio section ID**

Change `id="awards"` to `id="portfolio"` on the portfolio section (line 287) to match the nav link.

- [ ] **Step 8: Update carousel for Bootstrap 5**

Replace `data-ride="carousel"` with `data-bs-ride="carousel"`, `data-slide` with `data-bs-slide`, `data-target` with `data-bs-target`, and `data-slide-to` with `data-bs-slide-to` throughout the carousel (lines 292-433).

- [ ] **Step 9: Replace JS dependencies at the bottom**

Replace lines 437-447 with Bootstrap 5.3 JS CDN (no jQuery):

```html
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
    <script src="js/scripts.js"></script>
```

- [ ] **Step 10: Commit**

```bash
git add index.html
git commit -m "feat: upgrade to Bootstrap 5, add CV data, modernize design"
```

---

### Task 4: Final review and verification

**Files:**
- Review: `index.html`, `css/styles.css`, `js/scripts.js`

- [ ] **Step 1: Verify all existing data is preserved**

Open `index.html` and confirm:
- All 9 original experience entries are present
- Both education entries are present
- All interests text is present
- All 13 carousel slides with images exist
- Social links intact

- [ ] **Step 2: Verify new data is added**

Confirm:
- Yellow.ai experience is first in the experience list
- Professional headline is below the name
- Skills section has 4 categorized cards
- Domain Knowledge card exists

- [ ] **Step 3: Verify no Bootstrap 4 artifacts remain**

```bash
rg "data-toggle|data-ride|data-slide-to|data-slide=|jquery" index.html js/scripts.js
```
Expected: No matches

- [ ] **Step 4: Commit final verification**

```bash
git commit -m "chore: final verification, all data preserved" --allow-empty
```
