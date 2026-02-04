# Session Log: any.holdings Website Creation

**Date:** February 3, 2026
**Project:** any.holdings - Armitage & York Holdings LLC corporate website

---

## Context

Created a static website for Armitage & York Holdings LLC (any.holdings) to establish a web presence for the holding company. The site is needed to support an organizational software signing certificate application.

Organization details were sourced from documents in `C:\Users\acont\OneDrive\Documents\_DO NOT DELETE!\2. Armitage & York Holdings`.

### Organization Summary

- **Entity:** Armitage & York Holdings LLC
- **Type:** Wyoming Series LLC (formed July 12, 2019)
- **Registered Address:** 1309 Coffeen Avenue STE 1200, Sheridan, WY 82801
- **Registered Agent:** Cloud Peak Law, LLC
- **Sole Member/Manager:** Anthony Conte
- **Parent EIN:** 99-3726584
- **Series 1 (DocSort AI):** Desktop doc-sorting app (.NET 8, local AI). EIN 41-3996594.
- **Series 2 (PlanReviews AI):** SaaS plan review platform (Next.js, cloud AI). EIN pending.
- **Contact:** info@any.holdings

---

## What Was Done

### 1. Created static site files
- `index.html` - Homepage with hero, about, portfolio (DocSort AI + PlanReviews AI), contact
- `privacy.html` - Full privacy policy
- `terms.html` - Full terms of service
- `style.css` - Styling

### 2. Set up GitHub repo & Pages deployment
- Initialized git repo at `C:\src-personal\anyholdings`
- Remote: `git@github.com:aconte1975/anyholdings.git` (user created the repo manually)
- GitHub Actions workflow at `.github/workflows/deploy.yml` for auto-deploy to GitHub Pages
- Installed `gh` CLI via winget, authenticated via device flow
- Enabled GitHub Pages with Actions build source
- Custom domain `any.holdings` configured in Pages settings

### 3. Design iterations
- **v1 (730e9b6):** Basic, minimal design with Inter font. Stark white/gray palette.
- **v2 (2baad02):** Modern redesign with dark hero, gradient accents, SVG icons, card tags. Had layout/alignment bugs (portfolio heading flush left, grids collapsing to single columns).
- **v3 (f35cd8a):** Fixed all layout issues by switching to `.container` wrapper pattern, explicit `1fr 1fr` grids, `<span>` for section labels. Also changed to DM Sans/Serif fonts and warm color palette.
- **v4 (878ea4d - CURRENT):** Reverted fonts back to Inter (user preferred it) while preserving the layout fixes and warm color palette from v3.

### Key layout fixes (v3):
- All sections use `<div class="container">` for consistent max-width centering
- Section labels changed from `<p>` to `<span>` to avoid paragraph style conflicts
- Grids use explicit `grid-template-columns: 1fr 1fr` instead of `auto-fit minmax()`
- Card descriptions use `.card-desc` class to avoid generic `p` rule collisions

---

## Remaining TODO (for user)

1. **DNS:** Configure Squarespace DNS for `any.holdings` pointing to GitHub Pages IPs:
   - A records: 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153
2. **HTTPS:** Enable "Enforce HTTPS" in GitHub Pages settings once DNS propagates
3. **Code signing cert:** Apply with CA using organization details matching Wyoming SOS records

---

## Tech Stack

- Plain HTML/CSS (no framework)
- Inter font (Google Fonts)
- GitHub Pages hosting
- GitHub Actions deployment
- SSH auth to GitHub (`git@github.com:aconte1975`)
- `gh` CLI installed via winget during session

---

## Session: February 4, 2026 - Exactio Labs & Infrastructure Reorganization

### Context

Created Exactio Labs page as the technology operations DBA for the parent LLC. Exactio Labs provides shared infrastructure (GitHub, Cloudflare, dev resources) to portfolio companies. Also reorganized repo ownership and domain hosting.

### What Was Done

#### 1. Created Exactio Labs pages
- `exactio.html` - Full landing page with hero, about, services (6 cards), portfolio (DocSort AI + PlanReviews AI), contact
- `exactio-privacy.html` - Privacy policy branded for Exactio Labs
- `exactio-terms.html` - Terms of service branded for Exactio Labs
- Added Exactio-specific styles to `style.css` (cyan/sky-blue accent color, distinct hero gradient)

#### 2. Updated any.holdings main page
- Removed individual portfolio company cards (DocSort AI, PlanReviews AI)
- Replaced with "Operations" section linking to exactio.ai
- Added Exactio Labs link to footer

#### 3. Repository transfers
- Transferred repos from `aconte1975` to `anyholdings` GitHub account:
  - `anyholdings/anyholdings` (was `aconte1975/anyholdings`)
  - `anyholdings/docsort`
  - `anyholdings/planreviews`
- Updated local git remote to `git@github.com:anyholdings/anyholdings.git`
- Added GitHub Pro to `anyholdings` account (required for private repo Pages)

#### 4. Domain/hosting configuration
| Domain | Hosting | Repo/Service |
|--------|---------|--------------|
| any.holdings | GitHub Pages | `anyholdings/anyholdings` |
| docsort.ai | GitHub Pages | `anyholdings/docsort` |
| planreviews.ai | Vercel | `anyholdings/planreviews` |
| exactio.ai | Cloudflare redirect | → `any.holdings/exactio.html` |

#### 5. Cloudflare redirect setup for exactio.ai
- DNS: A record `@` → `192.0.2.1` (proxied), CNAME `www` → `exactio.ai` (proxied)
- Redirect rule: All incoming requests → `https://any.holdings/exactio.html` (301)

### Exactio Labs Services (as listed on page)
- Cloud Infrastructure (Cloudflare, cloud providers)
- Development Tooling (GitHub org, CI/CD, code review)
- Security & Compliance (policies, access management, scanning)
- DevOps & Automation (deployment, IaC, monitoring)
- Platform Services (SaaS subscriptions, AI/ML access, APIs)
- Domain & DNS (registration, SSL, email infrastructure)

### Design Notes
- Exactio Labs uses distinct-but-related branding:
  - Primary accent: `#0ea5e9` (sky blue) vs main site's `#0d9488` (teal)
  - Gradient: sky-blue → indigo
  - Hero: deeper navy-to-blue gradient
  - Same typography (Inter), layout patterns, warm backgrounds
