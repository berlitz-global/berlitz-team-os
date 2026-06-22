# Personas & Tiers

> **Status:** Living reference
> **Last Updated:** 2026-06-21
> **Source:** Board Update - Product/Technology (June 2, 2026); `strategy/business-context/berlitz-jtbd-and-users.md`
> **Used by:** All PRDs

This is the single source of truth for learner personas and subscription tiers. PRDs reference this doc rather than defining personas inline.

---

## Learner Personas

| Persona | Tier | Segment | Goals | Frustrations | Berlitz usage | Economics |
|---------|------|---------|-------|-------------|--------------|-----------|
| **Explorer** [~] | Free ($0/mo) | B2P free tier, casual or evaluating | Try language practice without commitment, build a basic habit | - | Unlimited drills (pronunciation, vocabulary, grammar). No conversation, no avatar, no human sessions | Top of funnel - drill habit converts to Plus/Career. Note: proposed persona, not yet in canonical doc. See Practice Drills PRD OQ-6. |
| **Hobbyist Hana** | Plus ($19/mo) | B2P self-serve, casual learner | Practice consistently, build a habit, improve gradually without big commitment | Most apps feel shallow; no real human feedback; paying feels risky before seeing value | Unlimited AI practice (drills + conversation), 2 AI tutor sessions/mo | Break-even + data |
| **Professional Pedro** | Pro ($49/mo) | B2P self-serve, working professional | Improve practical communication for work, see measurable progress, mix AI and human practice | Limited time, needs efficient sessions, wants outcomes not just lessons | 6 credits/mo, unlimited AI practice, 4 AI tutor + 2 human sessions | Core profit driver |
| **Career Carla** | Career ($39/mo) | B2P self-pay, often funded for/by work | Business English or a specific professional skill, credential to show employers | Generic language apps don't cover business contexts; needs proof of skill acquisition | 6 credits/mo, unlimited AI practice, 4 AI tutor + 1 human session, 1 free skill module | - |
| **Executive Elena** | Premium ($99/mo) | B2P premium / sponsored by enterprise | High-touch coaching with maximum human access; relocation/culture and skills programs | Needs flexibility, premium quality, fast outcomes; low tolerance for friction | 16 credits/mo, unlimited AI practice, 8 AI tutor + 4 EU human sessions; skills/culture bundles | High LTV and margin |

## Non-Learner Personas

| Persona | Segment | Goals | Frustrations | Berlitz usage | Key metrics |
|---------|---------|-------|-------------|--------------|-------------|
| **Buyer Ben** (Enterprise HR) | B2B enterprise / mid-market decision maker | Prove ROI, track skill gaps via pre/post assessments, integrate with HRIS, certify outcomes | Hard to demonstrate L&D impact; needs verifiable proof of value and "time to fluency" metrics | Admin-managed credit pools, ROI dashboards, manager feedback loops, certification | NRR target ~120% |
| **Instructor Ingrid** | Supply side - the platform's strategic moat | Coach effectively, see learner context, minimize manual prep, schedule with low friction | 0% learner data shared from sales; no first-5-minute personalization; 10-15 min/session lost to manual tasks; observations lost between sessions | Learner info persisted across sessions, AI-assisted lesson prep, self-study activity feed | 60-65% utilization (vs. 45.7%), instructor NPS >70, prep-time reduction >40% |

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
