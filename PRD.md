# PRD — kustonaut.github.io Portfolio
> Last updated: 2026-03-03
> Status: Live · v2.0
> Prototype covers: 90% of flows. This PRD covers: edge cases, design decisions, rollout, and tracking.

---

## 1. Problem Statement

**Problem:** Senior PMs who code have no good way to showcase their technical work alongside PM impact. LinkedIn is text-heavy. GitHub profiles are repo-lists. Neither shows the person behind the work.

**User story:** As a senior PM who builds tools, I want a portfolio that shows *what I built*, *why I built it*, and *the impact* — so that recruiters, peers, and collaborators immediately understand my unique value.

**Rough shape:** Single-page dark-themed portfolio site. Hero → About → Metrics → Journey → Projects → Stack → Philosophy → Writing → Recommendations → Connect. Hosted on GitHub Pages (free, fast, version-controlled).

---

## 2. Design Decisions

### Why single page, not multi-page?
- Portfolio visitors decide in <10 seconds. A single scroll path controls the narrative.
- No routing overhead. No framework dependency. Pure HTML/CSS/JS = instant load.
- GitHub Pages hosts it for free. Zero infrastructure.

### Why dark theme?
- Target audience is developers and technical PMs who spend hours in dark IDEs.
- Dark backgrounds let the cyan/purple accents and project iframes pop.
- Reduces visual fatigue for late-night browsing (conference follow-ups, recruiter research).

### Why embedded iframes for projects?
- Shows the *actual running project*, not a screenshot that could be faked.
- Visitors can interact without leaving the portfolio page.
- Creates a "wow" moment — the project cards are live.

### Typography & Color System
- **Font:** Inter (body), JetBrains Mono (code/accents) — both developer-familiar
- **Accent palette:** Cyan `#00d4ff`, Purple `#7c3aed`, Emerald `#22c55e`, Amber `#f59e0b`
- **Background:** Near-black `#06060b` → `#0e0e16` → `#111119` card hierarchy
- **Border strategy:** Ultra-subtle `rgba(255,255,255,0.06)` — visible structure without clutter

---

## 3. Edge Cases & Error States

### Iframe Failures
- **Scenario:** GitHub Pages is down, or a project repo is deleted/made private.
- **Current behavior:** Broken iframe shows blank white rectangle.
- **Required fix:** Add `onerror` fallback showing a screenshot + "Project temporarily unavailable" overlay.
- **Priority:** Medium — GitHub Pages has 99.99% uptime, but first impressions matter.

### Image CDN Failures
- **Scenario:** Medium CDN (`cdn-images-1.medium.com`) throttles or blocks hotlinking.
- **Current behavior:** Broken images with alt text.
- **Required fix:** Self-host critical images (hero photos, writing thumbnails) in repo `/assets/` folder. Use Medium CDN only as primary with self-hosted fallback.
- **Priority:** High — Medium has changed CDN policies before.

### Mobile Responsiveness
- **Scenario:** 40%+ of portfolio traffic will be mobile (recruiters on phones).
- **Current behavior:** Responsive breakpoints exist at 768px and 480px.
- **Known gaps:**
  - Photo stack in hero section can overflow on <375px screens
  - Iframe viewports are too small to be useful on mobile — should show screenshot + link instead
  - Book covers in recommendations may not align well on narrow viewports
- **Priority:** High — mobile is the primary viewing context for LinkedIn-sourced traffic.

### No-JavaScript Fallback
- **Scenario:** Corporate firewalls, accessibility tools, or privacy browsers block JS.
- **Current behavior:** Typing animation shows empty text. Counters show "0". Reveal animations never trigger. Tabs in recommendations don't work.
- **Required fix:** Add `<noscript>` fallback content. Use CSS-only reveals where possible. Set default visible state.
- **Priority:** Low — <2% of target audience runs no-JS.

