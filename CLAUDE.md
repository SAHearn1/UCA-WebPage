# CLAUDE.md — UCA-WebPage (RootWork Framework)

## Project Identity

- **Organization:** Urban Christian Academy (UCA) x Community Exceptional Children's Services (CECS)
- **Project:** RootWork Framework — "From Garden to Growth"
- **GitHub:** `SAHearn1/UCA-WebPage`
- **Live URL:** `https://uca-web-page.vercel.app`
- **Hosting:** Vercel (static deployment, no build step)
- **Location:** 4560 ACL Boulevard, Savannah, Georgia 31405

---

## Related Repository

A React/TypeScript companion app exists at `SAHearn1/SAHearn1-UCA-WebPage`:
- **Stack:** React 19 + Vite + TypeScript + Firebase 12 + Lucide React + Google Gemini
- **Live URL:** `https://sa-hearn1-uca-web-page.vercel.app`
- **Purpose:** Full portal with auth, enrollment wizard, parent dashboard, Stripe payments, agent orchestrator
- **Relationship:** This static site (UCA-WebPage) is the public-facing marketing/enrollment site. The companion app is the authenticated operational portal.
- **Firebase project:** `urban-christian-academy-20a7f` (real project — no longer placeholder)
- **Status:** Fully deployed. All env vars set in Vercel. Firebase rules live. Both parent and staff portals operational.

### Companion App Features (as of Feb 2026)
- Firebase Auth (email/password + Google sign-in) with role-based routing
- Dual-flow enrollment wizard: Parent (6-step) + Staff/Clinical (3-step)
- Parent dashboard: enrollment status, documents, payments, communication
- Staff dashboard: enrollment queue, approve/reject/waitlist, student roster, caseload management
- Firestore security rules deployed with staff/admin access controls
- Stripe payment integration (live keys)
- Audit logging on all enrollment state changes
- 15 env vars configured in Vercel for production

---

## Architecture — This Repo

```
UCA-WebPage/
├── index.html          # Single-page static site (HTML + inline JS)
├── styles.css          # External stylesheet (extracted from inline)
├── vercel.json         # Security headers, caching rules
├── favicon.svg         # Custom UCA favicon (gold circle + "UCA" text)
├── sitemap.xml         # SEO sitemap
├── robots.txt          # Crawler directives
├── .gitignore          # *.zip, node_modules, .env, .DS_Store, logs
├── .github/workflows/
│   ├── security.yml    # 12h cron security scanning (OWASP ZAP, SSL, headers)
│   └── html-check.yml  # Push: Nu HTML checker, Lighthouse CI, link check
├── CLAUDE.md           # This file — project docs & task tracking
└── README.md           # Deployment instructions
```

