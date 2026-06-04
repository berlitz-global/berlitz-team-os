# Berlitz Product & Technology Roadmap — 2026–2027

**Source:** Board Update — Product/Technology (June 2, 2026)
**Audience:** Board, P&T leadership
**Last Updated:** 2026-06-04

## 2026 Roadmap — Building Key Components

The 2026 plan sequences a move toward the "ideal app experience" across the year, building core components from the learner-facing apps through scheduling and into a future-proofed billing and payment foundation.

| Milestone | Target | Notes |
|---|---|---|
| Learner WebApp (English) 1–4 | September 2026 | First web experience release |
| Learner Mobile App | October 2026 | One-market test |
| Scheduling (F2F & Online) | November 2026 | — |
| Future-proof Billing & Payment | December 2026 | New revenue platform foundation |
| Operational Efficiency | Through 2026 | Ongoing workstream |
| Financial Audit Readiness | Through 2026 | Ongoing workstream |

The overall trajectory moves from the current state toward the ideal app experience over time, with billing/payment as the culminating end-of-year deliverable.

## Commercial Architecture Migration

A parallel track replaces Salesforce/STAR's CPQ approach with a modular commercial stack. The principle: eliminate complexity through product standardization (fixed tiers, fixed bundles, transparent pricing), after which CPQ is no longer needed — only a clean way to turn a closed deal into a signed contract and a live credit pool (CLM).

| Commercial task | What replaces CPQ | Tool |
|---|---|---|
| Generate enterprise quote | Standardized tier pricing page + contract template on deal close | HubSpot + Ironclad |
| Apply custom discounting | Discounts negotiated and recorded at contract level | Ironclad |
| Multi-country legal terms | Country-specific, legal-approved, version-controlled templates | Ironclad |
| Credit pool setup on close | Webhook auto-creates credit pool on eSign completion | Ironclad → Metronome |
| Revenue recognition | Meter usage → invoice → apply AR/DR rules | Metronome + Stripe + NetSuite |
| Contract renewals | Automated alerts 90/60/30 days before expiry; synced pipeline | Ironclad + HubSpot |
| Amendment tracking | Versioned contract records with full audit trail | Ironclad |

### Revenue Platform Cost Profile

The target stack is modeled at a fraction of the $8–9M/year Salesforce cost:

- **Salesforce (CRM only):** 150k–200k/year (vs. $8–9M); one-time ~60k, 6–8 weeks
- **Contracts/CLM:** 40k–80k/year; one-time ~50k, 6–7 weeks
- **Monetization (Metronome):** 30–40k/year + usage; one-time ~150k, 8–10 weeks
- **Payments (Stripe):** ~0.5% of revenue; one-time via Connor Group, ETA October
- **Finance (NetSuite):** 400–500k/year; one-time via Connor Group, ETA October

## Dual-Track Delivery Strategy

To protect growth from legacy drag, work runs on two tracks:

- **Legacy:** keep existing customers happy; maintenance only, no new features, manual fixes. Trying to "fix" it would waste millions and delay growth.
- **Growth engine:** drive all new growth (B2P & B2B) on a greenfield system — new tech, reconfigured billing outside Salesforce, new scheduling. Benefit: fast, scalable, compliant, profitable.

The recommended STAR remediation path is a "bypass" rather than a "fix": a one-time greenfield build with low (controlled-migration) risk, MVP in 6 months and full migration in 18 months — versus the ~$150k/month, 18+ month "fix" path.

## 2027 Product Package — Languages, Skills & Culture

By end of 2027 the package expands beyond language into skills and culture access. Baseline: 1 credit = $5, AI practice unlimited and free, AI tutor = 1 credit/session, human sessions = 1–2 credits.

| Tier | Price/mo | Credits | Language Access | Skills Access | Culture Access | Est. Profit |
|---|---|---|---|---|---|---|
| Free | €0 | 1 lifetime | Unlimited AI practice; 1 demo class | — | — | -$3 to -$8 |
| Plus | $19 | 2/mo | Unlimited AI practice; 2× AI Tutor | 10% off bundles | 10% off bundles | ~$9 to $12 |
| Pro | $49 | 6/mo | Unlimited AI practice; 4× AI Tutor; 2× LATAM teacher | 15% off bundles | 15% off bundles | ~$22 to $26 |
| Premium | $99 | 16/mo | Unlimited AI practice; 8× AI Tutor; 4× EU teacher | 1 skill bundle/year | 20% off bundles | ~$38 to $45 |
| Career | $39 | 6/mo | Unlimited AI practice; 4× AI Tutor; 1× EU teacher | 1 skill module free (role play + human) | — | ~$14 to $17 |
| Enterprise | Custom | Admin-managed, pooled | Unlimited AI practice | All skills programs | All culture programs | Highest, NRR ~120% |

The expansion path is Languages → Skills → Culture, with skills/culture programs (e.g., EU AI Act $299/person, Business Negotiation $349/person, Presentation Skills $499/person, relocation/culture programs $499/person) creating additional enterprise expansion revenue.

### 2026 MVP Package (for reference)

The initial 2026 launch package uses the same credit baseline with markets phased in: US (Enterprise, Premium, Career), LATAM (Free, Plus & Pro), Germany (Enterprise, Career), Japan (Free, Plus & Enterprise), India (Free, Plus & Pro), and UK + France (Enterprise & Career).

## Work That Remains

**Product packages:**

- Pricing discovery via Van Westendorp method
- Value discovery via MaxDiff survey
- Conjoint analysis on overall product packages
- 10–15 HR buyer qualitative interviews (Switch interviews, JTBD definitions)
- Resolve pricing units: Languages in credits, Skills/Culture in dollars

**Go-to-market team:**

- Brand repositioning plan
- Clear launch plan across markets
- Free-tier acquisition strategy
- Corporate partnerships
- Growth team budgets and scaling
