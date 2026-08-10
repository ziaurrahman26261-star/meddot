# Medical Billing Website — Content & Assets Production Guide

**Version 1.0 · Companion to `rcm-website-blueprint.md`**
**Purpose:** so your team can build every page without guessing — exact copy structure, exact images/assets, SEO-optimized content, navigation rules, and performance approach for every page. Follow this and you make no mistakes.

---

## Table of Contents

1. [How to use this guide](#g-part-0)
2. [Global design & asset style guide](#g-part-1)
3. [Image & media asset guide (formats, sizes, sourcing)](#g-part-2)
4. [Content & SEO writing rules](#g-part-3)
5. [Navigation & information architecture](#g-part-4)
6. [Performance & delivery approach (nothing lags)](#g-part-5)
7. [Page sheets: core pages](#g-part-6)
8. [Page sheets: services (12)](#g-part-7)
9. [Page sheets: specialties (matrix)](#g-part-8)
10. [Page sheets: state pages (template + data model)](#g-part-9)
11. [Page sheets: trust pages (case studies, reviews, platform)](#g-part-10)
12. [Calculators & interactive assets](#g-part-11)
13. [Blog content pack (90 days)](#g-part-12)
14. [Trust pack: testimonial & case-study collection system](#g-part-13)
15. [SEO master sheet (title/meta templates)](#g-part-14)
16. [Production QA checklist (launch without mistakes)](#g-part-15)

---

<a id="g-part-0"></a>
## Part 0 — How to use this guide

- **Part 1–2** set the global asset rules: one look, one icon set, one image pipeline. Read before any designer or photographer starts.
- **Part 3–4** set content + navigation rules: how every page is written and how users move through the site.
- **Part 5** is the performance contract: follow it and nothing lags.
- **Parts 6–11** are the page sheets: one sheet per page type with copy, SEO, images, and assets. Copy these directly into your CMS.
- **Parts 12–15** are the ongoing content machines (blog, testimonials, SEO templates) and the final QA checklist.

**Symbols:** 🖼 image asset · 🎨 icon/illustration · 🎬 video · 📄 document · ✍ copy to write · ⚙ build/config · ✅ verify

---

<a id="g-part-1"></a>
## Part 1 — Global design & asset style guide

### 1.1 Brand foundation (decide once, use everywhere)

| Element | Guideline | Example decision `[TBD]` |
|---|---|---|
| Company name | Exact spelling everywhere (legal = display = domain = socials) | [Your Co.] |
| Primary color | 1 strong accent (blue/teal = trust) + dark neutral | e.g., #0E5FA8 + #0F172A |
| Secondary accent | 1 supporting color (green = money/results) | e.g., #16A34A |
| Fonts | Max 2: 1 display sans (Inter) + 1 body (same family OK); mono only for code | Inter |
| Illustration style | ONE consistent style — flat geometric, same corner radius, same stroke | see 1.3 |
| Icon set | ONE library (Lucide / Phosphor) — never mix | Lucide |
| Photography style | Real, warm, candid, natural light; never clinical-stock (see 2.4) | see 2.4 |
| Logo | SVG, works on dark + light, min clear-space, favicon + apple-touch-icon | — |

### 1.2 The three asset families (everything on the site is one of these)

1. **Photography** — real people, real office, real clients (with permission). Emotional proof.
2. **Illustration/vector** — explains concepts (revenue cycle flow, dashboard UI, map). Logical proof.
3. **Data/UI** — charts, dashboard screenshots, KPIs. Numerical proof.
> Trust rule: **photography earns trust, illustrations explain, data proves.** Every page should use at least two of the three.

### 1.3 Illustration rules (keep it consistent or it looks unprofessional)

- Same palette as brand (no rainbow)
- Flat geometric style; no gradients on icons; no 3D
- Consistent stroke width (2px) and corner radius (8px) across all icons
- Icons: 24×24 viewBox, SVG, currentColor (so they inherit hover/theme colors)
- Illustrations for process/flow: same characters style, same proportions
- **One team member owns the illustration library** (single source of truth in the repo: `public/assets/illustrations/`)

### 1.4 Logo & brand asset pack (build this folder once)

```
public/assets/brand/
  logo.svg / logo-dark.svg / logo-mark.svg
  favicon.ico + favicon-32.png + apple-touch-icon.png
  og-image-1200x630.png        (social share card)
  brand-style-tokens.css       (colors, fonts, spacing as CSS vars)
```
- ✅ Logo on every page (header + footer), linked home
- ✅ OG image on every page (unique per page type at minimum)
- ✅ Favicon set — the tab icon is the first "polish" signal users see

### 1.5 Color usage rules (trust psychology)

- **Blue/teal** = trust, competence → primary CTAs, links, headers
- **Green** = money, growth → results, KPIs, "paid" states
- **Red/amber** = warnings → "revenue leakage", denial alerts (use sparingly)
- Dark neutrals for text; whitespace generous — this industry reads "clean = reliable"
- Contrast ≥ 4.5:1 everywhere (WCAG — see blueprint Part 9)

---

<a id="g-part-2"></a>
## Part 2 — Image & media asset guide

### 2.1 Formats, sizes & quality targets

| Asset type | Format | Max dimensions | Max file size | Notes |
|---|---|---|---|---|
| Hero image (above fold) | WebP (AVIF if supported) | 1600×900 | 250KB | The LCP element — optimize hardest (see 5.2) |
| Section/side images | WebP | 1200×800 | 150KB | Never bigger than the container needs |
| Card thumbnails | WebP | 800×600 | 80KB | Case studies, blog, specialties |
| Team photos | WebP/JPEG | 800×1000 | 120KB | Portrait, real people |
| Testimonial avatars | WebP | 200×200 | 20KB | Real photos only |
| Payer/client logos | **SVG** (or PNG 2x if no SVG) | 400×200 | 30KB | Grayscale + color version |
| Dashboard screenshots | WebP (or real UI via iframe/live) | 1600×1000 | 200KB | Design a clean mock, not a blurry screenshot |
| Charts/infographics | SVG (animated OK) | responsive | — | Crisp at any DPI |
| Video (dashboard demo) | MP4 (H.264) + poster.jpg | 1280×720 | < 8MB | Also GIF-fallback; see 2.3 |
| OG social card | PNG | 1200×630 | 300KB | Unique per page type |
| PDFs (checklists/guides) | PDF/A | — | < 5MB | Compressed, searchable text (not scanned images) |

### 2.2 Compression & delivery rules (the "nothing lags" contract)

1. 🖼 Always export WebP (or AVIF) — never upload JPEG/PNG originals
2. 🖼 Compress with `next/image` (sharp) — set explicit `width`/`height` (no layout shift)
3. 🖼 Above-the-fold hero: `fetchpriority="high"`, `eager`; everything below: `loading="lazy"`
4. 🖼 `alt` text on every image (rules in 2.6)
5. 🖼 Logo marquee: SVG inline (no HTTP requests, crisp, theme-able)
6. 🖼 No image wider than its display container; no upscaling (blurry = untrustworthy)
7. 🖼 GIFs banned on marketing pages (huge files) — use video or CSS animation instead
8. ✅ Run `npx next/image` optimization + Lighthouse CI gate (blueprint Part 8 budget)

### 2.3 Video assets (only 2 videos on the whole site to start)

| Video | Where | Spec | Purpose |
|---|---|---|---|
| **Dashboard demo** (60–90s, Loom/mp4) | Platform page + Home section 12 | Screen-recording of the real portal (or designed mock), 720p, captions | Shows transparency — biggest trust win |
| **Founder intro** (60s) | About page | Talking head, natural light, phone 4K is fine | People trust people |

- ✅ Poster image (poster.jpg) + `preload="none"` + click-to-play (never autoplay with sound)
- ✅ Captions/subtitles on both (accessibility + 85% watch muted)

### 2.4 Photography rules — what to shoot vs. what to buy vs. what to avoid

**Shoot yourself (or with a local photographer, half-day):**
- Team: group + individual portraits (real names behind them = trust)
- Office/workspace candid (natural light, working, smiling — not posed lab coats)
- A happy client meeting or handshake **only** with written permission
- Your whiteboard/KPI review meeting (shows process)

**If you must buy stock (use sparingly, editorial style):**
- Search terms that work: "office teamwork candid", "healthcare administrator desk", "practice owner laptop", "diverse professionals collaborating"
- Realistic, natural light, people doing actual work — never pointing at blank screens

**🔴 NEVER use (this is eBridge's exact mistake):**
- Doctor in white coat + stethoscope looking at camera (every billing site on Earth)
- People shaking hands in suits
- Glowing hologram/robot/finger-tapping-on-tablet (AI cliché)
- Watermarked, obviously-stock, outdated-resolution photos
- Photos of people without permission

### 2.5 Asset naming convention (repo discipline)

```
public/assets/
  photos/team/{name}-portrait.webp
  photos/office/office-candid-01.webp
  illustrations/revenue-cycle-flow.svg
  icons/{icon-name}.svg            (or use lucide-react components)
  logos/payers/{payer}-logo.svg
  logos/clients/{client}-logo.svg
  docs/{guide-name}.pdf
  video/dashboard-demo.mp4
```
- kebab-case, no spaces, no capital letters, descriptive
- Alt text and file name should match content

### 2.6 Alt-text rules (accessibility + SEO + trust)

- Every 🖼 needs `alt` that describes **what the image shows**, not "image"
- Logos: `alt="Aetna"`, `alt="[Client practice] logo"` (not "logo")
- Decorative only: `alt=""` (empty — screen readers skip)
- Screenshots: describe the KPI visible ("Client dashboard showing 98.2% clean claim rate")
- Keep under ~125 characters; include the keyword naturally when it's a content image

---

<a id="g-part-3"></a>
## Part 3 — Content & SEO writing rules

### 3.1 Voice & tone (write like a senior biller, not a marketing agency)

- **Plain English, specific, concrete.** "We file your claims within 48 hours" not "we ensure timely submission of claims"
- **Numbers over adjectives.** "Cut denials from 11% to 4% in 90 days" not "dramatically reduced denials"
- **No fluff words:** world-class, cutting-edge, solutions, comprehensive, best-in-class, synergize. Delete them.
- **Second person:** "your practice", "you get" — never "practices get"
- **Honest:** state what's included AND excluded. Honesty = trust. (eBridge hides — you publish.)
- Proofread twice. One typo = a credibility ding; typos are the #1 amateur signal in this industry.

### 3.2 Page anatomy (every page follows this skeleton)

```
H1 (promise, keyword-front-loaded)
  └ intro paragraph (2–3 sentences: who you help, what you do, the proof)
Benefits (3–5 bullets or cards — each an outcome, not a feature)
How it works (3–4 steps with timeline)
Proof (1 metric, 1 mini case study, or 1 testimonial)
FAQ (3–5 questions)      ← schema + objection-killing
CTA (primary + phone)    ← never more than 1 primary CTA per viewport
```

### 3.3 SEO writing rules per page type

| Page type | Word count | H1 | Target intent |
|---|---|---|---|
| Home | 600–900 | Brand + promise | Navigational/brand |
| Service | 1,200–1,800 | "Medical Billing Services That…" | Commercial |
| Specialty | 1,200–1,600 | "Medical Billing for [Specialty] Practices" | Commercial long-tail |
| State | 800–1,200 | "Medical Billing Services in [State]" | Local commercial |
| Case study | 800–1,200 | Client outcome | Research/proof |
| Blog | 1,200–2,000 | How-to question | Informational |
| Pricing | 600–900 | "Medical Billing Pricing: [model]" | High-intent commercial |

- **One H1 per page**, keywords in the first ~60 chars, natural (no keyword stuffing)
- **One primary keyword per page** + 2–3 secondary (map them in Part 14)
- **Unique content on every page** — never copy-paste sections between pages (Google doorway flag + their mistake)
- Internal links: every page links to 2–5 other relevant pages (service ↔ specialty ↔ state ↔ blog)
- Each page ends with a **FAQ block + FAQPage schema** (rich results = more clicks)
- Every stat on every page links to proof (case study, results page, or dashboard screenshot)

### 3.4 CTA copy rules

- Primary CTA text is **outcome-based**: "Get My Free Revenue Assessment" / "Get an Exact Quote" / "Book a Free Billing Audit"
- Secondary CTA: "See Client Results" / "Talk to a Biller" (phone)
- One primary CTA per screen; the button label and the form headline must match the page's promise
- Every phone number visible in top bar + mobile sticky bar + footer (phone is the #1 conversion channel here)

---

<a id="g-part-4"></a>
## Part 4 — Navigation & information architecture

### 4.1 IA rules

- **Max 5–6 top-level items** in the nav (human memory + mobile fit). eBridge has 8+ and a dropdown inside a dropdown — users get lost.
- Top-level: **Services ▾ · Specialties ▾ · States ▾ · Pricing · Results · Resources ▾ · Contact** + CTA button
- **Mega menu for Services** (12 items, grouped): *Billing & Coding* (Medical Billing, Medical Coding) · *Reimbursement* (AR Recovery, Denial Management, Prior Authorization, Eligibility Verification) · *Credentialing* (Credentialing, Payer Enrollment) · *Technology* (EHR/EMR Integration, Clearinghouse, Monthly Audit, RCM Consulting)
- **Mega menu for Specialties** (12–20 items, grouped by practice type): Behavioral (Mental Health, Psychiatry, Behavioral Health) · Primary Care (Family Medicine, Internal Medicine, Pediatrics) · Procedural (Cardiology, Pain Management, Orthopedics, OB/GYN, Urology, Podiatry, Dermatology, Radiology) · Acute (ER, Urgent Care)
- **Mega menu for States:** interactive mini-map + "All 50 states" (don't list 50 links in a menu — collapse to the map + search)
- **Breadcrumbs on every page below Home** (Home / Services / Medical Billing) — user wayfinding + SEO `BreadcrumbList`
- **Footer (4–5 columns):** Brand+trust badges · Core Services · Specialties (top 8 + all link) · Company (About, Team, Careers, Case Studies, Results, Reviews) · Contact + newsletter. Legal row under it.
- **Mobile:** hamburger → full-screen sheet with grouped sections; **sticky bottom bar**: [Call] [Free Assessment] — the two most important actions always one thumb away

### 4.2 Navigation UX rules (easy = trusted)

- Active page highlighted in nav; scroll state changes header background (blur + shadow)
- Every nav item lands on a real page — **zero dead links** (their "#" links are a failure; audit yours monthly)
- Search: optional at 70+ pages, add Algolia/Meilisearch later; skip in v1
- Click targets ≥ 44px on mobile; keyboard navigable menus (WCAG)
- "Where am I? Where can I go? How do I get back?" — answer all three on every screen

---

<a id="g-part-5"></a>
## Part 5 — Performance & delivery approach (nothing lags)

### 5.1 The performance contract (from blueprint Part 8 — here's how to achieve it)

| Target | Techniques |
|---|---|
| LCP < 2s | Hero image: WebP/AVIF ≤ 250KB, `fetchpriority="high"`, preconnect to image CDN; no third-party scripts in the critical path |
| INP < 200ms | Minimal client JS; interactivity components lazy; no jQuery-era plugins; icons as SVG components not font icons |
| CLS < 0.05 | Fixed `width`/`height` on ALL images; aspect-ratio boxes for video; no late-inserting banners |
| TTFB < 600ms | Static rendering (SSG/ISR) for all marketing pages; edge runtime; Vercel CDN |
| JS bundle < 250KB | No heavy UI frameworks beyond React; dynamic imports for chat/booking/map |
| Total weight < 1.5MB | Image budget (2.1), fonts subset + `display=swap`, self-host fonts |

### 5.2 Hero image optimization (the one that matters most)

1. Export 1600×900 WebP (AVIF variant too) — nothing wider
2. Serve via `next/image` with `sizes` attribute for mobile (800px) vs desktop
3. `priority` + `fetchPriority="high"` + `decoding="async"` (next/image handles)
4. Preload the LCP image via `<link rel="preload" as="image">`
5. Avoid hero carousels entirely — a static hero with one strong image converts better and never shifts layout (their marquee duplicates = lesson)

### 5.3 Third-party script policy (the #1 lag source)

- Audit: **chat SDK, analytics, booking widget, review widget** — that's it. Anything else goes behind user interaction or is self-hosted
- Load order: analytics (defer) → nothing blocking; booking (lazy, only near CTA); chat (deferred, after idle)
- Never use 3 tag managers stacked on each other
- Test with Lighthouse after EVERY addition — third parties are how sites silently rot

### 5.4 Caching & delivery

- Static pages: CDN cache (Vercel edge), `Cache-Control: public, s-maxage=3600`
- Fonts: self-host with `font-display: swap` + preload the two most-used weights only
- Icons: inline SVG (no icon font request)
- Dashboard mock/video: lazy below fold, click-to-play
- Monthly Lighthouse regression run (CI gate blocks deploys that regress > 5pts)

---

<a id="g-part-6"></a>
## Part 6 — Page sheets: core pages

> **Sheet format used below (fill every row before a page ships):** URL · Goal · Primary CTA · Copy (H1/subhead/sections) · SEO (title/meta/keywords/schema) · Images · Icons/Illustrations · Other assets · Trust elements · Performance notes.

### 6.1 Home `/` — the money page

**Goal:** visitor books a free revenue assessment or calls within 60s.
**Primary CTA:** "Get My Free Revenue Assessment" → `/book-consultation/`

**Copy:**
- H1: `Get Paid Faster. Cut Denials. We Handle Your Entire Revenue Cycle.`
- Subhead: `[Company] is a U.S.-based medical billing, coding & credentialing partner for [niche] practices. Clients average 98%+ first-pass claim acceptance — see the proof.` (link "see the proof" → /results/)
- Trust chips under CTA: `HIPAA-compliant · U.S.-based certified billers · No long-term contracts`
- Section headers (write in your voice, keep promise-first):
  1. "Your revenue cycle, handled end-to-end" (services)
  2. "Why practices switch to [Company]" (why us)
  3. "Built for your practice size" (who we serve)
  4. "Results our clients actually see" (case studies + dashboard)
  5. "How onboarding works — week by week" (process)
  6. "What clients say" (testimonials)
  7. "Serving practices across the U.S." (states map)
- Final CTA band: `Worth $5,000+ in unpaid claims? Get a free revenue assessment.` + booking embed

**SEO:**
- Title: `Medical Billing Services & Revenue Cycle Management | [Company]` (≤60 chars)
- Meta: `U.S.-based medical billing, coding & credentialing for [niche] practices. 98%+ first-pass acceptance, transparent pricing, live client dashboard. Get a free revenue assessment.` (≤155)
- Keywords: medical billing services, revenue cycle management, medical coding services, credentialing services
- Schema: `ProfessionalService` (global) + `FAQPage` (if FAQ on page)

**Images (4 max):**
- 🖼 Hero: real office/team candid photo or clean brand illustration — 1600×900 WebP ≤250KB, `alt="[Company] billing team reviewing client revenue dashboard"`
- 🖼 Dashboard screenshot (designed mock) for "Results" section — 1600×1000 WebP, `alt="Client dashboard: clean claim rate 98.2%, days in AR 24, denial rate 4.1%"`
- 🖼 Team/office candid for "Why us" — 1200×800 WebP
- 🖼 Founder/team photo for CTA band (optional) — 800×1000 WebP

**Icons:** 🎨 8 service icons · 3 "why us" icons · 3 segment icons · 4 stat icons (all Lucide, 24px, currentColor)

**Other assets:** payer logo strip (SVG grayscale → color on hover) · client logos (permission) · 🎬 dashboard demo video link (60–90s) · phone number prominent in hero + sticky bar

**Trust elements:** 4 real stats w/ tooltips→proof · 3 named testimonials → /reviews/ · Google rating badge · guarantee line in footer of page

**Performance:** hero `fetchpriority=high`; all below-fold lazy; no carousel; static render (SSG)

---

### 6.2 Services hub `/services/`

**Goal:** visitor self-selects a service in < 10s.
**CTA:** per-card → detail pages; bottom → "Not sure? Take our 2-minute quiz" or direct booking

**Copy:**
- H1: `Everything Your Revenue Cycle Needs — Under One Roof`
- Intro: who you help + the 12 services grouped
- Group headers: Billing & Coding · Reimbursement & Recovery · Credentialing · Technology & Compliance

**SEO:** Title `Medical Billing, Coding & Credentialing Services | [Company]` · Schema: `ItemList`/`Service` links · this page funnels internal link equity to all 12 service pages

**Images:** none required (icon-driven) — optionally 1 team photo. **Icons:** 12 service icons. **Assets:** compare table "In-house vs. [Company]" (build as table component)

---

### 6.3 Pricing `/pricing/` — the trust page

**Goal:** convert price-shoppers; kill "hidden fees" fear.
**Primary CTA:** "Get an Exact Quote — 15 min, no obligation"

**Copy (draft — adjust to your real numbers):**
- H1: `Simple Pricing. No Hidden Fees. Cancel Anytime.`
- Two-model table:
  | Model | Price | Best for | What's included |
  |---|---|---|---|
  | % of collections | 3–6% (range by volume/specialty) | Most practices | eligibility, claims (48h), denial mgmt, AR follow-up, payment posting, monthly reports, portal |
  | Per-claim flat | $[TBD]/claim | High-volume practices | same as above |
  | Credentialing | $[TBD]/provider (one-time) | Practices enrolling | CAQH, applications, payer follow-up |
  | Add-ons | Audit, consulting, EHR setup | — | one-time or monthly |
- **What's NOT included** (honesty table): postage, clearinghouse fees, prior auth (optional), state filings
- **Guarantee box:** `If your net collections don't improve within 90 days, the next quarter is free.` (link to how the guarantee works + contract excerpt)
- FAQ: setup fees? contracts? how does billing % compare to 10% firms? what if I'm mid-contract with another company? (→ switching guide)
- CTA band + calculator embed (revenue leakage)

**SEO:** Title `Medical Billing Pricing: % of Collections & Per-Claim Rates | [Company]` · keywords: medical billing cost, how much does medical billing cost, medical billing percentage rates · Schema: `FAQPage` + `Offer` where possible

**Images:** 0 stock; 🎨 small illustration next to guarantee box. **Assets:** calculator embed · PDF "Sample monthly report" (real-looking mock) as lead magnet

**Trust elements:** guarantee · included/excluded table · calculator · FAQ · phone + chat on page

---

### 6.4 About `/about/` + Team `/team/` + Careers `/careers/`

**About — Goal:** visitor believes you're real, credible, and committed. **Copy:** founder story (real, specific — why you started, what you saw in the industry), mission, values, milestones timeline, certifications (CPC/CCS/CPB, AAPC/HFMA membership), community. **Images:** 🖼 founder portrait + office candid + 1 milestone graphic (SVG timeline). **Trust:** real names, no stock.

**Team — Goal:** named experts (anonymity = the industry's default; you reverse it). **Copy:** each member: name, role, credentials, 2-line bio, LinkedIn. **Images:** 🖼 portraits 800×1000 WebP, consistent background (same shoot = professional). Include certified billers/coders + your engineers. **SEO:** Title `Our Team — Certified Medical Billers & Coders | [Company]` · schema `Person` per member.

**Careers — Goal:** attract certified talent + signal growth. **Copy:** roles (billers, coders, AR specialists, engineers), culture, benefits, remote policy, ATS embed. **Images:** 🖼 office/team candid. **Assets:** 📄 job descriptions (ATS), 📄 benefits PDF (optional).

---

### 6.5 Contact `/contact/` + Booking `/book-consultation/`

**Contact — Goal:** capture a qualified lead. **Form fields (qualify, don't just collect):** name · practice type (solo/clinic/multi-provider/hospital/ASC) · specialty · state · monthly claim volume · current setup (in-house/other vendor/new practice) · biggest pain (free text) · phone (optional). **Success path:** instant confirmation + calendar link + phone. **Sidebar:** phone, email, hours, response-time promise ("we reply within 1 business day"), chat. **Images:** 🖼 none (form page = fast); maybe team photo. **Assets:** form → API route → email (Resend) + CRM webhook + Slack notify.

**Booking — Goal:** bookings without friction. **Copy:** H1 `Book Your Free 30-Minute Revenue Assessment` + what happens on the call (3 bullets: we review, we tell you honestly, no obligation). **Assets:** Cal.com embed (timezone-aware), confirmation email + SMS reminder. **Trust:** "No obligation · No pressure · We'll tell you honestly if you don't need us" — this line books more calls than any discount.

---

### 6.6 Legal + 404 (quick sheets)

- **Privacy / Terms / Accessibility:** real documents (get counsel), HTML pages, linked in footer, `noindex` Terms/Privacy OK, Accessibility page is a trust signal (WCAG statement + contact for help)
- **404:** H1 `Page not found — but your revenue cycle doesn't have to be lost` + links (Services, Case Studies, Contact) + search + fun-on-brand illustration. Track 404s in analytics; fix monthly.

---

<a id="g-part-7"></a>
## Part 7 — Page sheets: services (12)

> **Universal service-page anatomy** (write each page uniquely — never paste sections between services):
> Hero (H1 = outcome + proof number) → "What's included" scope table → "How it works" (4 steps + timeline) → KPIs we report → mini case study/metric → service FAQ (3–5) → CTA.
> **Universal assets:** 🎨 1 icon per service (Lucide) · 🖼 optional 1 real photo per page (team/office/dashboard) · FAQPage schema · breadcrumbs · internal links to 2 related services + 2 specialties + 1 state + pricing.
> **Universal SEO:** Title = `[Service] Services for [Specialty] Practices | [Company]`; meta = outcome + proof + CTA.

| # | Service / URL | H1 (outcome promise) | Unique scope items (write honestly) | KPIs reported | Target keywords |
|---|---|---|---|---|---|
| 1 | Medical Billing `/services/medical-billing/` | "Medical Billing Services That Get You Paid Faster" | Claim submission (837/1500/UB-04 within 48h), eligibility checks, charge review, payment posting (835), denial mgmt, AR follow-up, patient statements, monthly reports | Clean claim rate, days in AR, denial rate, collection rate | medical billing services, revenue cycle management |
| 2 | Medical Coding `/services/medical-coding/` | "Certified Medical Coding That Prevents Denials" | CPT/ICD-10/HCPCS coding, chart audits, modifier accuracy, payer-specific guidance, coder Q&A, quarterly coding audits | Coding accuracy %, denial rate by coding cause | medical coding services, certified coder, ICD-10 coding |
| 3 | Credentialing `/services/credentialing/` | "Get Credentialed Faster — Start Billing Sooner" | CAQH management, payer enrollment (Medicare/Medicaid/commercial), re-credentialing, status tracking, deadline alerts | Days to enrollment, payers enrolled, re-credential % on time | credentialing services, payer enrollment, CAQH, provider credentialing |
| 4 | AR Recovery `/services/ar-recovery/` | "Recover Stuck Revenue — We Chase the Payers" | Aging analysis, payer follow-up, appeals & reconsiderations, secondary billing, collections on 60–180+ day claims | $ recovered, days in AR reduction, aging buckets | AR recovery, accounts receivable management, medical claim appeals |
| 5 | Denial Management `/services/denial-management/` | "Stop Denials Before They Cost You" | Denial root-cause analysis, prevention workflows, appeal management, payer trend reporting | Denial rate, first-pass acceptance, appeal win rate | denial management, claim denial appeals, denial prevention |
| 6 | Prior Authorization `/services/prior-authorization/` | "Never Lose a Claim to a Missing Auth Again" | Auth tracking, submission to payers, deadline alerts, status updates, denial of auth appeals | Auth approval rate, days-to-auth, missed-auth rate | prior authorization services, medical prior auth |
| 7 | Eligibility Verification `/services/eligibility-verification/` | "Verify Before You Treat — Get Paid Every Time" | Real-time eligibility checks, benefit verification, coverage summaries, pre-service reports | % verified before visit, coverage errors caught | eligibility verification, insurance benefit verification |
| 8 | Payment Posting `/services/payment-posting/` | "Accurate Posting. Zero Overpayments Missed." | ERA/835 auto-posting, EOB review, underpayment detection, credit balance handling, daily reconciliation | Posting accuracy, days to post, underpayment $ recovered | payment posting, ERA posting, EOB reconciliation |
| 9 | Monthly Billing Audit `/services/monthly-billing-audit/` | "Find the Revenue Leaking Out of Your Practice" | Full claims sample audit, coding audit, payment/compliance review, leak report, corrective action plan | $ leaks found, coding error %, compliance gaps | medical billing audit, revenue leak audit |
| 10 | Clearinghouse Solutions `/services/clearinghouse-solutions/` | "One Secure Pipe for Every Claim" | EDI setup, claim format validation, rejection handling, payer connectivity, 277/999 status monitoring | Claim rejection rate, submission success % | medical clearinghouse, EDI claim submission |
| 11 | EHR/EMR Integration `/services/ehr-emr-integration/` | "Your Billing Lives Inside the Tools You Already Use" | Integration with Kareo, AdvancedMD, eClinicalWorks, DrChrono, RXNT, PracticeEHR, athena (list what you support), workflow mapping, staff training | Claims per day, error rate, staff time saved | EHR integration, EMR billing integration, Kareo/AdvancedMD billing |
| 12 | RCM Consulting `/services/rcm-consulting/` | "A Full Revenue Cycle Checkup — Fix It Once" | Full RCM assessment, workflow redesign, revenue integrity, compliance readiness, KPI benchmarks, 90-day plan | Benchmark gaps, $ opportunity, projects completed | revenue cycle consulting, RCM assessment |

**Assets per service page:** 🎨 scope-table icons (check/x) · 🎬 no video per service (keep site fast) · 🖼 dashboard screenshot only on services 1, 4, 5 (claim/AR/denial views — 3 mock screens max, reuse components) · 📄 sample report PDF on services 1, 8, 9 · FAQ block every service.

**Service × Specialty internal links (important for SEO + trust):** Medical Billing ↔ every specialty · Credentialing ↔ specialties w/ complex enrollment (Mental Health, Psychiatry, Pain Mgmt) · Denial Management ↔ specialties w/ high denial rates (Mental Health, Cardiology) · Prior Auth ↔ Radiology, Orthopedics, Pain Mgmt · Coding ↔ all specialties.

---

<a id="g-part-8"></a>
## Part 8 — Page sheets: specialties (matrix)

> **Template (unique per specialty — no copy-paste):** H1 `Medical Billing for [Specialty] Practices` → "Why [specialty] billing is different" (real codes/modifiers/payer quirks) → top 5 denials table → mini case study → specialty FAQ → CTA. Schema: `Service` + `FAQPage`.
> **Assets per specialty:** 🎨 1 specialty icon (consistent set) · 🖼 0 stock photos (icon + text; add real local testimonials as they arrive) · breadcrumbs · links to 2–3 related services + 1–2 states.
> **SEO:** Title `Medical Billing for [Specialty] Practices | [Company]`; meta = specialty promise + proof + CTA.

| Specialty | Unique angle (must be real & written fresh) | Example keyword | Example denial to cover |
|---|---|---|---|
| Mental Health | 90837/90834, add-on codes, telehealth GT/95, no-show billing, LCSW/LMFT Medicare rules | mental health billing services | "diagnosis not covered" |
| Psychiatry | med management 99213-25 + add-ons, TMS, intakes, auth for ECT | psychiatry medical billing | missing modifier 95 |
| Physical Therapy | timed units, 97161–97168 eval, POC requirements, Medicare 8-minute rule | physical therapy billing | timed units exceeded |
| Internal Medicine | E/M levels, chronic care 99490, annual wellness, incident-to | internal medicine billing | E/M undercoding/level mismatch |
| Cardiology | 93306 global periods, stress tests, device implants, MUEs | cardiology medical billing | global period edits |
| Pain Management | HCPCS G-codes, MUE limits, PPSV, urine drug screening 80305–7, auth-heavy | pain management billing | MUE exceeded |
| Family Medicine | E/M + vaccines (90460/90471), well visits, care coordination | family medicine billing | vaccine code mismatch |
| Emergency Rooms | high-volume ED E/M 99281–85, critical care 99291, observation | ER medical billing | observation vs inpatient |
| Urology | cystoscopy bundles, surgical global periods, 76770/76775 US | urology medical billing | unbundling errors |
| Pediatrics | well-child 99381–99395, immunizations, newborn, modifier 25 rules | pediatrics medical billing | modifier 25 overuse |
| OB/GYN | global maternity 59400/59610, delivery bundles, NST/BPP | OB GYN medical billing | global package split |
| Podiatry | nail/wound procedures, HCPCS L-codes, diabetic foot care | podiatry medical billing | DME/L-code denial |
| Dermatology | destruction codes 17000s, MOHs 17311–13, path global | dermatology medical billing | Mohs staging errors |
| Orthopedics | fracture care global periods, 99213-25 same-day, DME splints | orthopedics billing | same-day E/M denial |
| Radiology | 70000–79999, professional vs technical component, AI-aided codes | radiology billing | missing modifier 26/TC |
| Behavioral Health (addictions) | H0001–H2034, ASAM levels, MAT (J-codes), IOP/PHP | behavioral health billing | level of care denial |
| Urgent Care | POS 20, 99202–99215, flu/COVID codes, cash vs insurance | urgent care billing | POS modifier issues |
| Gastroenterology | scopes 43235+, pathology bundles, sedation | GI medical billing | unbundled pathology |
| Endocrinology | continuous glucose monitors, insulin pumps, 95249–95251 | endocrinology billing | DME medical necessity |
| Sleep Medicine | 95800–95811, home vs lab studies, CPAP supplies | sleep medicine billing | PSG frequency limit |

**Rule:** only ship a specialty page you can genuinely service. Quality > quantity — a bad page costs trust even if it ranks.

---

<a id="g-part-9"></a>
## Part 9 — Page sheets: state pages (template + data model)

> **Why these matter:** local searches ("medical billing in Texas") + your linkable asset (timely filing tables). eBridge has 200-word doorway pages — yours will be genuinely useful reference pages. Build programmatically (blueprint Part 6.2) from a content DB.

**State page template (800–1,200 words, all unique per state):**
1. H1 `Medical Billing Services in [State]`
2. Intro (2–3 paragraphs): you serve [specialty] practices across [State]; U.S.-based; state-specific knowledge
3. **Timely filing limits table** — the gold asset:
   | Payer | Professional claims | Institutional claims | Appeals window |
   |---|---|---|---|
   | Medicare | [TBD days] | [TBD] | [TBD] |
   | Medicaid [State Program] | [TBD] | [TBD] | [TBD] |
   | Blue Cross [State] | [TBD] | [TBD] | [TBD] |
   | Aetna / Cigna / UHC / Humana | [TBD] | [TBD] | [TBD] |
4. State-specific rules: prompt-pay laws, no-fault (NY/FL/MI/KY), workers' comp, balance billing, telehealth rules, Medicaid quirks
5. Credentialing notes: state payer enrollment portals, CAQH, NPI, specific requirements
6. 3 local testimonials (as you earn them)
7. Local FAQ (5 questions, FAQPage schema)
8. CTA + phone + booking

**Data model (drives pages + calculator — update once, everywhere):**
```json
{
  "state": "Texas",
  "slug": "texas",
  "medicaidProgram": "TX Medicaid (STAR)",
  "promptPayLaw": "Texas Insurance Code §843.338 — 45 days clean claim",
  "noFault": false,
  "workersComp": true,
  "timelyFiling": [ {"payer":"Medicare","professional":365,"institutional":365,"appeals":120},
                    {"payer":"BCBS TX","professional":180,"institutional":180,"appeals":180} ],
  "enrollmentPortals": ["NPI", "CAQH", "TX HHSC"],
  "localTestimonials": [],
  "faqs": []
}
```

**Build order:** start with 10 states (your target markets) → launch → expand 5 states/month as you sign clients there. Verify every timely-filing number with a human before publish — **wrong compliance data destroys trust faster than no data.**

**Assets:** 🖼 none per state page (text + tables = fast) · 🎨 US map component on `/states/` hub (SVG, hover states, keyboard accessible) · schema `Service` + `FAQPage` + breadcrumbs · internal links: 2–3 services + 2–4 specialties + pricing + 2 neighboring-state pages.

---

<a id="g-part-10"></a>
## Part 10 — Page sheets: trust pages

### 10.1 Case Studies `/case-studies/` + detail pages

**Hub:** grid cards: client type + specialty + state + headline metric (`+38% collections in 90 days`) + duration. **Detail:** Situation → What we found (audit) → What we did (specific actions) → Results (before/after table) → Client quote → CTA.
**Assets:** 🖼 client logo (permission) · 🎬 optional 2–3 min video version · 📄 downloadable one-pager PDF · OG card per study.
**SEO:** Title `[Client] Case Study: [Outcome Metric] | [Company]` · schema `Article` + `Review` only if genuine.
**Rules:** permission to publish · anonymize payers if needed · never inflate · include what DIDN'T work (radical honesty = elite trust).

### 10.2 Results `/results/` + Platform `/platform/`

- **Results:** living proof — quarterly real KPIs (aggregate clean claim rate, days in AR, denial rate, $ recovered), dashboard screenshots, client review scores. **Assets:** 🎬 dashboard demo video (60–90s) · 🖼 3 mock dashboard screens (KPI cards, aging buckets, payer performance) · SVG charts with real (aggregated) numbers.
- **Platform:** "Your revenue cycle on a live dashboard" — portal features (KPIs, claim status, reports, docs, alerts) as icon+copy cards, then the demo video, then FAQ, then CTA ("See a live demo"). Schema `SoftwareApplication`.
- **Trust rule:** every number on these pages = real aggregated data or clearly-labeled example data. No fake "97.2%" without a source. (This is the exact line eBridge crossed.)

### 10.3 Reviews `/reviews/` + HIPAA `/hipaa-security/` + Payers `/payers/` + FAQ `/faq/`

- **Reviews:** real named testimonials (photo + practice + city) · Google rating embed · video testimonials · client logo wall · **review collection automation** (SMS/email post-engagement → Google review link). Never invent.
- **HIPAA/Security:** plain language: BAA available · encryption (TLS/AES-256) · role-based access + audit logs · staff training · breach response · data retention. **Assets:** 📄 security one-pager PDF (lead magnet) · schema `WebPage`. Rule: describe only what you actually do; say "HIPAA-compliant practices", never "HIPAA certified".
- **Payers:** filterable table/grid: Medicare (A/B/Advantage), Medicaid programs, Aetna, BCBS, Cigna, Humana, UHC, Anthem, Oscar, Centene, workers' comp, no-fault. **Assets:** 🎨 SVG payer logos (grayscale, color on hover) · schema `Service` areaServed.
- **FAQ hub:** categorized (Billing · Credentialing · Pricing · Security · Onboarding · Technology), every item links into a relevant page, FAQPage schema on hub + each category. **Content source:** transcribe your sales calls — publish what you actually say.

### 10.4 Blog `/blog/` + Resources `/resources/`

- **Blog:** 4 posts/month (clusters in Part 12). Each post: 1 primary keyword, 1,200–2,000 words, 1 internal link to money page, 1 CTA, FAQ schema where apt, OG card, author byline (real person = trust).
- **Resources:** gated downloads (checklists, trackers, glossary) → email list → nurture sequence. **Assets:** 📄 3 launch PDFs (revenue leakage checklist · payer enrollment tracker · medical billing glossary), designed in brand style (not raw Word docs — a bad PDF hurts more than none).

---

<a id="g-part-11"></a>
## Part 11 — Calculators & interactive assets

> Interactive tools = trust + backlinks + lead capture. Build 2 at launch (your engineers can do both in a day each).

### 11.1 Revenue Leakage Calculator
- **Inputs:** monthly claims volume · avg claim value · current denial rate · current days-in-AR
- **Outputs:** "You're leaving ~$X/year on the table" + clean visual (big number + bar chart) + what good looks like (benchmark table)
- **CTA:** "Get a free audit to find your actual leaks" → booking
- **Assets:** 🎨 chart component (recharts or pure SVG) · schema `FAQPage` ("How do I know my denial rate?") · shareable result (OG-able URL)

### 11.2 Timely Filing Calculator
- **Inputs:** state · payer · claim type · days since DOS
- **Outputs:** "You have X days left to file" / "Past deadline — here's how to appeal" + table of limits
- **Assets:** driven by the same data model as state pages (Part 9) — one source of truth
- **CTA:** "We handle filing deadlines so you don't miss one" → medical billing page

**Build rules:** both calculators: client-side JS only (no server round-trip = instant), mobile-first, 3 fields max, privacy note ("nothing is stored"), results page links to pricing + booking.

---

<a id="g-part-12"></a>
## Part 12 — Blog content pack (90 days)

> 4 posts/month. Each: 1,200–2,000 words · 1 primary keyword · internal link to a money page · 1 CTA · FAQ schema · author byline.

**Cluster 1 — Billing basics (trust + education):**
1. How to Read an EOB: A Practice Owner's Guide *(primary kw: how to read an eob)*
2. What Is a Clean Claim Rate — and Why It's Your #1 Billing Metric
3. Days in AR, Explained in Plain English
4. Medical Billing Percentage Rates: What Practices Actually Pay (2026) → links to Pricing
5. How to Switch Billing Companies Without Losing a Dollar (→ onboarding guide)

**Cluster 2 — Payer rules (linkbait + SEO):**
6. Timely Filing Limits by State: The Complete 2026 Table (→ state pages)
7. Medicare Telehealth Rules 2026: What Changed
8. Aetna / Cigna / UHC Filing Rules: Cheat Sheet
9. No-Fault Billing in NY, FL & MI: What to Know

**Cluster 3 — Denial management (your specialty edge):**
10. Top 10 Claim Denial Reasons (by Specialty) → links to specialty pages
11. How to Appeal a Denied Claim: Step-by-Step
12. Denial Management Checklist: 20 Things to Check Monthly
13. Why Your Denial Rate Might Be Wrong (measurement pitfalls)

**Cluster 4 — Credentialing (high-intent):**
14. CAQH Explained: What Providers Need to Know
15. How Long Does Payer Enrollment Really Take? (Realistic Timelines)
16. Credentialing vs. Contracting: The Difference Matters
17. Re-credentialing Season: A 90-Day Checklist

**Cluster 5 — Compliance (authority):**
18. RAC Audits 101: What Triggers One, How to Survive
19. OIG Work Plan 2026: Highlights for Small Practices
20. 10 Compliance Red Flags in Your Billing (Self-Audit)

**Promotion loop:** publish → LinkedIn founder post → email list → 1 image/quote card per post for social → review 404s & internal links monthly.

---

<a id="g-part-13"></a>
## Part 13 — Trust pack: testimonial & case-study collection system

> Trust content is **collected**, not written. Build the system so it runs on autopilot.

### 13.1 Testimonial pipeline
1. **Trigger:** 90 days after onboarding + after every big win (recovered AR, denial drop, first payment speed)
2. **Ask (specific beats general):** "Your claims' average time-to-payment dropped from 45 to 21 days. Could we get a sentence or two on what that's changed for your practice?"
3. **Collect:** email/SMS link → Google review + short form (name, practice, city, permission checkbox, photo upload)
4. **Publish:** reviews page + relevant specialty/state pages + home rotation
5. **Track:** review rate per month; goal ≥ 4 reviews/month after month 3

### 13.2 Case-study template (fill this before you write anything)
```
Client: [type, specialty, state, volume]
Situation: [current setup, pain, stakes]
Audit findings: [what we found, $ leak identified]
Actions: [3–6 specific things we did]
Results (before → after): clean claim rate X→Y · days in AR X→Y · denial rate X→Y · $ recovered
Quote: [client, verbatim, permission]
```
- **Permission checklist:** name OK? practice name OK? numbers OK? video OK? → sign a release
- One case study per quarter minimum; publish to blog + LinkedIn + a PDF version

### 13.3 The honesty rule (this is your moat)
Every number you publish is either (a) audited client data with permission, (b) your own aggregated portfolio stats, or (c) clearly-labeled example data. If it can't be backed, it doesn't go live. This single rule makes you different from 90% of the industry — and it's why practices will trust you.

---

<a id="g-part-14"></a>
## Part 14 — SEO master sheet (title/meta templates)

| Page type | Title template (≤60) | Meta template (≤155) |
|---|---|---|
| Home | `Medical Billing Services & RCM | [Company]` | `U.S.-based medical billing, coding & credentialing for [niche]. 98%+ first-pass acceptance, transparent pricing, live dashboard. Get a free assessment.` |
| Service | `[Service] Services | [Company]` | `[Outcome promise]. Includes [top 3 scope items]. [Proof stat]. Get a free [service] assessment.` |
| Specialty | `Medical Billing for [Specialty] Practices | [Company]` | `[Specialty]-specific billing: [unique codes/quirks]. [Proof stat]. Free [specialty] billing audit.` |
| State | `Medical Billing Services in [State] | [Company]` | `[State]-specific billing + timely filing limits for [top payers]. [Proof]. Free revenue assessment.` |
| Pricing | `Medical Billing Pricing: % of Collections & Per-Claim | [Company]` | `Simple pricing, no hidden fees. [models + range]. Guarantee included. Get an exact quote.` |
| Case study | `[Outcome Metric] for [Client Type] | [Company]` | `How we [outcome] for a [specialty] practice in [state]. [3 metrics]. Read the full case study.` |
| Blog | `[Keyword-Rich Title] | [Company] Blog` | `[Answer the search intent in one line]. [1 more line of value]. Read the guide.` |
| FAQ | `[Topic] Questions Answered | [Company]` | `Honest answers on [topic] for practice owners. [Teaser question]. Learn more.` |

**Global rules:** unique title+meta per page (never duplicated by the programmatic engine — add a CI check) · keyword naturally in first 60 chars · CTA in meta where natural · no keyword stuffing · OG title/image every page · canonical + breadcrumbs · `sitemap.xml` regenerated on publish.

---

<a id="g-part-15"></a>
## Part 15 — Production QA checklist (launch without mistakes)

### Content QA (every page, before ship)
- [ ] H1 unique + promise-first · one H1 per page
- [ ] No placeholder text, no "Lorem", no "John Doe", no `[TBD]` left behind
- [ ] Every stat traceable to proof (link) or clearly-labeled example
- [ ] Every testimonial real + named + permitted
- [ ] Spelled correctly ×2 (typos = the industry's #1 amateur signal)
- [ ] Unique content — no section copy-pasted from another page
- [ ] FAQ present + FAQPage schema · internal links 2–5 · CTA + phone present
- [ ] Title ≤60 · meta ≤155 · unique · OG image set

### Asset QA
- [ ] All images WebP/AVIF, compressed to budget (Part 2.1), `width`/`height` set
- [ ] Hero: ≤250KB + `fetchpriority=high` · below-fold all lazy
- [ ] alt text on every image (rules 2.6) · no banned stock clichés (2.4)
- [ ] Icons from ONE set · logos SVG grayscale+color · PDFs branded, searchable
- [ ] Videos: poster + captions + click-to-play · no GIFs

### Performance QA
- [ ] Lighthouse ≥ 90 (perf, SEO, a11y, best practices) desktop + mobile
- [ ] CWV in the green (LCP<2s, INP<200ms, CLS<0.05) — CI gate
- [ ] JS bundle ≤250KB · third-party scripts ≤ 4, all deferred
- [ ] No 404s from internal links (crawl test) · sitemap + robots live

### Trust QA (final walk-through as a skeptical practice owner)
- [ ] "Who are these people?" → named team + founder story
- [ ] "Can they prove it?" → case studies + results + reviews
- [ ] "How much does it cost?" → pricing page + included/excluded
- [ ] "Is my data safe?" → HIPAA page + BAA mention
- [ ] "Is switching scary?" → onboarding/process page + switching guide
- [ ] "Can I reach a human?" → phone in top bar + chat + response-time promise

**Final rule:** if a page fails any of the three QAs (content, asset, performance) it doesn't ship. Ship fewer pages, ship them perfect — that's how you beat a competitor who shipped 15 sloppy ones.

---

*End of production guide. Build order: brand assets → design system → core pages → services → specialties/states (data first) → trust pages → calculators → blog. QA gate before every deploy.*






