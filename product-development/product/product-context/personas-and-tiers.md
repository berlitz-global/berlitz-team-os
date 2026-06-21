# Personas & Tiers

> **Status:** Living reference
> **Last Updated:** 2026-06-21
> **Source:** Board Update - Product/Technology (June 2, 2026); `strategy/business-context/berlitz-jtbd-and-users.md`
> **Used by:** All PRDs

This is the single source of truth for learner personas and subscription tiers. PRDs reference this doc rather than defining personas inline.

---

## Learner Personas

### Explorer (Free, $0/mo) [~]

- **Segment:** B2P free tier, casual or evaluating
- **Goals:** Try language practice without commitment, build a basic habit
- **Berlitz usage:** Unlimited drills (pronunciation, vocabulary, grammar). No conversation sessions, no avatar, no human sessions
- **Conversion role:** Top of funnel. Drill habit is the hook that converts to Plus/Career
- **Note:** Proposed persona - not yet in the canonical persona doc. The cost model assumes a $0 free tier but this persona needs formal sign-off. See Practice Drills PRD OQ-6.

### Hobbyist Hana (Plus, $19/mo)

- **Segment:** B2P self-serve, casual learner
- **Goals:** Practice consistently, build a habit, improve gradually without big commitment
- **Frustrations:** Most apps feel shallow; no real human feedback; paying feels risky before seeing value
- **Berlitz usage:** Unlimited AI practice (drills + conversation), 2 AI tutor sessions/mo; generates learning data for the platform
- **Tier economics:** Break-even + data

### Professional Pedro (Pro, $49/mo)

- **Segment:** B2P self-serve, working professional
- **Goals:** Improve practical communication for work, see measurable progress, mix AI and human practice
- **Frustrations:** Limited time, needs efficient sessions, wants outcomes not just lessons
- **Berlitz usage:** 6 credits/mo, unlimited AI practice, 4 AI tutor + 2 human sessions
- **Tier economics:** Core profit driver

### Career Carla (Career, $39/mo)

- **Segment:** B2P self-pay, often funded for/by work (B2B self-pay)
- **Goals:** Business English or a specific professional skill (role-play + human), credential to show employers
- **Frustrations:** Generic language apps don't cover business contexts; needs proof of skill acquisition
- **Berlitz usage:** 6 credits/mo, unlimited AI practice, 4 AI tutor + 1 human session, 1 free skill module

### Executive Elena (Premium, $99/mo)

- **Segment:** B2P premium / sponsored by enterprise
- **Goals:** High-touch, high-quality coaching with maximum human access; relocation/culture and skills programs
- **Frustrations:** Needs flexibility, premium quality, and fast outcomes; low tolerance for friction
- **Berlitz usage:** 16 credits/mo, unlimited AI practice, 8 AI tutor + 4 EU human sessions; skills/culture bundles
- **Tier economics:** High LTV and margin

### Enterprise HR Buyer - Buyer Ben (Enterprise, custom)

- **Segment:** B2B enterprise / mid-market decision maker
- **Goals:** Prove ROI, track skill gaps via pre/post assessments, integrate with HRIS, certify outcomes
- **Frustrations:** Hard to demonstrate L&D impact; needs verifiable proof of value and "time to fluency" metrics
- **Berlitz usage:** Admin-managed credit pools, ROI dashboards, manager feedback loops, certification; NRR target ~120%

### Instructor Ingrid (supply side)

- **Segment:** Supply side - the platform's strategic moat
- **Goals:** Coach effectively, see learner context, minimize manual prep, schedule with low friction
- **Frustrations:** 0% learner data shared from sales; no first-5-minute personalization; 10-15 min/session lost to manual tasks; observations lost between sessions
- **Target metrics:** 60-65% utilization (vs. 45.7%), instructor NPS >70, prep-time reduction >40%

---

## Tier Summary

| Tier | Price | AI Practice | AI Tutor Sessions | Human Sessions | Avatar | Credits |
|------|-------|------------|-------------------|---------------|--------|---------|
| Free | $0/mo | Drills only (unlimited) | - | - | No | - |
| Plus | $19/mo | Unlimited (drills + conversation) | 2/mo | - | Simli | - |
| Pro | $49/mo | Unlimited | 4/mo | 2/mo | Simli | 6/mo |
| Career | $39/mo | Unlimited | 4/mo | 1/mo | Simli | 6/mo |
| Premium | $99/mo | Unlimited | 8/mo | 4/mo | HeyGen | 16/mo |
| Enterprise | Custom | Unlimited | Custom | Custom | HeyGen | Pool |

---

## Feature Entitlements by Tier

| Feature | Free | Plus | Pro | Career | Premium | Enterprise |
|---------|------|------|-----|--------|---------|------------|
| Pronunciation drills | Yes | Yes | Yes | Yes | Yes | Yes |
| Vocabulary drills + Wordbook | Yes | Yes | Yes | Yes | Yes | Yes |
| Grammar exercises | Yes | Yes | Yes | Yes | Yes | Yes |
| AI conversation (audio-only) | - | Yes | Yes | Yes | Yes | Yes |
| AI conversation (avatar) | - | Yes (Simli) | Yes (Simli) | Yes (Simli) | Yes (HeyGen) | Yes (HeyGen) |
| Human sessions | - | - | Yes | Yes | Yes | Yes |
| Business content modules | - | - | - | Yes | Yes | Yes |
| Skills/culture bundles | - | - | - | - | Yes | Yes |
| Admin dashboard + ROI | - | - | - | - | - | Yes |
| SSO/SAML | - | - | - | - | - | Yes |
