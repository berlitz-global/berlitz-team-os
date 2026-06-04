# Berlitz - Business Info

**Source:** Board Update — Product/Technology (June 2, 2026)
**Last Updated:** 2026-06-04

# Company Overview

- **Product framing:** Product at Berlitz is a measurable communication outcome delivered via AI, humans, content, and operational intelligence. Not "Course = Product" but "Outcome + Experience + Monetization + Intelligence = Product."
- **Strategic direction:** Pivot to "Digital-First B2B" to drive 10x growth, with focus on B2P and B2B; move product from "Human-Only" to "AI-Hybrid" (scale with AI, quality with humans).
- **Product categories:** Learn Language (fluency, conversation, pronunciation); Learn Skills (compliance, regulation, presentation, negotiations); Learn Culture (localization, etiquette, cross-cultural communication).
- **Delivery model:** Role-play, simulation, assessments, AI tutor, human coach, personalization, enterprise reports.
- **Commercial layer:** Credit-based consumption, AI + human hybrid delivery, usage-based monetization, subscription + consumption.

# Target Market

- **B2P / Self-serve (Volume & Speed):** millions of individual learners practicing daily.
- **B2B / Enterprise (Depth & Validation):** enterprises and HR buyers purchasing programs for teams and demanding outcomes and ROI.
- **Segments:** B2P & SMBs (consistency & habit formation), Mid-Market (flexibility with consistency), Enterprise (maximum control & efficiency).
- **Launch markets:** US (Enterprise, Premium, Career), LATAM (Free, Plus & Pro), Germany (Enterprise, Career), Japan (Free, Plus & Enterprise), India (Free, Plus & Pro), UK + France (Enterprise & Career).

# Pricing

Credit-based model. Baseline: **1 credit = $5**, AI practice unlimited and free, AI tutor = 1 credit/session, human sessions = 1–2 credits.

Three credit structures by segment:

- **Use It or Lose It** (B2P & SMBs): drives engagement, predictable consumption, simpler to manage.
- **Rollover Credits** (Mid-Market): unused credits roll forward and expire after a window; fair and flexible, better for seasonal usage.
- **Admin-Managed Pools** (Enterprise): admin allocates per user/team with real-time usage and visibility; centralized budget control and ROI reporting.

2026 MVP launch tiers:

| Tier | Price/mo | Credits | AI Practice | AI Tutor | Human Sessions | Best For |
|------|----------|---------|-------------|----------|----------------|----------|
| Free | €0 | 1 lifetime | Unlimited | 1 demo class | 1 demo class | Acquisition hook with video |
| Plus | $19 | 2/mo | Unlimited | 2 sessions | Not included | Hobbyists — break-even + data |
| Pro | $49 | 6/mo | Unlimited | 4 sessions | 2 sessions (LATAM) | Professionals — core profit driver |
| Premium | $99 | 16/mo | Unlimited | 8 sessions | 4 sessions (EU) | Executives — high LTV & margin |
| Career | $39 | 6/mo | Unlimited | 4 sessions | 1 session (EU) | Professionals needing business English (B2B self-pay) |
| Enterprise | Custom | Admin-managed | Unlimited | Pooled | Pooled | ROI-driven |

# Key Metrics & Assets

Supply-side strengths (the "instructor moat"):

- 97.8% student satisfaction
- 3.83/4 eCFF quality score
- 84% of instructors would recommend Berlitz; 80% are excited
- 5-year average instructor tenure
- Instructor utilization target: 60–65% (vs. 45.7% current)

MVP unit economics (per 1,000 signups): +$5.1k/month gross profit, +$9.6k MRR, $650 LTV (Career), $48 ARPU (paid users). Modeled on 20% free-to-paid conversion, ~20 AI sessions/free user at ~$0.10, 6% monthly churn.

| Tier | Users | Revenue | AI Cost | Teacher Cost | Gross Profit | LTV |
|------|-------|---------|---------|--------------|--------------|-----|
| Free | 800 | $0 | $1.6k | $0 | -$1.6k | — |
| Plus | 60 | $1.1k | $120 | $0 | $849 | $317 |
| Pro | 60 | $2.9k | $120 | $225 | $2.2k | $817 |
| Career | 40 | $1.6k | $80 | $200 | $1.0k | $650 |
| Premium | 40 | $4.0k | $80 | $600 | $2.7k | $1,650 |
| **Total** | **1,000** | **$9.6k** | — | — | **+$5.1k** | — |

# Competitive Landscape

Berlitz targets the unoccupied intersection of unlimited AI practice, human teaching, and certified outcomes.

| Competitor | Pricing | AI Practice | Human Teachers | Weaknesses vs. Berlitz |
|------------|---------|-------------|----------------|------------------------|
| Duolingo | Free / $7–14/mo; Super $84/yr | Unlimited (best in class) | None | No human teachers, shallow outcomes, not B2B, low ARPU |
| Babbel | $14/mo or $84/yr | Limited, mostly content | Group add-on | Weak AI, no 1:1 premium teacher, no B2B |
| Italki | $5–80/session | Minimal | 10,000+ tutors | No AI, no outcomes tracking, no B2B, no certification |
| Preply | $15–40/hr; Business separate | Growing (beta) | 40,000+ tutors | Inconsistent quality, no owned curriculum, weak outcomes data (closest B2B+human+AI competitor) |
| Rosetta Stone | $12–36/mo; enterprise | Speech AI (older) | Limited live | Outdated UX, weak AI, losing share (displacement opportunity) |
| Busuu | Free / $14/mo | AI grammar | Community only | No 1:1 human teachers, weak AI depth |
| **Berlitz (target)** | **$0–99/mo** | **Unlimited, free all tiers** | **LATAM + EU/native, credit-gated** | Must build consumer app, engagement UX, AI investment |

# Salesforce / STAR Context

STAR (Salesforce-based platform, 2023–24) was intended to replace LCMS/COSMOS for order-to-cash, billing, delivery, and scheduling, with revenue recognition passed to NetSuite daily. Germany (~50 LCMS instances) and Poland migrated successfully, but per-country rollout behaves like "building a house, not turning a key" (2–4 months even for small countries). The rev-rec architecture is considered critically flawed; independent audits (Hubbl) found 84 high-severity security flaws; the system is ~94% custom-built atop 130,000+ lines of obsolete code. Total modeled STAR spend 2022–2027 is **$45.16M** (~$8–9M/year), motivating the move of scheduling, billing, and monetization off Salesforce.