### Tech Stack
- **Pure HTML/CSS/JS** — no framework, no build, no dependencies
- **Fonts:** Playfair Display (headings), DM Sans (body), Cormorant Garamond (editorial)
- **Colors:** Forest green (#1B3A20), Gold (#C6973F), Cream (#FAF6F0), Bark/Soil browns
- **JS:** IntersectionObserver scroll reveals, nav scroll effect, smooth anchor scrolling, mobile nav toggle
- **Mobile:** Responsive at 900px breakpoint with hamburger menu
- **Form:** FormSubmit.co (AJAX submission to info@rootworkframework.com)

### Deployment
- Push to `main` → Vercel auto-deploys
- No build command needed (static HTML)
- Security headers configured in `vercel.json`
- Two GitHub Actions workflows run on push

---

## Design System

### Color Tokens (CSS Custom Properties)
| Token | Hex | Usage |
|-------|-----|-------|
| `--forest` | `#1B3A20` | Primary dark green, nav, hero bg |
| `--forest-mid` | `#2D5A34` | Secondary green |
| `--sage` | `#5B7F5E` | Section labels, badges |
| `--leaf` | `#3D8B37` | Accent green, progress bars |
| `--cream` | `#FAF6F0` | Page background |
| `--cream-warm` | `#F5EDE0` | Alternate section bg |
| `--gold` | `#C6973F` | CTAs, highlights, brand accent |
| `--gold-light` | `#E8D5A8` | Hover states, hero text |
| `--bark` | `#5C4033` | Earthy accent |
| `--soil` | `#3E2723` | Footer bg, deep dark |
| `--sky-deep` | `#2C5F6E` | Teal accent |

### Typography
| Font | Role | Weights |
|------|------|---------|
| Playfair Display | Headings, brand, hero titles | 400, 600, 700 (+ italic) |
| DM Sans | Body text, nav, UI | 300–700 (+ italic) |
| Cormorant Garamond | Editorial intros, quotes | 400, 500, 600 (+ italic) |

### Component Patterns
- **Section structure:** `.section` > `.section-container` > `.section-label` + `.section-title` + `.section-intro`
- **Cards:** Border-radius 16px, subtle border, hover lift + shadow
- **Buttons:** `.btn-primary` (gold bg), `.btn-secondary` (transparent + border)
- **Animations:** `.reveal` class with IntersectionObserver, delay classes `.reveal-delay-1` through `-5`

---

## Page Sections (in DOM order)

| # | Section | ID | Content |
|---|---------|-----|---------|
| 1 | Navigation | `#nav` | Fixed top bar, brand, links, Portal link, mobile hamburger |
| 2 | Announcement | — | Summer Camp 2026 countdown (opens March 1) |
| 3 | Hero | `#main-content` | "From Garden to Growth", stats bar |
| 4 | About / Framework | `#about` | 4 pillars + animated cycle ring |
| 5 | Video | `#vision` | "The Vision" — video placeholder (coming soon) |
| 6 | Programs | `#programs` | 6 program cards + portal callout |
| 7 | Summer Camp | `#summer` | Feature section, pricing, capacity, countdown |
| 8 | Scholarships | `#scholarships` | 3 GA scholarship pathways with external links |
| 9 | Services | `#services` | 6 support services list |
| 10 | Testimonials | `#testimonials` | 3 testimonial cards (parent, educator, parent) |
| 11 | Trust | `#trust` | 6 credential/compliance cards |
| 12 | Gallery | `#gallery` | 5 Unsplash images with lazy loading |
| 13 | CTA / Enroll | `#enroll` | UCA contact info + enrollment inquiry form (FormSubmit.co) |
| 14 | Footer | — | Brand, copyright |

---

## Current Status — Phases 1–6 Complete (Updated Feb 2026)

All foundational work is done. The static site is production-ready, deployed, and live at `https://uca-web-page.vercel.app`.

### What's been completed

| Phase | Summary |
|-------|---------|
| **1 — Critical Fixes** | Mobile nav toggle with ARIA, meta description + OG/Twitter tags, favicon (SVG), .gitignore, ZIP removed |
| **2 — Functional** | Enrollment form (FormSubmit.co with validation), Portal link in nav + programs callout, Summer Camp section with countdown, scholarship external links, fg2g-rwfw.com link |
| **3 — Accessibility** | Skip-to-content link, WCAG AA color contrast, ARIA landmarks/labels on nav + cycle ring + footer, `:focus-visible` styles with gold accent |
| **4 — Performance/SEO** | CSS extracted to `styles.css`, JSON-LD (EducationalOrganization + Event), sitemap.xml + robots.txt, Playfair Display 700 preloaded, `body::before` z-index fixed to 1 |
| **5 — Content** | Hero + about images, 5-image photo gallery (Unsplash, lazy loaded), 3 testimonial cards, video placeholder, contact info updated to UCA org branding |
| **6 — Infrastructure** | Security headers (CSP, HSTS, X-Frame-Options, etc.), Vercel Analytics script, 2 GitHub Actions (security scan 12h cron + HTML/Lighthouse/link check), .gitignore |
| **Post-Phase** | Nav brand logo fix (scrolls to hero), video placeholder improved with description |

### Security posture
- X-Content-Type-Options: nosniff
- X-Frame-Options: DENY
- X-XSS-Protection: 1; mode=block
- Referrer-Policy: strict-origin-when-cross-origin
- Permissions-Policy: camera=(), microphone=(), geolocation=()
- Content-Security-Policy: strict (self + fonts.googleapis.com + formsubmit.co)
- Strict-Transport-Security: 31536000 (1 year)
- OWASP ZAP baseline scan every 12 hours

---

## Remaining Tasks

### Static Site — Actionable Now

- [ ] **T-1 — Embed "The Vision" video**
  - Replace the placeholder in `#vision` section with a real YouTube/Vimeo embed
  - Use `loading="lazy"` on the iframe
  - Requires: actual video URL from Dr. Hearn

- [ ] **T-2 — Verify FormSubmit email**
  - FormSubmit.co endpoint changed to `info@rootworkframework.com`
  - First form submission triggers a verification email — must be confirmed before forwarding works
  - Action: submit a test form, then check inbox for verification link

- [ ] **T-3 — Configure custom domain**
  - Site is at `uca-web-page.vercel.app` — needs a real domain
  - Configure in Vercel → Settings → Domains, set DNS records
  - After setup: update canonical URL and OG tags in `index.html`

### Companion Portal — FULLY DEPLOYED (Feb 2026)

- [x] **T-4 — Firebase config** — All config values retrieved from Firebase API, `.env.local` complete
- [x] **T-5 — Environment variables** — All 15 vars set in both `.env.local` and Vercel production
- [x] **T-6 — vercel.json** — Security headers (CSP, HSTS, X-Frame-Options) + SPA rewrite rules
- [x] **T-7 — CLAUDE.md** — Full project docs with architecture, roles, build phases, dev workflow
- [x] **Auth & Role Infrastructure** — AuthModal with role selection, Firestore rules, role-based routing
- [x] **Staff Portal** — Dashboard, enrollment queue, detail view, student roster, caseload management
- [x] **Parent Portal** — Multi-student enrollment, guardian address/relationship, "New Enrollment" button
- [x] **Staff Onboarding** — Dual-flow wizard with StepProfessionalInfo + StepStaffReview, `staffOnboarding` collection
- [x] **Audit Logging** — logActivity wired into all enrollment + staff state changes
- [x] **Firestore Rules** — Deployed to production with staff/admin access + staffOnboarding collection
- [x] **Build Verified** — TypeScript passes, Vite production build clean

### Phase 7 — Future Enhancements

- [ ] **T7.1 — Dark mode toggle**
  - Add `prefers-color-scheme` media query support
  - Optional: manual toggle in nav

- [ ] **T7.2 — Multi-language support**
  - English/Spanish if the school serves multilingual families

- [ ] **T7.3 — Convert to Next.js or Astro**
  - Only if the site grows beyond a single page

- [ ] **T7.4 — Deeper portal integration**
  - Shared auth between marketing site and portal
  - Embedded enrollment wizard or unified navigation

- [ ] **T7.5 — Blog or news section**
  - Headless CMS (Notion, Sanity, Contentful) for content management

- [ ] **T7.6 — Print stylesheet**
  - Hide nav, footer, animations; optimize for A4/Letter

---

## Development Workflow

### Local Development
```bash
# This is a static site — just open index.html in a browser
# Or use a local server:
npx serve .
# Or with Python:
python -m http.server 8000
```

### Making Changes
1. Edit `index.html` and/or `styles.css`
2. Test locally in browser (check both desktop and mobile viewport)
3. Commit and push to `main` — Vercel auto-deploys

### Commit Conventions
- Use descriptive messages: `fix: mobile nav toggle`, `feat: add enrollment form`, `style: extract CSS`
- Keep commits focused — one logical change per commit

### Testing Checklist (before pushing)
- [ ] Desktop layout renders correctly (1200px+)
- [ ] Mobile layout renders correctly (375px)
- [ ] All nav links scroll to correct sections
- [ ] Mobile hamburger menu opens/closes
- [ ] All buttons and links work
- [ ] No console errors
- [ ] Page loads in under 3 seconds

---

## Contact & Credentials

| Field | Value |
|-------|-------|
| **Organization** | Urban Christian Academy (UCA) |
| **Email** | info@rootworkframework.com |
| **Phone** | (301) 219-2728 |
| **Address** | 4560 ACL Boulevard, Savannah, GA 31405 |
| **GitHub** | SAHearn1 |
| **Vercel Team** | shawns-projects-5cde83d1 |
