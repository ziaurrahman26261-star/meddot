# Medical Billing, Credentialing & RCM Company — Complete Website Blueprint & Competitive Analysis

**Version 1.0 · Prepared for: [Your Company Name] [TBD] · Audience: full engineering + design + content team**
**Scope:** a fast, modern, scalable, multi-page website for a medical billing / RCM / credentialing company — better than eBridgeRCM (ebridgercm.com) in every measurable way.

---

## Table of Contents

1. [How to use this document](#part-0)
2. [Executive summary](#part-1)
3. [eBridgeRCM — forensic, page-by-page analysis](#part-2)
4. [Your positioning & trust strategy](#part-3)
5. [Complete sitemap (multi-page architecture)](#part-4)
6. [Page-by-page blueprint](#part-5)
7. [Tech stack & system architecture](#part-6)
8. [SEO & content strategy](#part-7)
9. [Performance & Core Web Vitals](#part-8)
10. [Accessibility](#part-9)
11. [Security, privacy & HIPAA](#part-10)
12. [Conversion optimization](#part-11)
13. [Analytics & measurement](#part-12)
14. [Build roadmap (4 phases)](#part-13)
15. [Master launch checklist](#part-14)

---

<a id="part-0"></a>
## Part 0 — How to use this document

- **Part 2** is the competitive analysis of eBridgeRCM. Read it once to understand the playbook.
- **Part 3** is the strategy: how you win trust and differentiate. Read before designing anything.
- **Parts 4 + 5** are the actual blueprint: every page, every section, in build order. Hand these to your content writers and designers as the source of truth.
- **Part 6** is for your engineers: stack, architecture, and the client portal spec.
- **Parts 7–14** are cross-cutting: SEO, speed, security, analytics, and the schedule.

**Conventions used in this document**

| Mark | Meaning |
|------|---------|
| 🟢 KEEP | Do it like eBridgeRCM (it works) |
| 🔧 IMPROVE | Keep the idea, but do it better |
| 🔴 DROP/AVOID | Their mistake; do not copy |
| ➕ ADD | Not on their site; this is where you win |
| `[TBD]` | Your decision to make (name, pricing, etc.) |

---

<a id="part-1"></a>
## Part 1 — Executive summary

### 1.1 The one-sentence strategy

> eBridgeRCM wins on **structure** (one promise, CTA everywhere, SEO page farm). It loses on **credibility** (fake testimonials, unverifiable stats, typos, slow WordPress, hidden pricing). You win by keeping their structure, fixing every credibility problem, and adding **proof + transparency** (published pricing, real case studies, live client portal) on a **modern, fast, scalable stack** your team owns.

### 1.2 What eBridgeRCM gets right (copy these)

1. One clear hero promise with a quantified result ("boost collections 15–30%")
2. Trust bullets right under the hero (99.8% acceptance, no hidden charges, nationwide)
3. A CTA on every section ("Free Consultation" in nav, hero, mid-page, footer)
4. Audience segmentation ("Who we serve": solo providers / growing clinics / mid-size practices)
5. 3-step process section (reduces fear of starting)
6. Per-service pages, per-specialty pages, per-state pages (long-tail SEO capture)
7. Specific numbers everywhere (40+ specialties, 50 states, $124.8M collected)
8. Phone number + contact in the sticky top bar (the #1 conversion channel in this industry)
9. Newsletter capture in footer
10. Full footer link structure (internal linking + navigation)

### 1.3 What they get wrong (your opportunity list)

1. 🔴 Fake placeholder testimonials ("John Doe", "Goe Bloggs")
2. 🔴 Unverifiable headline stats with zero case studies behind them
3. 🔴 Typos: "Credentailing", "Specialites", "Paediatics", "YourPractice", "hipaa"
4. 🔴 Slow WordPress + Elementor (dozens of images, duplicated slider content)
5. 🔴 "Transparent pricing" claimed, but pricing hidden behind a consultation
6. 🔴 Dead links ("Downloadables #", "Guides #", "Case Studies #")
7. 🔴 Stock doctor photos identical to every other billing site
8. 🔴 Duplicate content in marquees/sliders (bad for SEO)
9. 🔴 Thin doorway-style state pages (Google risk)
10. 🔴 No live chat, no client portal, no case studies, no results dashboard
11. 🔴 No pricing page, no calculator, no guarantee (beyond a slogan)
12. 🔴 Inconsistent branding: "eBridge RCM LLC" / "eBridgeRCM" / "EBRIDGE RCM"

### 1.4 The four pillars of your site (everything below maps to these)

| Pillar | What it means | Pages it powers |
|---|---|---|
| **1. Proof** | Real case studies, real metrics, real named clients, real reviews | Case Studies, Results, Testimonials, Team |
| **2. Transparency** | Published pricing, calculators, guarantees, clear process | Pricing, Calculators, Process, Guarantee |
| **3. Expertise** | Domain depth: payer rules, timely filing limits, specialty nuance, compliance | Specialty pages, State pages, Blog, Resources |
| **4. Technology** | Fast site + client portal with live KPIs + automation story | Home, Platform page, Client Portal |

---

<a id="part-2"></a>
## Part 2 — eBridgeRCM: forensic, page-by-page analysis

### 2.1 Homepage — section-by-section autopsy

| # | Their section | Purpose | Verdict | Your version |
|---|---|---|---|---|
| 1 | Top bar: phone, email, location | Instant contact | 🟢 KEEP | Same + live-chat trigger |
| 2 | Nav: Services / Specialties / Resources / Contact + CTA | Navigation + conversion | 🟢 KEEP | Same structure, cleaner, fewer levels |
| 3 | Hero: "Stop Leaving Revenue on the Table. Get Paid Faster, Guaranteed" + 15–30% + bullets | Promise + proof + action | 🔧 IMPROVE copy | H1 = the promise; subhead = explainer (see below) |
| 4 | Marquee: Nationwide, 40+ specialties, HIPAA, satisfaction | Trust strip | 🔧 IMPROVE | 4 real, defensible stats, each linking to proof |
| 5 | "Why eBridge" — 3 value props with icons | Differentiation | 🟢 KEEP | Same + each links to a proof page |
| 6 | Services grid (4–5 cards + "Just 2.99%" anchor) | Service discovery | 🟢 KEEP | 6–8 cards + real pricing anchors |
| 7 | Specialties grid (8+ cards) | SEO + relevance | 🟢 KEEP | Same + "View all N specialties" |
| 8 | Consultation CTA with checklist | Conversion | 🟢 KEEP | Same + inline calendar booking |
| 9 | Who we serve (3 segments) | Personalization | 🟢 KEEP | Same + each segment → tailored landing page |
| 10 | Testimonials slider (5 "doctors") | Social proof | 🔴 FIX HARD | Real named testimonials + Google reviews link |
| 11 | EHR/EMR platform expertise | Trust via familiarity | 🟢 KEEP | Logos of platforms you *actually* support |
| 12 | States grid + big numbers ($124.8M, 800+) | Local SEO + scale proof | 🔧 IMPROVE | Real, audit-backed numbers + interactive US map |
| 13 | 3-step process | Reduces friction | 🟢 KEEP | 4 steps with deliverables + timelines |
| 14 | Newsletter | Email capture | 🟢 KEEP | Same + lead magnet ("free revenue audit checklist") |
| 15 | Footer | Navigation + SEO + contact | 🟢 KEEP | Same + trust badges (HIPAA, memberships, reviews) |

**Hero copy autopsy (theirs vs. yours)**

- Their H1 is a label: "Healthcare RCM Company in USA". Their best line — "Stop Leaving Revenue on the Table" — is the *subhead*. They buried their promise.
- Yours: **H1 = the promise** ("Get Paid Faster. Cut Denials. We Handle Your Entire Revenue Cycle."), **subhead = explainer + auditable number** ("Our clients average 98%+ first-pass claim acceptance — see the numbers behind that claim.").

### 2.2 Services hub + service detail pages

**Their pattern:** `/services/` hub → each service gets a page: hero → payer logos → service list → work hours → 3-step process → testimonials → CTA.

**Autopsy**

- 🟢 KEEP: one page per service, each with its own hero promise, benefits, and CTA.
- 🔴 DROP: the work-hours table on a services page (put hours on Contact only).
- 🔴 DROP: the same 3-step process verbatim on every page (duplicate content risk).
- 🔧 IMPROVE: every service page must answer the 4 questions a buyer asks:
  1. **What exactly do you do?** (scope of work, included/excluded)
  2. **How does it work in practice?** (workflow, tools, timeline, who does what)
  3. **What proof do you have?** (case study, metric, testimonial)
  4. **How is it priced?** (anchor or link to Pricing)
- ➕ ADD: scope-of-work lists, payer knowledge per service, KPIs you'll report, and a **"DIY vs. outsourced" comparison table** (a huge trust winner).

### 2.3 Specialty pages ("medical billing for X")

**Their pattern:** 8+ specialties in nav (Mental Health, Psychiatry, Physical Therapy, Internal Medicine, Cardiology, Pain Management, Family Medicine, ERs) + more from the hub (Urology, Pediatrics, OB/GYN, Podiatry). Page = hero → 2–3 paragraphs → bullets → CTA.

**Autopsy**

- 🟢 KEEP: the concept — specialty pages capture high-intent searches and make practices feel understood.
- 🔴 DROP: thin, templated, near-duplicate content (Google can treat these as doorway pages).
- 🔧 IMPROVE: each specialty page needs genuinely specialty-specific content:
  - Unique coding challenges (psychiatry: 90837/90834, add-on codes, telehealth modifiers GT/95; cardiology: 93306 echo global periods; pain management: HCPCS G-codes, MUE limits)
  - Top denial reasons *for that specialty* and how you fix them
  - Payer quirks (Medicare vs. commercial behavior for that specialty)
  - One mini case study or specialty-specific metric
  - 3–5 specialty-specific FAQs
- ➕ ADD: 12–20 specialty pages (list in Part 4).

### 2.4 State pages

**Their pattern:** ~15 states linked from homepage; each is a thin page ("Medical billing in [State]").

**Autopsy**

- 🟢 KEEP: per-state pages are the right idea (local SEO, "medical billing services in Texas" searches).
- 🔴 DROP: thin doorway pages with no unique value — Google risk and a weak user experience.
- 🔧 IMPROVE: make each state page a **genuine local resource**:
  - **Timely filing limits table for that state** (state-specific rules + major payers) — this is a killer, linkable asset eBridge only touches in one blog post
  - State-specific payer landscape (Medicaid nuances, no-fault states like NY/FL/MI, workers' comp rules)
  - Licensing/credentialing notes for that state (CAQH, NPI, state enrollment portals)
  - 2–3 local client testimonials (once you have them)
  - Local FAQ
- ➕ ADD: all 50 states programmatically (with unique content per state — your engineers can generate from a content DB; see Part 6).

### 2.5 About / Contact / Blog / FAQ pages

- **About** — exists, but generic. ➕ ADD: founder story, team photos, credentials (CPC/CCS/CPB certifications), company timeline, mission.
- **Contact** — standard form + phone. 🔧 IMPROVE: add calendar booking (Cal.com/Calendly), office hours, response-time promise, and a form with the right fields (practice type, state, monthly claim volume — qualify leads before the call).
- **Blog** — exists. 🔧 IMPROVE: cluster topics (billing basics, payer-specific guides, timely filing limits, denial management, compliance) with proper internal linking. This is your long-term SEO engine.
- **FAQ** — exists. ➕ ADD: categorized FAQ with FAQPage schema, and expand with objection-handling questions (pricing, security, contract terms, onboarding time, guarantees).

### 2.6 What is entirely missing from their site (your moat)

1. ➕ **Pricing page** — they say "transparent pricing" but hide it. Publishing starting prices is the single biggest trust differentiator in this industry.
2. ➕ **Real case studies** — with client names (permission), before/after metrics, methodology.
3. ➕ **Results/Outcomes page** — sample client dashboard showing real KPIs (clean claim rate, days in AR, denial rate, collection rate).
4. ➕ **Client portal** — a login where clients see live KPIs, claim status, aging reports. No US billing competitor in this tier has one; with your engineering team, this is your wedge.
5. ➕ **Pricing/ROI calculators** — "revenue leakage calculator" and "timely filing calculator".
6. ➕ **Guarantee page** — a real, written performance guarantee.
7. ➕ **HIPAA/Security page** — a plain-language page + BAA explanation. Builds trust with privacy-conscious practices.
8. ➕ **Payers page** — the list of payers they bill (Medicare, Medicaid, Aetna, BCBS, Cigna, Humana, UHC, Anthem, workers' comp, no-fault).
9. ➕ **Live chat / AI assistant** — 24/7 lead capture (an AI company's site should have an AI assistant; a billing company should too — "24/7 support" claims need a 24/7 channel).
10. ➕ **Careers page** — top RCM talent searches for remote billing jobs; you also want to hire billers/coders.
11. ➕ **Resources hub** — guides, checklists, downloads (dead links on their site = your opportunity to actually build them).
12. ➕ **Team page** — named people with credentials. The #1 trust gap in this industry is anonymity.

---

<a id="part-3"></a>
## Part 3 — Your positioning & trust strategy

### 3.1 The trust problem in RCM outsourcing

Buyers (practice owners, office managers, clinic administrators) have been burned:
- Billing companies that promise the world, deliver nothing, and lock them into contracts
- Offshore teams with no payer knowledge and bad English on the phone
- Opaque pricing ("2.99% of collections" hides a dozen add-on fees)
- Zero visibility into what's happening with their claims

Every trust element on your site should be designed to answer the unspoken question:
**"Why should I hand you my practice's revenue?"**

### 3.2 The trust stack (build ALL of these)

Ordered by impact. This is the core of Part 1's "Proof + Transparency" pillars.

| # | Trust element | How to do it right | Where it lives |
|---|---|---|---|
| 1 | **Real named testimonials** | Full name + practice name + city/state + photo (with permission). Video is even better. | Home, Specialty pages, Reviews page |
| 2 | **Published case studies** | Problem → approach → measured result (e.g., "recovered $214k in 90 days from 9 months of stuck AR"). | Case Studies |
| 3 | **Transparent starting pricing** | "$X per claim" or "X% of net collections" with a plain-language what's-included table. | Pricing |
| 4 | **Written guarantee** | e.g., "If your net collections don't improve within 90 days, the next quarter is free." Back it with the contract. | Pricing, Home, Guarantee section |
| 5 | **Verifiable numbers** | Every stat links to proof (case study, dashboard screenshot, testimonial). No orphan numbers. | Home stats, About |
| 6 | **Named team with credentials** | Real photos, names, certifications (CPC, CCS, CPB, PMP, HFMA/AAPC membership), LinkedIn links. | Team, About |
| 7 | **HIPAA & security page** | Plain-language explanation + BAA, encryption, access controls, audit logs, employee training. | HIPAA/Security |
| 8 | **Compliance depth** | Timely filing limits, OIG/RAC audit readiness, payer rules — published as free resources. Signals you know the domain. | State pages, Blog, Resources |
| 9 | **Third-party proof** | Google Business Profile reviews, BBB profile, Clutch (they have a "services" category), LinkedIn recommendations. Embed/aggregate. | Reviews page, Footer |
| 10 | **Client portal demo** | Even a 60-second GIF of the dashboard ("this is what your practice sees"). Concrete beats abstract. | Platform page, Home |
| 11 | **Founder story** | Why you started this, who you are, your background. People trust people. | About |
| 12 | **Onboarding transparency** | Publish your 30-day onboarding plan (what happens week 1–4). Kills the #1 fear: "what if it's a mess to switch?" | Process page, FAQ |

### 3.3 Positioning statement (fill in, then use everywhere)

> **[Company Name]** is a U.S.-based medical billing, coding, and credentialing company that helps **[niche: e.g., mental health / cardiology / multi-specialty]** practices in **[states]** get paid faster. Unlike traditional billing partners, we combine **[certified U.S. billers]** with **[proprietary automation / live client dashboard / transparent flat pricing]** — and we publish **[our pricing / our results / our guarantee]**.

### 3.4 Pick a wedge before you scale (like their "40+ specialties" — but real)

| Wedge option | Why it works | Marketing angle |
|---|---|---|
| **A. Specialty depth** | "Mental health billing done right" — psychiatry/psychotherapy has complex coding; solo providers are underserved | "You're a therapist, not a biller. We handle 90837 + telehealth + modifiers." |
| **B. State depth** | Dominate 1–2 states first (e.g., New York + New Jersey), then expand | Local reviews, local events, state-specific content |
| **C. Practice size** | Solo providers & small clinics (they're ignored by big firms) | "Big-firm expertise without big-firm minimums" |
| **D. Technology** | Client portal + automation as the differentiator | "Your revenue cycle on a live dashboard" |

**Recommendation:** start with **A or C** for your niche + **B** for geography. Use D as the differentiator everywhere. Then expand the page farm (specialties × states) programmatically — your engineers can generate hundreds of genuinely useful pages from a content database (timely filing tables, payer rules, FAQs per state/specialty).

### 3.5 Branding rules (fix what they broke)

- One exact company name everywhere: legal name + display name + domain + social handles
- One logo lockup, one color palette, one type scale (design system — Part 6)
- Zero typos in production. Add a proofreading step to the release pipeline (content lint + human pass)
- Voice: confident, concrete, plain-English. No "world-class solutions" fluff. Say "we filed 1,200 claims last month for cardiology practices in Texas" not "we provide comprehensive solutions."

---

<a id="part-4"></a>
## Part 4 — Complete sitemap (multi-page architecture)

### 4.1 Site map overview

```
/
├── /                  Home
├── /about/            About Us (+ team)
├── /services/         Services hub
│   ├── /services/medical-billing/
│   ├── /services/medical-coding/
│   ├── /services/credentialing/
│   ├── /services/ar-recovery/
│   ├── /services/denial-management/
│   ├── /services/prior-authorization/
│   ├── /services/eligibility-verification/
│   ├── /services/payment-posting/
│   ├── /services/patient-billing/
│   ├── /services/monthly-billing-audit/
│   ├── /services/clearinghouse-solutions/
│   ├── /services/ehr-emr-integration/
│   └── /services/rcm-consulting/
├── /specialties/      Specialties hub
│   └── /specialties/{specialty}/    12–20 pages (template)
├── /states/           States hub (+ interactive map)
│   └── /states/{state}/             50 pages (template)
├── /pricing/          Pricing + guarantee
├── /case-studies/     Case studies hub
│   └── /case-studies/{slug}/        4–8 detail pages
├── /results/          Outcomes + dashboard demo
├── /platform/         Technology + client portal
├── /reviews/          Testimonials + Google reviews
├── /team/             Team page
├── /careers/          Careers
├── /hipaa-security/   HIPAA & security
├── /payers/           Payers we work with
├── /faq/              FAQ hub (categorized)
├── /blog/             Blog
│   └── /blog/{slug}/                 4 posts/month initially
├── /resources/        Guides, checklists, calculators
│   ├── /resources/revenue-leakage-calculator/
│   └── /resources/timely-filing-calculator/
├── /contact/          Contact + booking
├── /book-consultation/  Booking page (Cal.com embed)
├── /privacy-policy/
├── /terms-of-service/
├── /accessibility/
├── /404/              404 page
└── /portal/           Client portal (app, auth required)
```

### 4.2 Page counts & effort

| Page group | Count | Content depth | Effort (team of 3–5) |
|---|---|---|---|
| Core pages (Home, About, Services hub, Pricing, Contact, etc.) | ~12 | High | 2–3 weeks |
| Service detail pages | 12 | High | 2–3 weeks |
| Specialty pages | 12–20 | Medium (unique per specialty) | 1–2 weeks |
| State pages | 50 | Medium (data-driven, unique content) | 1–2 weeks (programmatic) |
| Case studies | 4–8 | High | ongoing |
| Blog + Resources | 10–20 | Medium | ongoing |
| **Total launch scope** | **~70 pages** | — | **6–8 weeks** |

**Build order:** Core pages → Services → Specialties (top 8) → States (top 10) → launch → then fill in the rest programmatically while you market the top pages.

---

<a id="part-5"></a>
## Part 5 — Page-by-page blueprint

> Every page follows the same anatomy: **Hero (promise) → Proof (numbers/case studies) → How it works → Objections (FAQ) → CTA**. Design once, vary the content.

### 5.1 Universal page template (applies to every page)

- **Header:** top bar (phone, email, hours) + sticky nav (Services ▾, Specialties ▾, States ▾, Pricing, Case Studies, Resources ▾, Contact) + CTA button ("Free Revenue Assessment")
- **Footer (5 columns):** company blurb + trust badges → Core Services → Extra Services → Resources/Company → Contact + newsletter. Plus legal row.
- **Floating elements:** live chat launcher (bottom-right), sticky mobile call button (tel:), "Book free assessment" in the nav on every page
- **SEO defaults:** unique title/meta/OG per page, JSON-LD schema (see 7.4), canonical, breadcrumbs
- **Consistency rules:** one CTA style, one accent color, no stock-photo clichés (use real team/clients or clean illustrations), every stat links to proof

---

### 5.2 Homepage `/` — the money page

**Goal:** convert visitors into booked assessments / phone calls within 30–60 seconds.
**Audience:** practice owners, office managers, clinic admins (low technical knowledge, high fear of being cheated).

**Sections (top to bottom):**

| # | Section | Content guidance |
|---|---|---|
| 1 | Top bar | Phone, email, "Mon–Sat 9–6 ET", chat trigger |
| 2 | Nav | As per universal template |
| 3 | **Hero** | H1: "Get Paid Faster. Cut Denials. We Handle Your Entire Revenue Cycle." Subhead: explainer + auditable number ("Clients average 98%+ first-pass acceptance — here's how"). CTAs: "Get My Free Revenue Assessment" (primary) + "See Client Results" (secondary). Trust chips: HIPAA-compliant · U.S.-based certified billers · No long-term contracts |
| 4 | **Proof strip** | 4 real stats with tooltips linking to proof: first-pass acceptance %, denial rate reduction, avg. days-in-AR improvement, $ recovered to date. (Start with honest placeholder targets; replace with real audited numbers) |
| 5 | **Payers logo strip** | Medicare, Medicaid, Aetna, BCBS, Cigna, Humana, UnitedHealthcare, Anthem + "and 1,000+ commercial plans" |
| 6 | **Services** | 8 cards (billing, coding, credentialing, AR recovery, denial management, prior auth, audit, integration) — each: icon, one-line promise, 3 bullets, link to detail page. One card links to Pricing |
| 7 | **Why us (3 columns)** | 1) Certified U.S. team (→ Team) 2) Live dashboard & transparency (→ Platform) 3) Real guarantee (→ Pricing/Guarantee) |
| 8 | **Who we serve** | 3 segments: Solo providers / Growing clinics / Mid-size practices. Each links to a tailored section or page |
| 9 | **Specialties** | 8 specialty cards (the ones you actually serve) + "See all N specialties" |
| 10 | **Case study spotlight** | 1 featured case study with numbers + link to all |
| 11 | **Process (4 steps)** | Week 1: onboarding & data transfer → Week 2: claims begin → Week 3–4: denial cleanup of backlog → Ongoing: monthly KPI review. Show *deliverables + timeline* per step (their 3 steps had no timeline) |
| 12 | **Results preview** | Screenshot/GIF of the client dashboard (KPI cards: clean claim rate, days in AR, denial rate, collection rate) |
| 13 | **Testimonials** | 3 real, named, photo'd testimonials + "Read our Google reviews" link |
| 14 | **States strip** | Interactive US map (hover = states served) + link to /states/ |
| 15 | **Final CTA band** | "Worth $5,000+ of unpaid claims? Get a free revenue assessment." + calendar booking embed |
| 16 | **Newsletter + footer** | Lead magnet: "The Revenue Leakage Checklist (PDF)" |

**Homepage KPIs:** hero CTA click rate, phone call rate, form completion rate, time-to-booking.

---

### 5.3 Services hub `/services/`

**Goal:** organize the 12 services so visitors self-select fast; capture those still comparing.
**Sections:** hero ("Everything your revenue cycle needs — under one roof") → services grid grouped by category (Billing & Coding / Reimbursement & Recovery / Credentialing / Technology & Compliance) → "Not sure what you need?" quiz or CTA → compare table (DIY vs. outsourced) → testimonials → CTA.
**SEO:** this is the hub that links to all 12 detail pages (internal linking equity).

---

### 5.4 Service detail page — template + worked example

**Anatomy (for all 12 services):**

1. Hero: H1 = outcome ("Stop Denials Before They Happen: Denial Management That Works"), subhead = explainer + proof number
2. "What's included" scope table (12–20 bullets, honest about exclusions)
3. "How it works" — 4-step workflow specific to *this* service with tools and timeline
4. KPIs we report for this service (table: metric → what good looks like)
5. Mini case study or metric (real)
6. Payer/specialty nuances relevant to this service
7. 3–5 FAQ (specific to this service)
8. CTA: "Get a free [service] assessment" + phone
9. Schema: `Service` + `FAQPage`

**Worked example — `/services/medical-billing/`**

- H1: "Medical Billing Services That Get You Paid Faster" | Sub: "Clean claims, proactive denial management, and faster reimbursements — with a live dashboard showing every dollar."
- Scope table: claim submission (CMS-1500/UB-04, 837P/837I), eligibility verification, charge capture review, payment posting (ERA/835), denial management, AR follow-up, patient statements, monthly reports, payer credentialing support, EHR integration support. **Excluded:** (be honest) — e.g., billing for anesthesia groups with CRNAs unless negotiated.
- How it works: 1) Onboarding & EDI setup (week 1) → 2) Claims submitted within 48h (ongoing) → 3) Denials worked within 7 days (ongoing) → 4) Monthly KPI review call.
- KPIs reported: clean claim rate, days in AR, denial rate, collection rate, net collections trend.
- CTA: "Get a free billing audit of your last 3 months of claims."

---

### 5.5 Specialties hub + specialty template

**Hub `/specialties/`:** hero → grid of 12–20 specialty cards → "Don't see yours? Ask us" CTA.

**Specialty page template** (each must be genuinely unique — this is where you beat them):

1. Hero: "Medical Billing for [Specialty] Practices" + specialty-specific promise
2. **"Why [specialty] billing is different"** — 3–4 paragraphs of real domain content (unique codes, modifier rules, payer quirks, telehealth rules, MUE issues, etc.)
3. **Top 5 denial reasons in [specialty]** + how you prevent each (table)
4. Mini case study or metric
5. 3–5 specialty FAQs
6. CTA + phone + calendar
7. Schema: `MedicalSpecialty`/`Service` + `FAQPage`

**Worked example — `/specialties/mental-health-billing/`**

- Unique content: CPT 90791/90834–90838, add-on 90833/90836/90838, psychotherapy-with-E/M combos, telehealth modifiers GT/95/93, place-of-service 10 vs 02, Medicare incident-to rules for LCSWs/LMFTs, insurance panel enrollment for behavioral health, no-show billing rules.
- Denial table: "Diagnosis not covered" (F-codes vs. coverage policies), "Missing modifier 95 for telehealth", "Frequency exceeded" (90837 vs 90834 limits), "Not medically necessary" (progress notes requirements), "Service not covered by plan" (out-of-network).
- CTA: "Free mental health billing audit — we'll review your last 3 months of EOBs."

**Specialty list to build (12–20):** Mental Health · Psychiatry · Physical Therapy · Internal Medicine · Cardiology · Pain Management · Family Medicine · Emergency Rooms · Urology · Pediatrics · OB/GYN · Podiatry · Dermatology · Orthopedics · Radiology · Behavioral Health (addictions) · Gastroenterology · Endocrinology · Nephrology · Urgent Care. *(Add only specialties your team can genuinely support.)*

---

### 5.6 States hub + state template

**Hub `/states/`:** hero + interactive US map (click a state) + search + list.

**State page template** (50 pages — programmatic, but each with real unique content):

1. Hero: "Medical Billing Services in [State]"
2. **Timely filing limits table** (your killer content asset): rows = major payers (Medicare, Medicaid, BCBS, Aetna, Cigna, UHC, Humana), columns = claim type (professional/institutional), days allowed, appeals window. Updated regularly — make it linkable ("cite us" bait).
3. State-specific payer landscape: Medicaid program name + quirks, no-fault/workers' comp rules if applicable (NY/FL/MI/KY), balance-billing laws, prompt-pay laws (e.g., TX, NY, PA, FL require payers to pay/deny within X days)
4. Credentialing notes: state enrollment portals, CAQH, NPI, specific payer applications
5. 3 local testimonials (as they accumulate)
6. Local FAQ (5 questions)
7. CTA + phone
8. Schema: `LocalBusiness`-adjacent `Service` pages + `FAQPage`

**Why this beats them:** their state pages are 200 words of fluff. Yours are genuinely useful reference pages → better rankings, more backlinks, more trust.

---

### 5.7 Pricing `/pricing/` — the differentiator

**Goal:** convert price-shoppers and kill the "hidden fees" objection. Be the rare billing company that publishes prices.

**Recommended structure:**
- Hero: "Simple pricing. No hidden fees. Cancel anytime."
- **Two pricing models** (most practices understand both):
  1. **% of collections** — e.g., 3–6% of net collections depending on volume/specialty (mental health/pain management often higher, high-volume primary care lower). Show a range table.
  2. **Per-claim flat fee** — e.g., $X per claim for high-volume practices.
- **What's included table** (both models): eligibility, claim submission, denial management, AR follow-up, payment posting, monthly reports, client portal access. **What's NOT included** (honest): patient statements postage, clearinghouse fees, credentialing (optional add-on), prior auth (optional add-on).
- **Credentialing pricing:** flat per-provider fee (e.g., $[TBD]/provider) or bundled.
- **Add-ons:** monthly billing audit, RCM consulting, EHR integration setup (one-time).
- **The guarantee box:** "If your net collections don't improve within 90 days, the next quarter is free." (Legal: define "improve" in the contract; cap exposure; require baseline audit first — which you do for free anyway.)
- **Calculator embed:** revenue leakage calculator (see 5.14).
- FAQ: "Why don't you charge 10% like the big firms?" (answer: automation + volume + transparency), "Any setup fees?", "Contract terms?"
- CTA: "Get an exact quote — 15-minute call, no obligation."

**SEO:** target "medical billing cost", "how much does medical billing cost", "medical billing percentage rates" — high-intent, low-competition-against-firms-that-hide-pricing.

---

### 5.8 Case studies `/case-studies/`

**Goal:** the single most persuasive content type for this industry.

**Hub:** grid of 4–8 case studies, each with: client type, specialty, state, headline result ("+38% collections in 90 days"), 2–3 metrics, duration.

**Detail template:** Situation (client, specialty, volume, problem) → What we found (the audit) → What we did (specific actions: coding corrections, denial appeals, AR cleanup, credentialing) → Results (before/after table: clean claim rate, days in AR, denial rate, $ recovered) → Client quote → CTA.
**Rules:** only publish with client permission; anonymize payers if needed; never inflate. Even "we recovered 40% of the backlog we identified" is compelling if true. Video case studies (2–3 min) outperform text 3x.

---

### 5.9 Results `/results/` + Platform `/platform/`

- **`/results/`**: aggregate "living proof" — real KPIs across your book of business (quarterly updated), client dashboard screenshots, chart of cumulative $ recovered, client review scores.
- **`/platform/`** ("Your revenue cycle on a live dashboard"): explain the client portal — KPIs visible 24/7 (clean claim rate, days in AR, denial rate by payer, aging buckets, $ pending), claim-level status tracking, document vault, monthly report downloads. Include a 60–90s screen recording demo (Loom) — no login needed. This page is your engineering team's showcase; it's what no competitor at your tier has.

---

### 5.10 Reviews `/reviews/`

- Aggregated testimonials (named, photographed, permission-granted) + Google Business Profile rating widget + video testimonials + a "our clients" logo wall (practices that allow it).
- Add review-collection automation: post-engagement SMS/email ask → Google reviews. Every 5-star review is free SEO + trust.
- **Never** invent reviews (their #1 mistake).

---

### 5.11 About `/about/`, Team `/team/`, Careers `/careers/`

- **About:** founder story (why you started this — be specific), mission, values, timeline of milestones, certifications, community involvement.
- **Team:** real photos, names, titles, credentials (CPC/CCS/CPB/CEMA), short bios, LinkedIn links. Include a few certified coders/billers plus your engineers. Anonymity is the industry's default — your named team is a weapon.
- **Careers:** remote roles (billers, coders, AR specialists, engineers), benefits, culture, application form (ATS embed). Hiring signal = growth signal; also attracts the certified talent you need.

---

### 5.12 HIPAA/Security `/hipaa-security/` + Payers `/payers/`

- **HIPAA/Security page:** plain-language commitment + specifics: Business Associate Agreement (BAA) on request, encryption in transit/at rest, role-based access + audit logs, employee training, breach response process, data retention/deletion policy, HIPAA-compliant stack (hosting, email, files). Include a "Download our security one-pager" lead magnet. *(See Part 10 for the technical reality — don't overclaim.)*
- **Payers page:** the full list: Medicare (Parts A/B, Advantage), Medicaid (state programs), commercial (Aetna, BCBS, Cigna, Humana, UHC, Anthem, Oscar, Centene…), workers' comp, no-fault (NY/FL/MI), and "1,000+ plans via our clearinghouse network". Filterable table is even better.

---

### 5.13 FAQ `/faq/`

- Categorized hub: Billing & Coding · Credentialing · Pricing & Contracts · Security & Compliance · Onboarding · Technology.
- Every FAQ answers an objection, with links into relevant pages. Include the 10 questions you'll actually be asked on sales calls — write down what you say on calls and publish it.
- FAQPage schema on every FAQ (rich results).
- Bonus: a "How to switch billing companies" guide (onboarding fear is your biggest competitor — teach them how to leave their current provider safely).

---

### 5.14 Blog `/blog/` + Resources `/resources/` + Calculators

**Blog (SEO engine):** 4 posts/month in clusters:
- *Billing basics* ("How to read an EOB", "What is clean claim rate?")
- *Payer guides* ("Aetna timely filing limits by state", "Medicare telehealth rules 2026")
- *Denial management* ("Top 10 denial reasons by specialty", "How to appeal a denied claim")
- *Credentialing* ("CAQH explained", "How long does payer enrollment take?")
- *Compliance* ("RAC audits 101", "OIG work plan highlights")
- Each post: 1 primary keyword, 1 internal link to a money page, 1 CTA, FAQ schema where apt.

**Resources:** downloadable checklists & guides ("Revenue leakage checklist", "Payer enrollment tracker spreadsheet", "Medical billing glossary") gated behind email → grows your list → nurture sequences → booked calls.

**Calculators (interactive, build with your engineers — high linkbait value):**
1. **Revenue leakage calculator:** inputs (monthly claims, denial rate, avg claim value) → output "you're losing $X/yr" → CTA "get a free audit".
2. **Timely filing calculator:** input state + payer → "you have X days to file — past-due claims worth $Y".
3. *(Optional later)* Credentialing timeline estimator, ROI of outsourcing calculator.

---

### 5.15 Contact `/contact/` + Booking `/book-consultation/`

- **Contact:** form fields that qualify (name, practice type, specialty, state, monthly claim volume, current billing setup, what's the biggest pain) + phone + email + hours + response-time promise ("reply within 1 business day") + chat. Qualifying fields = better sales calls. Form backend must notify your team + CRM instantly (see Part 6).
- **Booking:** Cal.com/Calendly embed with timezone-aware slots, "Free 30-min revenue assessment" + calendar integration + confirmation email + SMS reminder. Offer both "assessment call" and "instant demo of the dashboard".

---

### 5.16 Legal pages + 404

- **Privacy Policy / Terms of Service / Accessibility:** standard but real (don't copy from a generator without review; get them drafted properly).
- **404 page:** on-brand, with links to Services, Case Studies, and a search box. Track 404s in analytics and fix broken links monthly (their dead links are a lesson).

---

### 5.17 Client portal `/portal/` (application, not marketing page)

- Auth (SSO-ready), role-based access (practice owner / office manager / biller).
- **Dashboard KPIs:** clean claim rate, days in AR (by aging bucket), denial rate (by payer, by reason), collection rate, net collections (monthly trend), $ in pending status.
- **Claim-level view:** search/status/timeline per claim.
- **Reports:** exportable monthly statements (CSV/PDF), aging report, payer performance.
- **Documents:** secure upload/download vault (BAA signed before use).
- **Notifications:** email/SMS alerts on denials, payer changes, aged claims.
- Build on a HIPAA-compliant basis (Part 10). This is your moat — eBridge has nothing like it.

---

<a id="part-6"></a>
## Part 6 — Tech stack & system architecture

> For your team: production-grade, fast, scalable, and mostly free/low-cost to start. Two systems: the **marketing site** (public) and the **client portal + internal RCM engine** (your real product). A **headless content layer** powers both.

### 6.1 Recommended stack (marketing site)

| Layer | Choice | Why |
|---|---|---|
| Framework | **Next.js (App Router) + TypeScript** | SSR/ISR for SEO, edge rendering, component model your team knows |
| Styling | **Tailwind CSS + shadcn/ui** | Fast to build, consistent design system, accessible primitives |
| Content | **Headless CMS (Sanity or Contentful)** or **MDX files** | Structured content for 70+ pages incl. programmatic state/specialty pages; editorial workflow for blog |
| Data | **PostgreSQL (Supabase/Neon) + Prisma** | Single source of truth for states, specialties, payers, timely-filing tables, KPIs, testimonials, case studies |
| Forms/leads | Custom API route + **Resend** (email) + CRM webhook | Own your leads; no third-party form vendor lock-in |
| Booking | **Cal.com (self-host or embed)** | Timezone-aware, syncs to team calendars |
| Analytics | **Plausible or GA4 + GTM** | Privacy-friendly, fast; GA4 for ads later |
| Errors/monitoring | **Sentry** | Frontend error tracking |
| Hosting | **Vercel (or AWS Amplify / CloudFront+S3)** | Edge CDN, preview deployments, instant rollbacks |
| CI/CD | **GitHub Actions + Vercel previews** | Deploy previews per PR, Lighthouse CI gate (perf budget) |
| Testing | **Playwright** (E2E), **Vitest** (unit) | Regression safety on a site with 70+ templated pages |

**Why not WordPress?** Their site is WordPress/Elementor and that's exactly why it's slow and janky. Next.js gives you: 90+ Lighthouse scores, ISR for the programmatic pages (regenerate state/specialty pages when content DB updates), TypeScript safety on 70+ templates, and previews for your content writers.

### 6.2 The programmatic page engine (your SEO moat)

One schema → 50 state pages + 20 specialty pages + 12 service pages, all unique content:

```
content/
  states/{slug}.md          # intro, payer landscape, laws, credentialing notes, local FAQ
  specialties/{slug}.md     # codes, denials, payer quirks, FAQ
  data/
    timely-filing.json      # state × payer × claim-type → days (your editorial gold)
    payers.json             # names, plans, contact URLs
    kpis.json               # your real, audited stats
```

- Pages render via **ISR** (`revalidate: 3600`) — content writers edit in CMS, site rebuilds automatically
- **Single-source-of-truth:** timely-filing table drives both state pages AND the calculator — update once, everywhere
- Content QA: a lint script checks every generated page for minimum word count + unique paragraphs (kills the doorway-page problem)

### 6.3 Client portal + RCM engine (your product)

> Scope for your engineers. Start with the **read-only KPI dashboard** (fast win, massive trust signal), then add claim-level features.

| Module | MVP (month 1–2) | Later |
|---|---|---|
| Auth | NextAuth/Clerk, role-based access | SSO, MFA |
| Dashboard | KPI cards from data warehouse: clean claim rate, days in AR, denial rate, collection rate, net collections | Real-time-ish, payer drill-downs |
| Claims | — | Claim-level status feed (from your billing software's API or CSV sync), aging buckets |
| Reports | Monthly PDF export | Custom report builder |
| Documents | Secure vault (S3 + signed URLs + encryption) | eSignature |
| Notifications | Email alerts on denials | SMS, Slack/Teams webhooks |

**Data reality:** your portal's data comes from the billing system you use internally (Kareo, AdvancedMD, Waystar, athena, or your own engine). Integrate via their APIs or nightly CSV/EDI exports into a warehouse (Postgres → Redshift/BigQuery later). Never build a portal without a defined data source — define that in the very first sprint.

### 6.4 Automation differentiators (you're an engineer — use it)

- **Claim scrubber pre-submission** (error checking against payer rules → fewer denials) — measurable, publishable stat
- **Denial auto-classification** (categorize denial reasons from payer codes → targeted appeals) — great case-study fodder
- **Prior-auth tracking** with deadline alerts
- **Eligibility verification automation** via clearinghouse API (Availity/Waystar/Change)
- **Client-facing alerting** ("3 claims aged past 60 days with payer X")
- ⚠️ **Compliance guardrail:** automation assists humans; keep a certified coder/biller review step. Never claim "AI replaces certified coders" — payers and auditors will bite.

### 6.5 Environments & workflow

- `main` → production (Vercel) · preview per PR · staging mirror with sample data
- Content changes via CMS preview before publish
- Security: secrets in env vars/secret manager (never in repo), dependency scanning (Dependabot), image optimization built-in (next/image)

---

<a id="part-7"></a>
## Part 7 — SEO & content strategy

### 7.1 Keyword universe (three tiers)

| Tier | Keywords | Page type |
|---|---|---|
| **Money** | "medical billing services", "medical coding services", "credentialing services", "RCM company", "revenue cycle management company", "denial management services" | Services hub + detail pages |
| **Long-tail** | "medical billing for [specialty]", "[specialty] billing services [state]", "how much does medical billing cost", "medical billing percentage rates", "timely filing limit [state] [payer]" | Specialty × State pages, Pricing, State pages |
| **Content** | "how to read an EOB", "top denial reasons [specialty]", "CAQH explained", "how to appeal denied claim", "RAC audit preparation" | Blog + Resources |

Your programmatic engine means you can capture tier-2 at scale — but only if content is unique (Part 6.2 lint). **Start ranking tier-2 in states/specialties you actually serve.**

### 7.2 Technical SEO checklist

- [ ] Unique title (≤60 chars) + meta description (≤155) per page, templated with real data
- [ ] Canonical tags everywhere; no duplicate-title states/specialties
- [ ] `sitemap.xml` (auto-generated incl. all 70+ pages) + `robots.txt` + `rss.xml` for blog
- [ ] Next.js `metadata` API for OG/Twitter cards (shareable case studies = free distribution)
- [ ] Core Web Vitals budget (Part 8) — speed is a ranking factor
- [ ] Internal linking: every service ↔ specialties ↔ states ↔ blog cluster
- [ ] HTTPS + HTTP/3 + CDN (Vercel default)
- [ ] 404 tracking + monthly broken-link sweep

### 7.3 Local SEO (for the 1–2 states you start in)

- **Google Business Profile** (category: Medical Billing Service) with real photos, services, hours, and review collection automation
- Consistent NAP (name, address, phone) across directories (Yelp, BBB, Clutch, Healthgrades, Manta, local medical directories)
- Local backlinks: sponsor a medical association event, write for a local practice blog, guest posts on healthcare finance sites
- Location pages serve as landing pages for "medical billing [city]" searches

### 7.4 Structured data (JSON-LD) — implement everywhere

| Schema | Pages |
|---|---|
| `Organization`/`ProfessionalService` (logo, contact, geo, sameAs) | Global (layout) |
| `Service` (name, provider, areaServed, offers) | All service/specialty/state pages |
| `FAQPage` | All FAQ blocks + blog posts with FAQs |
| `BreadcrumbList` | Global |
| `Review`/`AggregateRating` | Reviews page (only real ratings) |
| `Article`/`BlogPosting` | Blog |
| `WebSite` + SearchAction (sitelinks search box) | Global |

### 7.5 Content calendar (first 90 days)

- **Week 1–4:** all core + service pages (priority: Home, Billing, Coding, Credentialing, AR Recovery, Pricing, Contact)
- **Week 5–8:** 8 specialties + 10 states (the ones you serve)
- **Week 9–12:** 12 blog posts (4/mo) + 2 case studies + 2 resources/calculators
- **Ongoing:** monthly blog ×4, quarterly case study, state/specialty expansion as you sign clients in new states

**Promotion:** LinkedIn (founder + team posts, publish the case studies), the blog feeds email nurture, Google Business posts weekly, and every case study gets an OG card + short video version.

---

<a id="part-8"></a>
## Part 8 — Performance & Core Web Vitals

**Budget (make it a CI gate — Lighthouse CI fails the build if exceeded):**

| Metric | Target | How to hit it |
|---|---|---|
| LCP | < 2.0s | next/image, preload hero image, no render-blocking third parties |
| INP | < 200ms | minimal client JS, no heavy libraries, lazy hydrate components |
| CLS | < 0.05 | fixed dimensions on images, no layout-shifting banners |
| TTFB | < 600ms | edge rendering (Vercel), ISR for static pages |
| Total JS | < 250KB | code-split, no jQuery/Elementor-era bloat |
| Page weight | < 1.5MB | WebP/AVIF, no 768px+ hero images at 1024px widths (their exact mistake) |

**Rules:** every image optimized & sized; fonts self-hosted or `display=swap` with `preload`; third-party scripts (chat, analytics, booking) loaded async/deferred; a single chat widget SDK, not three.

---

<a id="part-9"></a>
## Part 9 — Accessibility (WCAG 2.2 AA)

- Semantic landmarks (`header/nav/main/footer`), single `h1` per page, logical heading order
- All images `alt`; icons have `aria-label`; focus states visible; skip-to-content link
- Color contrast ≥ 4.5:1 (test with axe/Lighthouse)
- Forms: real `<label>`s, error messages announced (`aria-live`), not just color
- Mobile: touch targets ≥ 44px, no horizontal scroll at 320px, readable without zoom
- Interactive US map: keyboard navigable + list fallback for screen readers
- Run axe + Lighthouse accessibility checks in CI

---

<a id="part-10"></a>
## Part 10 — Security, privacy & HIPAA (the reality check)

**The marketing site itself** (no PHI): standard web security — HTTPS, security headers (CSP, HSTS, X-Frame-Options), rate-limited forms, spam protection (honeypot + provider verification), dependency scanning, no secrets in the repo.

**If/when you add PHI** (client portal, document vault, intake forms): you become a HIPAA **business associate** in practice terms. That means, before going live with any PHI-handling feature:

1. **Sign BAAs** with every subcontractor touching PHI (hosting, email, file storage, analytics with raw logs). Use providers that offer BAA out of the box (AWS, Azure, GCP, Supabase, Vercel's HIPAA tier if you go there).
2. **Access controls:** least-privilege, role-based, MFA for all staff, audit logs of PHI access.
3. **Data protection:** encryption in transit (TLS 1.2+) and at rest (AES-256), backups with retention policy, secure deletion.
4. **Incident response plan** + breach notification process (written, tested).
5. **Training:** all staff complete HIPAA/privacy training; keep records.
6. **Marketing truth rule:** publish a security one-pager that describes what you *actually* do. Do not claim "HIPAA certified" (no such certification exists) — say "HIPAA-compliant practices" with a BAA available.

> If this sounds like a lot: it is — which is exactly why most small billing firms don't do it, and why doing it right is a marketable differentiator. Start with the read-only portal (no PHI) to prove the concept, then add PHI features once the BAA/compliance groundwork is in place.

**Other compliance pages to get right:** Terms of Service (define pricing basis, contract terms, client responsibilities), Privacy Policy (GDPR/CCPA-friendly), and an OIG/RAC-audit-readiness stance on your Compliance content (shows domain authority).

---

<a id="part-11"></a>
## Part 11 — Conversion optimization

### 11.1 CTA hierarchy

- **Primary (every page):** "Get My Free Revenue Assessment" → booking page
- **Secondary:** "See Client Results" → case studies · "Talk to a Biller" → phone
- **Sticky mobile:** call button + "Book" (their site has a call button in top bar only; mobile users deserve a thumb-zone CTA)
- Every stat and case study card ends in a CTA — the reading → booking loop never breaks

### 11.2 Lead form design

- Fields: name, practice type, specialty, state, **monthly claim volume** (qualifier), current setup (in-house / other vendor / new practice), biggest pain (free text)
- Keep it short enough to finish in 60s; longer forms kill small-practice owners
- Success path: instant confirmation ("we reply within 1 business day") + calendar link + phone number
- Follow-up SLA: **< 4 business hours** on leads (they're warm for ~24h)

### 11.3 Objection-killers on every money page

- "Is switching hard?" → onboarding page + "How to switch billing companies" guide
- "Will you lock me in?" → no long-term contracts + cancel-anytime copy
- "Will you understand my specialty?" → specialty pages with real depth
- "Can I see results?" → dashboard demo + case studies
- "What does it cost?" → pricing page with ranges
- A/B test: pricing page with ranges vs. "get a quote" only (many firms win with ranges + calculator)

### 11.4 Live chat / AI assistant

- Rule: 24/7 availability claim requires 24/7 channel. Start with a human-hours chat (your team), add an AI assistant trained on your FAQ/services between hours. Chat transcripts feed your FAQ and your sales scripts.
- Capture email before chat or after 2 messages — every conversation is a lead.

---

<a id="part-12"></a>
## Part 12 — Analytics & measurement

| Metric | Tool | Review cadence |
|---|---|---|
| Sessions, pages, bounce, conversions | Plausible / GA4 | Weekly |
| Keyword rankings (money + long-tail) | Search Console + Ahrefs/Semrush (if budget) | Monthly |
| Form/booking/phone-call completions | GA4 events + Cal.com analytics + call tracking (CallRail) | Weekly |
| Lead → booked call → signed client | CRM pipeline (HubSpot/Attio/Pipedrive) | Weekly |
| Chat interactions & offline capture | Chat vendor analytics | Weekly |
| Lighthouse/CWV in production | Lighthouse CI + CrUX | Per deploy + monthly |
| 404s & broken links | GA4 + crawl (Screaming Frog monthly) | Monthly |

**North-star metric:** booked revenue assessments per week (site → call pipeline). Every improvement (pricing page, case studies, chat, speed) should move that number. Track it publicly in your weekly standup.

---

<a id="part-13"></a>
## Part 13 — Build roadmap (4 phases)

### Phase 0 — Foundations (Week 1–2)
- [ ] Company name, brand, logo, design system (colors, type, components)
- [ ] Repo + Next.js scaffold + CI (lint, typecheck, Lighthouse gate)
- [ ] Content DB schema (states, specialties, payers, timely-filing, KPIs, testimonials, case studies)
- [ ] Draft legal: Privacy, Terms, Accessibility
- [ ] Set up: domain, email, Google Business Profile, analytics, CRM, phone/voicemail, booking tool

### Phase 1 — Core site (Week 3–6)
- [ ] Universal template (header/footer/chat/sticky CTA) + Home
- [ ] Services hub + 12 service pages (template + content)
- [ ] About, Team, Pricing (+ guarantee), Contact, Booking
- [ ] HIPAA/Security, Payers, FAQ, Reviews
- [ ] Lighthouse ≥ 90 all categories; mobile-first QA

### Phase 2 — Programmatic SEO engine (Week 7–10)
- [ ] Specialty template + 8–20 specialty pages (real content)
- [ ] State template + 10–50 state pages with timely-filing tables
- [ ] Calculators (revenue leakage, timely filing)
- [ ] Blog live + first 8 posts
- [ ] Case studies: 2 published (from Phase 0–1 client work — start doing client work NOW, not later)

### Phase 3 — Portal & automation (Week 11–16)
- [ ] Client portal v1: auth + KPI dashboard (no PHI)
- [ ] Data pipeline from your billing system → dashboard
- [ ] Claim scrubber + denial classification automation (internal)
- [ ] Notifications (denial alerts to clients)
- [ ] AI chat assistant (FAQ-trained) after hours

### Phase 4 — Scale (Month 5+)
- [ ] Expand specialties/states as you sign clients there (data-first)
- [ ] Video case studies + quarterly results page update
- [ ] Paid ads (Google Search: money keywords; LinkedIn: founder content) once case-study proof exists
- [ ] Referral program for practices + partner program for smaller billing firms

---

<a id="part-14"></a>
## Part 14 — Master launch checklist

**Content (all written, proofread ×2, no placeholder names):**
- [ ] 12 core pages, 12 service pages, 8–20 specialties, 10+ states, pricing, case studies ×2, blog ×8
- [ ] Every stat traceable to proof; every testimonial real + named + permitted

**Trust:**
- [ ] Google Business Profile live + review collection running
- [ ] Named team with credentials; founder story
- [ ] Guarantee drafted with counsel; BAA template ready
- [ ] Security one-pager honest and accurate

**Technical:**
- [ ] Lighthouse ≥ 90 (perf/SEO/accessibility/best practices); CWV budget in CI
- [ ] sitemap, robots, schema on all templates, canonical-free duplicates
- [ ] Forms → CRM + email with < 4h SLA; booking calendar live
- [ ] Analytics + call tracking + error monitoring live
- [ ] 404 page + broken-link sweep scheduled monthly

**Launch sequence:**
1. Ship Phase 1 core site (no "under construction" anywhere)
2. Submit sitemap to Search Console; request indexing on key pages
3. Publish launch LinkedIn posts (founder story + case study #1)
4. Announce to any existing clients/network → first Google reviews
5. Weekly content cadence begins; review North-star metric every Monday

---

*End of blueprint. Build order priority: **trust elements > core pages > SEO engine > portal**. When in doubt, ask: "does this page make a skeptical practice owner trust us more?" If not, fix it before shipping.*





