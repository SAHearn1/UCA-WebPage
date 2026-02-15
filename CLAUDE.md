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
- **Stack:** React 19 + Vite + TypeScript + Firebase + Tailwind + Google Gemini
- **Live URL:** `https://sa-hearn1-uca-web-page.vercel.app`
- **Purpose:** Full portal with auth, dashboard, file vault, caseload mgmt, compliance, agent orchestrator
- **Relationship:** This static site (UCA-WebPage) is the public-facing marketing/enrollment site. The companion app is the authenticated operational portal.

---

## Architecture — This Repo

```
UCA-WebPage/
├── index.html          # Single-file static site (HTML + inline CSS + inline JS)
├── vercel.json         # Security headers (X-Content-Type, X-Frame-Options, XSS)
├── .vercelignore       # Excludes .git, node_modules, README.md, *.log, .DS_Store
├── README.md           # Deploy instructions
└── urban-christian-academy---rootwork-framework.zip  # Original source archive (SHOULD BE REMOVED)
```

### Tech Stack
- **Pure HTML/CSS/JS** — no framework, no build, no dependencies
- **Fonts:** Playfair Display (headings), DM Sans (body), Cormorant Garamond (editorial)
- **Colors:** Forest green (#1B3A20), Gold (#C6973F), Cream (#FAF6F0), Bark/Soil browns
- **JS:** IntersectionObserver scroll reveals, nav scroll effect, smooth anchor scrolling
- **Mobile:** Responsive at 900px breakpoint

### Deployment
- Push to `main` → Vercel auto-deploys
- No build command needed (static HTML)
- Security headers configured in `vercel.json`

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
| 1 | Navigation | `#nav` | Fixed top bar, brand, links, mobile hamburger |
| 2 | Announcement | — | Summer Camp 2026 opens March 1 |
| 3 | Hero | — | "From Garden to Growth", stats bar |
| 4 | About / Framework | `#about` | 4 pillars + animated cycle ring |
| 5 | Programs | `#programs` | 6 program cards |
| 6 | Summer Camp | `#summer` | Feature section, pricing, capacity |
| 7 | Scholarships | `#scholarships` | 3 GA scholarship pathways |
| 8 | Services | `#services` | 6 support services list |
| 9 | Trust | `#trust` | 6 credential/compliance cards |
| 10 | CTA / Enroll | `#enroll` | Contact info, email/phone |
| 11 | Footer | — | Brand, copyright |

---

## Known Issues & Bugs

### Critical
1. **Mobile nav hamburger does not work** — `<button class="nav-toggle">` exists but has NO click handler in JS. On mobile (<900px), nav links are hidden and unreachable.
2. **ZIP file committed to repo** — `urban-christian-academy---rootwork-framework.zip` (103KB) is tracked in git. Should be in `.gitignore` or removed.

### Functional
3. **No form or enrollment flow** — "Enroll Now" and "Begin Your Journey" buttons link to `#enroll` which is just a contact section with email/phone. No intake form exists.
4. **No link to companion portal** — The React app (SAHearn1-UCA-WebPage) has auth/dashboard but this site doesn't link to it.
5. **"Explore the Framework" button** — links to `#about` but could deep-link to the companion app's framework pedagogy section.
6. **All anchor links scroll but `#` brand link** — nav brand `href="#"` causes page jump to top instead of smooth scroll.

### Accessibility
7. **No skip-to-content link** — screen readers must tab through entire nav.
8. **No `aria-expanded` on hamburger** — toggle button has no state for assistive technology.
9. **Color contrast** — Some light text on green backgrounds may not meet WCAG AA (e.g., `rgba(255,255,255,0.6)` on `#1B3A20`).
10. **No alt text on visual elements** — SVG botanical art and cycle ring have no descriptions.
11. **No `lang` subtags** — Document is `lang="en"` which is fine, but no region specified.

### SEO & Meta
12. **No meta description** — `<meta name="description">` is missing.
13. **No Open Graph / Twitter Card tags** — No social preview when shared.
14. **No favicon** — Browser shows default icon.
15. **No structured data** — No JSON-LD for educational organization schema.
16. **No sitemap.xml or robots.txt** — Not critical for single page but good practice.

### Performance
17. **All CSS is inline** — 1042 lines of CSS in `<style>`. Works but makes caching impossible; external stylesheet would be better.
18. **Google Fonts blocking render** — `font-display: swap` is set via Google's URL but three font families load synchronously on first paint.
19. **SVG noise texture on `body::before`** — Full-viewport fixed overlay with `z-index: 9999` sits above everything; potential paint performance issue.

---

## Task List — Operability

### Phase 1: Critical Fixes (Must-Do)

- [ ] **T1.1 — Fix mobile navigation**
  - Add JS click handler for `.nav-toggle` to toggle `.nav-links` visibility
  - Add `aria-expanded` attribute toggling on the button
  - Add CSS for `.nav-links.open` state (slide-down or overlay menu)
  - Ensure clicking a nav link closes the menu
  - Test at 320px, 375px, 768px, 900px breakpoints

- [ ] **T1.2 — Remove ZIP file from repo**
  - Delete `urban-christian-academy---rootwork-framework.zip` from tracked files
  - Add `*.zip` to `.gitignore`
  - Commit the removal

- [ ] **T1.3 — Add meta description and SEO tags**
  - Add `<meta name="description" content="...">` (150-160 chars)
  - Add Open Graph tags: `og:title`, `og:description`, `og:image`, `og:url`, `og:type`
  - Add Twitter Card tags: `twitter:card`, `twitter:title`, `twitter:description`
  - Add canonical URL: `<link rel="canonical" href="https://uca-web-page.vercel.app">`

- [ ] **T1.4 — Add favicon**
  - Create or generate a UCA favicon (gold circle with "UCA" text, matching `.nav-brand-icon`)
  - Add `<link rel="icon">` in multiple sizes (16x16, 32x32, apple-touch-icon)
  - Place favicon files in repo root or `/assets`

### Phase 2: Functional Improvements

- [ ] **T2.1 — Build enrollment inquiry form**
  - Replace the `#enroll` CTA section with a functional contact/inquiry form
  - Fields: Parent/Guardian Name, Email, Phone, Student Grade Level, Program Interest (dropdown), Message
  - Options for form backend: Formspree, Netlify Forms, Google Forms embed, or a Vercel serverless function
  - Add form validation (required fields, email format)
  - Add success/error state feedback

- [ ] **T2.2 — Link to companion portal**
  - Add a "Parent/Staff Portal" link in the nav
  - Link to `https://sa-hearn1-uca-web-page.vercel.app` (or custom domain when ready)
  - Consider a card or callout in the programs section pointing to the portal

- [ ] **T2.3 — Add Summer Camp registration flow**
  - The announcement banner and summer section both reference registration opening March 1
  - Build or link to a registration form (could use the companion app's RegistrationWizard)
  - Add a countdown timer to March 1 if before that date, or "Now Open" badge after

- [ ] **T2.4 — Add scholarship application links**
  - Each scholarship card should link to the actual GA application portals:
    - GSNS: Georgia DOE Special Needs Scholarship application
    - Promise Scholarship: GA ESA portal
    - GOAL: SSO partner organization
  - Or link to a UCA-hosted page with step-by-step application instructions

- [ ] **T2.5 — External link to fg2g-rwfw.com**
  - The CTA section references `fg2g-rwfw.com` — verify this domain is active and correct
  - Ensure the link opens in a new tab with `target="_blank" rel="noopener noreferrer"`

### Phase 3: Accessibility & Compliance

- [ ] **T3.1 — Add skip-to-content link**
  - Add `<a href="#main-content" class="skip-link">Skip to content</a>` as first child of `<body>`
  - Style it as visually hidden until focused
  - Add `id="main-content"` to the hero or first content section

- [ ] **T3.2 — Fix color contrast**
  - Audit all text/background combinations with a WCAG contrast checker
  - Target: AA compliance (4.5:1 for normal text, 3:1 for large text)
  - Key areas to check: hero stat labels, footer text, section intros on dark backgrounds, announcement banner

- [ ] **T3.3 — Add ARIA landmarks and labels**
  - Add `role="banner"` to nav, `role="main"` to content area, `role="contentinfo"` to footer
  - Add `aria-label` to the cycle ring visual ("RootWork Framework cycle diagram")
  - Add `aria-label` to the nav toggle ("Toggle navigation menu")
  - Ensure all interactive elements are keyboard-accessible

- [ ] **T3.4 — Add focus styles**
  - Ensure all links, buttons, and interactive elements have visible focus indicators
  - Use `:focus-visible` for keyboard-only focus styles
  - Match focus ring to gold accent color for brand consistency

### Phase 4: Performance & SEO

- [ ] **T4.1 — Extract CSS to external stylesheet**
  - Move all CSS from inline `<style>` to `styles.css`
  - Add `<link rel="stylesheet" href="styles.css">` to `<head>`
  - Benefits: browser caching, cleaner HTML, easier maintenance
  - Update `.vercelignore` if needed

- [ ] **T4.2 — Add structured data (JSON-LD)**
  - Add `EducationalOrganization` schema with:
    - name, description, url, address, telephone, email, founder
  - Add `Event` schema for Summer Camp 2026
  - Add `Offer` schemas for scholarship amounts

- [ ] **T4.3 — Add sitemap.xml and robots.txt**
  - Create `sitemap.xml` with the single page URL
  - Create `robots.txt` allowing all crawlers
  - Reference sitemap in robots.txt

- [ ] **T4.4 — Optimize font loading**
  - Add `<link rel="preload">` for the most critical font (Playfair Display 700)
  - Consider reducing to 2 font families if Cormorant Garamond is not essential
  - Add `font-display: swap` fallback in CSS for system font stack

- [ ] **T4.5 — Fix body::before noise overlay**
  - The SVG noise texture is `z-index: 9999` which overlays everything
  - It has `pointer-events: none` so it doesn't block clicks, but:
  - It creates a full-viewport compositor layer — test if removing it improves paint performance
  - If keeping it, reduce z-index to 1 or use `will-change: transform` for GPU compositing

### Phase 5: Content & Media

- [ ] **T5.1 — Add real images**
  - The site is 100% CSS/SVG/emoji with zero photographs
  - Add hero image (garden, students, campus)
  - Add images to program cards or about section
  - Use WebP format with `<picture>` fallback for JPEG
  - Add proper `alt` text to all images
  - Consider lazy loading with `loading="lazy"`

- [ ] **T5.2 — Add a photo gallery section**
  - The companion app (SAHearn1-UCA-WebPage) has a `PhotoGallery.tsx` with 4 garden-themed images
  - Replicate or link to it from this site
  - Use CSS grid with lightbox functionality

- [ ] **T5.3 — Add testimonials or quotes**
  - Parent testimonials, student stories, or faculty quotes
  - Adds social proof and humanizes the page

- [ ] **T5.4 — Add video embed**
  - "The Vision" content referenced in the companion app
  - Could be embedded YouTube/Vimeo player in the hero or a dedicated section
  - Use `loading="lazy"` on iframe

- [x] **T5.5 — Update contact information**
  - Email updated to: `info@rootworkframework.com`
  - Phone: `(301) 219-2728`
  - Address: `4560 ACL Boulevard, Savannah, Georgia 31405`
  - Personal references removed; site now promotes UCA as organization

### Phase 6: Infrastructure & DevOps

- [ ] **T6.1 — Add custom domain**
  - Configure a custom domain in Vercel (e.g., `rootworkframework.org` or `uca.rootworkframework.org`)
  - Set up DNS records as instructed by Vercel
  - Update canonical URL and OG tags to match

- [ ] **T6.2 — Set up Vercel Analytics**
  - Enable Vercel Web Analytics for traffic tracking
  - Or integrate a lightweight analytics solution (Plausible, Umami, etc.)

- [ ] **T6.3 — Add HTTPS redirect**
  - Vercel handles this by default, but verify with `curl -I http://...` that HTTP redirects to HTTPS

- [ ] **T6.4 — Configure Vercel preview deployments**
  - Currently the preview URL returned 401 (Unauthorized)
  - Check Vercel project settings → General → "Deployment Protection"
  - Either disable protection for previews or configure authorized access

- [ ] **T6.5 — Set up CI checks**
  - Add a GitHub Action for:
    - HTML validation (html-validate or Nu HTML checker)
    - Lighthouse CI audit (performance, accessibility, SEO scores)
    - Link checker (broken links)

- [ ] **T6.6 — Create a .gitignore**
  - There is no `.gitignore` in this repo (only `.vercelignore`)
  - Add one with: `*.zip`, `node_modules/`, `.DS_Store`, `*.log`, `.env`

### Phase 7: Future Enhancements

- [ ] **T7.1 — Add dark mode toggle**
  - The design system already has dark tokens (forest, soil)
  - Add `prefers-color-scheme` media query support
  - Optional: manual toggle in nav

- [ ] **T7.2 — Add multi-language support**
  - If the school serves multilingual families, consider i18n
  - Start with English/Spanish

- [ ] **T7.3 — Convert to Next.js or Astro**
  - If the site grows beyond a single page, consider a static site generator
  - Astro is ideal for content-heavy static sites with optional JS islands
  - This would enable multi-page routing, component reuse, and build-time optimization

- [ ] **T7.4 — Integrate with the companion portal**
  - Shared auth: allow users to sign in from this site and redirect to the portal dashboard
  - Embed portal components (enrollment wizard) as iframes or micro-frontends
  - Unified navigation between the two sites

- [ ] **T7.5 — Add a blog or news section**
  - School news, program updates, garden progress, community events
  - Could use a headless CMS (Notion, Sanity, Contentful) for content management

- [ ] **T7.6 — Add print stylesheet**
  - For parents who want to print program info, scholarship details, or the full page
  - Hide nav, footer, animations; optimize layout for A4/Letter

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
1. Edit `index.html` directly
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