### Slow Connections
- **Scenario:** Conference WiFi, mobile data in transit.
- **Current behavior:** 6 iframes load simultaneously = heavy initial payload.
- **Required fix:** Lazy-load iframes with IntersectionObserver (only load when scrolled into view). Show placeholder shimmer until loaded.
- **Status:** `loading="lazy"` is set on iframes — browser-native lazy loading. Sufficient for now.

### Open Library Cover API
- **Scenario:** Book covers loaded from `covers.openlibrary.org` — API may be slow or return placeholder images.
- **Current behavior:** Books show without covers if API fails.
- **Required fix:** Add inline fallback covers (colored rectangles with book title text).
- **Priority:** Low — cosmetic only.

---

## 4. Content Sections & Purpose

| Section | Purpose | Success Metric |
|---------|---------|----------------|
| **Hero** | Hook in <3 seconds. Name, role, value prop, CTAs | Scroll-through rate >70% |
| **About** | Human context. Not a resume — a story | Time on section >5s |
| **Photo Marquee** | Show personality (travel, volunteering) | Emotional connection |
| **Metrics** | Quantified impact — not vanity, real scale | Credibility signal |
| **Journey** | Career narrative in 3 chapters | "I get what this person does" |
| **Projects** | Featured work with live demos | Click-through to project pages |
| **Tech Stack** | Signal technical depth + breadth | PM-who-codes credibility |
| **Philosophy** | 3 principles — shows thinking style | Cultural fit signal |
| **Writing** | Content outside code — personality + depth | Medium click-throughs |
| **Recommendations** | Taste signal — what shaped my thinking | Intellectual credibility |
| **Connect** | Clear CTAs — GitHub, LinkedIn, X, Medium | Contact rate |

---

## 5. Tracking & Analytics

### Current State
- **No analytics installed.** Pure static site with zero tracking.

### Recommended (Not Yet Implemented)
- **Option A:** Simple analytics via [Plausible](https://plausible.io/) or [Umami](https://umami.is/) — privacy-first, no cookies, GDPR compliant.
- **Option B:** GitHub Pages traffic (Settings > Traffic) — gives basic view counts per page. Already available for free.
- **Key metrics to track:**
  - Page views / unique visitors (weekly trend)
  - Scroll depth (are people reaching Projects section?)
  - Outbound clicks (GitHub repos, LinkedIn, Medium articles)
  - Device split (mobile vs desktop)

---

## 6. Rollout & Deployment

### Current Setup
- **Repo:** `kustonaut/portfolio` → GitHub Pages → `kustonaut.github.io`
- **Deploy:** Push to `main` branch auto-deploys via GitHub Pages
- **No build step** — pure HTML, no framework, no bundler
- **Custom domain:** Not configured (using default `.github.io`)

### Future Considerations
- Custom domain (`akshaydixit.dev` or similar) — adds professionalism
- RSS feed for writing section — auto-populate from Medium API
- Project metrics auto-update — pull GitHub stars via API, display live counts
- SEO: structured data (JSON-LD) for Person schema → rich Google results

---

## 7. Iteration Backlog

| # | Improvement | Source | Priority |
|---|-------------|--------|----------|
| 1 | Self-host critical images (hero, writing thumbnails) | Edge case: CDN failure | High |
| 2 | Mobile UX: replace iframes with screenshots on <768px | Edge case: mobile | High |
| 3 | Add basic analytics (Plausible or Umami) | Tracking gap | Medium |
| 4 | Iframe error fallbacks with screenshots | Edge case: Pages down | Medium |
| 5 | No-JS fallback content | Accessibility | Low |
| 6 | Book cover fallback images | Edge case: OpenLibrary API | Low |
| 7 | JSON-LD Person schema for SEO | Discoverability | Low |
| 8 | Auto-update GitHub star counts via API | Data freshness | Low |
| 9 | Case study pages for Brain OS + issue-sentinel | Depth | Future |
| 10 | Blog/writing feed from Medium RSS | Content freshness | Future |
