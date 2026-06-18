# Modernize Portfolio Website — Design Spec

**Date**: 2026-06-18  
**Branch**: `modernize-portfolio`  
**Status**: Approved

## Overview

Modernize the GitHub Pages portfolio at `agungmohmd.github.io` by upgrading from Bootstrap 4.5/jQuery to Bootstrap 5.3/vanilla JS, refreshing the visual design to a blue/teal/slate palette, and adding data from Mohammad Agung Perdana's CV without removing any existing content.

## Architecture & Tech Stack

- **CSS**: Bootstrap 5.3 via CDN + custom `styles.css` (replaces bundled Bootstrap 4.5)
- **JS**: Vanilla JavaScript (no jQuery, no jQuery Easing)
- **Smooth scroll**: CSS `scroll-behavior: smooth` + `IntersectionObserver` for scrollspy
- **Icons**: Font Awesome 6.2 (keep existing CDN)
- **Fonts**: Inter (body) + Saira Extra Condensed (headings, keep) via Google Fonts
- **Structure**: Single `index.html` (GitHub Pages compatible)

## Visual Design

### Color Palette

| Role | Color | Hex | Usage |
|---|---|---|---|
| Primary accent | Blue | `#2563eb` | Headlines, links, active nav |
| Secondary accent | Sky blue | `#0ea5e9` | Highlights, badges, hover states |
| Teal accent | Teal | `#14b8a6` | Section dividers, skill indicators |
| Dark background | Slate-900 | `#0f172a` | Sidebar nav background, dark mode |
| Light background | Slate-50 | `#f8fafc` | Page background in light mode |
| Text primary | Slate-800 | `#1e293b` | Body text light mode |
| Text muted | Slate-500 | `#64748b` | Secondary text |
| Dark mode text | White | `#ffffff` | Body text dark mode |

### Typography
- Headings: Saira Extra Condensed (keep existing)
- Body: Inter (new, replaces Muli)
- Monospace: System default for code/tool references

### Components
- **Sidebar nav**: Dark slate (`#0f172a`) background with blue accent on active
- **Cards**: Rounded corners (`0.5rem`), soft shadows, light borders
- **Experience items**: Left blue accent border
- **Skill cards**: 4 categorized cards with icon + text

### Dark/Light Mode
- Toggle in nav sidebar
- Persisted via `localStorage`
- Default: light mode (or system preference via `prefers-color-scheme`)

## Content Changes

### About Section
- Add professional headline below name: "Senior Customer Success Specialist | Technical Solution Architect"
- Update phone: `+6281375675615`
- Keep existing about paragraph, address, email, social icons

### Experience Section
- Add Yellow.ai role at the TOP (most recent):
  - Title: Senior Customer Success Engineer
  - Company: Yellow.ai
  - Period: October 2023 – January 2026
  - Description: Managed 12+ enterprise accounts, drove 20-30% faster implementations, maintained majority renewal/expansion rate, resolved escalations, translated requirements into technical specs
- Keep all 9 existing experience entries intact below

### Skills Section
Merge existing icon grid into 4 categorized cards:

1. **Customer Success & Account Management**: Stakeholder Management, Client Onboarding, Account Health Monitoring, Churn Prevention, Upsell & Renewal, Escalation Management, SLA Management, NPS/CSAT
2. **Project & Delivery**: Agile & Scrum, SDLC, Requirement Analysis, Sprint Planning, UAT Coordination, Risk Management, Technical Documentation
3. **Technical Proficiency**: Existing programming icons (Go, Docker, JavaScript, Node.js, HTML5, CSS3, Angular, Vue.js, npm, PHP, Laravel, Database, Server, Linux, Git) + RESTful & SOAP APIs, System Integration, SQL, Postman, Jira/Trello, Conversational AI Platforms
4. **Domain Knowledge**: B2B SaaS, Enterprise Software, Conversational AI, ERP/HRIS, Fintech, B2B Marketplace

### Unchanged Sections
- Education (both entries)
- Interests (all text)
- Portfolio carousel (all 13 slides, all images, all captions)

## Implementation Plan

1. Create branch `modernize-portfolio`
2. Replace CSS: Bootstrap 5.3 CDN + new custom `styles.css` with blue/teal/slate palette
3. Replace JS: Vanilla JS rewrite of `scripts.js` (scrollspy, smooth scroll, dark mode toggle)
4. Update HTML: add Yellow.ai role, headline, phone, skill cards
5. Remove jQuery + Bootstrap 4 dependencies
6. Test locally

## Constraints
- Do NOT work on master branch
- Do NOT push
- Do NOT remove any existing data
- Single HTML file (GitHub Pages compatible)
