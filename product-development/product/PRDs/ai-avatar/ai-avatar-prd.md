# AI Avatar Experience - PRD

| Field | Value |
|-------|-------|
| **Author** | Jan Hoffmann, PM |
| **Status** | Draft |
| **Last Updated** | 2026-06-21 |
| **Related RFC** | TBD - see Decisions Requiring PDRs below |
| **Related Plan** | `engineering/design/plans/ai-tutor-architecture.md` |
| **Related Research** | `product-context/ai-avatar-tutor-spec-research.md`, `product/PRDs/feature-matrix.md`, `competitive-research/strategic-positioning.md` |
| **Dependencies** | Upstream: `ai-conversation/ai-conversation-prd.md` (the conversation product this avatar mode renders), `curriculum-factory/curriculum-factory-prd.md` (content). Sibling: `practice-drills/practice-drills-prd.md` (drills) |

---

## Overview

The AI Avatar Experience is the visual presentation layer that wraps the AI Conversation Experience in an animated 3D character with lip-sync, expressions, gestures, and customisable appearance and dialect. It is one of two modes the learner can choose (the other being audio-only). Everything about conversation steering, corrections, Berlitz Method, and CEFR bounding lives in the AI Conversation Experience PRD - this PRD covers only what is avatar-specific: rendering, visual quality, appearance customisation, dialect selection, uncanny valley mitigation, and avatar-specific cost management.

Given the avatar comes with a cost, the primary target users will be from the paid tiers, with the highest contributing margin coming from B2B.

---

## 1. Problem Statement

1. **A voice-only AI conversation is functional but not immersive.**
   - Audio-only lacks social presence, visual engagement, and non-verbal cues (gestures, expressions, eye contact)
   - The avatar adds the engagement layer that motivates learners to return
   - Evidence: agent behavior (gesture, gaze) improves transfer (d ~= 0.4-0.8; Mayer & DaPra 2012; Davis 2018); voice principle (d ~= 0.74; Mayer 2014); personalization principle (d ~= 1.1)
   - Learning gain from a face alone is small (image principle ~null) - the value is engagement, not instruction (spec research 3.1-3.2)

2. **Competitive parity requires a visual avatar.**
   - Praktika (5/5 avatar rating, $35.5M Series A) is the direct benchmark
   - Duolingo launched video avatar "Lily"
   - Without avatar, Sep 2026 launch lacks the flagship visual feature (spec research 5.1; strategic-positioning.md)

3. **The avatar must be customisable for a global learner base.**
   - A single fixed avatar cannot represent learners across Berlitz's launch markets (US, LATAM, Germany, Japan, India, UK, France)
   - Learners need to select appearance and dialect/accent fitting their context - e.g., a Japanese learner practising British English for a London posting

---

## 2. Business Opportunity

### Why the avatar layer specifically

The conversation product works without the avatar (audio-only mode). The avatar is justified by three business cases:

| Business lever | Impact |
|---------------|--------|
| Competitive positioning | Anchors the "High AI" axis. Without avatar, launch lacks a flagship differentiator. Praktika validates demand. (strategic-positioning.md) |
| Engagement & retention | Avatar sessions drive habit formation through immersive practice. Session return rate target: >=40% within 7 days [~]. Audio-only usage is 10x avatar on current HeyGen setup - but we believe this is a UX quality issue, not a format problem [~]. |
| Free-to-paid conversion | Avatar is the highest-engagement feature for driving upgrades. Target: +20% relative conversion lift [~]. |
| Enterprise deal enablement | AI avatar is a top-line demo feature for enterprise sales. [~] |

### Avatar-specific costs (v0.2.8)

The avatar render is the only cost component unique to this PRD. All other AI costs (LLM, ASR, TTS, pronunciation) are in the AI Conversation Experience.

| Tier group | Avatar vendor | Render cost/min | Render cost per 30-min session | Added % of total AI session cost |
|-----------|-------------|----------------|-------------------------------|--------------------------------|
| Free | No avatar (voice-only) | $0 | $0 | 0% |
| Plus-Career | Simli Trinity-1 | $0.01/min | 0.276€ | 55% of 0.507€ total |
| Premium-Enterprise | HeyGen LiveAvatar Lite | $0.10/min | 2.76€ | 92% of 2.991€ total |

The avatar render is the single largest AI cost line for paid tiers. This is why:
- Free tier has no avatar (cost control)
- Self-hosting and on-device rendering need to be on the roadmap to lower avatar costs, enabling the avatar as the default app interface and allowing avatar access in the free tier as a conversion tool (free trial)

(cost model v0.2.8)

> For how these compose with conversation costs, see [Cost Model Summary](../../product-context/cost-model-summary.md).

---

## 3. Why Now

1. **Avatar tech is now viable at enterprise cost.** Simli, HeyGen, and Tavus have reached sub-$0.10/min at volume. Open-source alternatives (MuseTalk, LivePortrait) are approaching real-time. Not viable 18 months ago. (spec research 4.2)

2. **Sep 2026 launch needs visual differentiation.** The Learner App web launch is Sep 2026. Avatar is the feature that makes it look like an AI product, not a courseware app. (roadmap)

3. **Praktika is the direct competitor.** 5/5 avatar rating, $35.5M raised, claims 20M+ learners. Berlitz must match visual quality while adding curriculum depth. (spec research 5.1)

---

## 4. Customer Requests

- [~] HeyGen usage data shows audio-only usage is 10x avatar (HeyGen usage dashboard, May 2026). Root cause unclear - see OQ-4
- No direct customer requests for avatar specifically. Demand is inferred from competitive benchmarking (Praktika) and engagement research (Mayer, Davis)
- **Validation plan:** User research during AI Conversation Experience dogfood (Aug 2026) will include avatar preference questions. >=5 learner interviews. Owner: PM

---

## 5. Goals & Success Metrics

### Avatar-specific metrics

| Metric | Definition | Baseline | Target | Timeframe |
|--------|-----------|----------|--------|-----------|
| Avatar adoption rate | % of paid-tier AI sessions that use avatar mode (vs audio-only) | ~10% on current HeyGen [~] | >=30% [~] | GA + 90 days |
| Avatar uncanny valley rate | % of post-session feedback rating appearance as "unnatural" | N/A (new) | <5% | GA + 30 days |
| Free-to-paid conversion lift (avatar) | A/B test: free users shown avatar demo session vs audio-only only. Exposure = completed >=1 avatar demo. MDE ~1pp on ~5% base requires ~15k users per arm [~]. | ~5% [~] | +20% relative lift [~] | GA + 90 days |
| All-in cost per avatar minute (Free-Career) | Total AI session cost including avatar render | N/A | <=$0.05/min | Launch |
| All-in cost per avatar minute (Premium/Enterprise) | Same, higher-quality avatar | N/A | <=$0.15/min | Launch |

All other metrics (speaking time, session return, completion, efficacy) are owned by the AI Conversation Experience PRD - they measure the conversation quality, not the visual layer.

### Guardrails

| Guardrail | Threshold | Action | Monitoring |
|-----------|-----------|--------|------------|
| Avatar render cost per minute | Must not exceed 1.5x tier target for >24h | Alert PM + Engineering; investigate vendor billing | Daily cost aggregation from `avatar.session.cost` |
| Uncanny valley rate | Must not exceed 10% | Disable avatar for affected vendor tier; fall back to audio-only | Weekly from `avatar.session.feedback` |
| Render latency | Must not exceed 200ms sustained >1h | Alert; if >250ms, rollback to audio-only | Real-time from avatar render pipeline |

### Instrumentation (avatar-specific events)

> **Full schema:** See [Instrumentation Schema](../../product-context/instrumentation-schema.md) for the complete event schema across all products.

These supplement the `ai.*` events defined in the AI Conversation Experience PRD:

| Event | Payload | Metrics it feeds |
|-------|---------|-----------------|
| `avatar.render.started` | `avatar_vendor`, `avatar_config` (appearance, dialect) | Avatar adoption rate, cost |
| `avatar.session.cost` | `avatar_render_cost` | Cost per minute by tier |
| `avatar.session.feedback` | `appearance_natural` (boolean), `appearance_rating` (1-5), `free_text` | Uncanny valley guardrail |

**Derived:**
- **Avatar adoption rate** = COUNT(`ai.session.started` WHERE mode=avatar) / COUNT(`ai.session.started` WHERE tier IN paid_tiers)
- **Uncanny valley rate** = COUNT(WHERE `appearance_natural` = false) / COUNT(WHERE `appearance_natural` IS NOT NULL)

### Non-goals

- **Conversation quality, corrections, Berlitz Method** - owned by AI Conversation Experience PRD.
- **Multiple avatar personas with distinct personalities** - post-MVP. Single customisable avatar at launch.
- **Scene/environment variety** - post-MVP. Single or minimal scene at launch.
- **Conversation recording & playback with avatar replay** - post-MVP (C6).
- **Photorealism as a goal** - evidence supports investing in voice, gesture, and feedback quality over visual fidelity. (spec research 3.4)

---

## 6. User Stories

### Any learner (avatar-specific stories)

**US-1: Customise avatar appearance**
As a learner, I want to choose my avatar's appearance (gender, skin tone, clothing style) so that the conversation partner feels relatable and comfortable to practice with.

*Acceptance criteria:*
- Learner can select from a set of appearance options before their first avatar session
- Selection persists across sessions and devices
- Changing appearance does not interrupt an active session (applied on next session start)

**US-2: Select avatar dialect/accent**
As a learner, I want to choose the avatar's spoken dialect/accent (e.g., neutral American English, British English, Castilian Spanish) so that I practise hearing and responding to the accent relevant to my learning goal.

*Acceptance criteria:*
- Available accents are tied to the target language (not all accents available for all languages)
- Selection persists across sessions
- Accent change takes effect from the next AI utterance (no session restart required)

**US-3: Graceful degradation on poor connection**
As a learner on a slow connection, I want the session to continue in audio-only mode rather than freeze or stutter, so that I don't lose my practice time.

*Acceptance criteria:*
- On connections <2 Mbps, avatar gracefully falls back to audio-only with transcript
- Learner is informed: "Switched to audio mode - your connection is slow"
- Session data (corrections, speaking time) is preserved regardless of mode switch

### Executive Elena (Premium)

**US-4: Premium visual quality**
As Executive Elena, I want the avatar to feel polished - no visible lip-sync artifacts, natural expressions - so that it matches the premium quality I expect.

*Acceptance criteria:*
- No visible lip-sync artifacts or expression glitches on a stable connection (>=5 Mbps)
- HeyGen LiveAvatar quality tier for Premium/Enterprise
- Avatar responds to conversation context with appropriate facial expressions (not a fixed smile)

---

## 7. Requirements

### Functional Requirements

| ID    | Requirement                                                                                                                                                                                                                                                                                                 | Priority | Source                                               |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ---------------------------------------------------- |
| FR-01 | System shall render a single animated 3D avatar with lip-sync synchronized to TTS output, facial expressions responsive to conversation context (minimum: smile on positive feedback, concerned expression on repeated errors, neutral on exposition), and voice consistent with Berlitz brand personality. | P0       | Feature matrix C1; architecture Layer C              |
| FR-02 | Learner shall be able to customise the avatar's visual appearance (e.g., gender, skin tone, clothing style) and select the avatar's spoken dialect/accent for the target language. Selection persists across sessions.                                                                                      | P1       | Feature matrix C1 extensions; architecture B4        |
| FR-03 | Avatar shall provide visual cues when delivering corrections (hand gesture on correction delivery) or when the learner is stuck (leaning forward, encouraging expression). Minimum 3 distinct gesture types at launch.                                                                                      | P1       | Architecture Layer C; Davis 2018 (gesture d ~= 0.36) |
| FR-04 | On degraded connections (<2 Mbps), system shall gracefully fall back to audio-only mode with transcript, preserving session data.                                                                                                                                                                           | P1       | US-3                                                 |

### Non-Functional Requirements

| ID | Requirement | Target | Rationale |
|----|------------|--------|-----------|
| NFR-01 | **Uncanny valley:** Must avoid uncanny valley effects | <5% negative appearance feedback | Evidence favors stylized over photoreal. Avatar style is an **open question for design/engineering**. (spec research 3.3) |
| NFR-02 | **Cost (Plus-Career):** Avatar render cost per minute | <=$0.01/min (Simli Trinity-1) | At 30 min/session, 0.276€ render cost. (cost model v0.2.8) |
| NFR-03 | **Cost (Premium/Enterprise):** Avatar render cost per minute | <=$0.10/min (HeyGen LiveAvatar Lite) | Higher fidelity justified by tier revenue. (cost model v0.2.8) |
| NFR-04 | **Self-hosted path:** Architecture must support migration to self-hosted avatar render | Migration achievable by 2027 without redesign | MuseTalk/LivePortrait approaching real-time. Self-hosted drives cost toward ~$0.005/min. (spec research 4.5) |
| NFR-05 | **Render latency:** Avatar render must not add more than 150ms at dogfood, tightening to <100ms at GA | Dogfood: <150ms; GA: <100ms render overhead | The AI Conversation Experience targets <500ms total; avatar render gets at most 100ms of that budget at GA. |
| NFR-06 | **Component modularity:** Avatar render vendor swappable without session architecture changes | Swap Simli <-> HeyGen <-> self-hosted without touching conversation logic | Vendor market moving fast; lock-in is a strategic risk. |

---

## 8. AI Evaluation Plan (Avatar Visual Quality)

The avatar render is probabilistic - lip-sync timing, expression selection, and gesture triggering vary per utterance and depend on vendor model, network conditions, and conversation context.

### Evaluation dimensions

| Dimension | Method | Launch | Target | Aspirational |
|-----------|--------|--------|--------|-------------|
| Lip-sync accuracy | Audio-visual offset measured in ms (automated) | <150ms offset | <100ms offset | <80ms offset |
| Expression appropriateness | Human eval on sample of N=20 sessions per release, rated on 3-point rubric (appropriate / neutral / inappropriate) | >=80% appropriate | >=90% appropriate | >=95% appropriate |
| Gesture relevance | Human eval - does the gesture match the conversational context (correction, encouragement, greeting)? | >=70% relevant | >=85% relevant | >=90% relevant |

### Guardrails (visual quality)

| Rule | Threshold | Action | Fallback |
|------|-----------|--------|----------|
| Lip-sync offset >200ms for >5% of utterances in a session | Per-session check | Log `avatar.quality.degraded`; if >10% of sessions affected, disable avatar tier | Fall back to audio-only for affected sessions |
| Expression glitch (frozen face, wrong emotion) | Manual QA + user reports | Investigate vendor; if systemic, disable until patch | Audio-only fallback |

### Eval infrastructure

- Lip-sync offset measurement tool must be operational before Phase 2 beta entry. Owner: Engineering.
- Human eval sample (N=20 sessions) reviewed per release. Owner: Design + QA.

---

## 9. Launch Plan

The avatar experience launches in sync with the AI Conversation Experience. Avatar launches in **Beta** with web (Sep 2026) and reaches **GA** with mobile (Oct 2026). Web users receive the GA-quality avatar update in October. Phases below are avatar-specific gates layered on top of the conversation product's launch plan.

### Phase 1: Internal Dogfood (Aug 2026)

**Avatar-specific entry criteria:**
- Avatar renders in browser with lip-sync and expressions
- At least one appearance customisation option functional (dialect selection can be stubbed)

**Avatar-specific exit criteria:**
- No P0 visual bugs (lip-sync drift, render crashes)
- Qualitative feedback on avatar style collected from >=20 internal users
- Render latency <150ms [~]

### Phase 2: Beta (Sep 2026)

**Avatar-specific entry criteria:**
- Appearance and dialect customisation functional
- Graceful degradation on slow connections implemented
- Cost per avatar minute within tier targets

**Avatar-specific exit criteria:**
- Uncanny valley rate <10% [~] (relaxed for beta; tighten to <5% for GA)
- Avatar adoption rate >=15% of paid-tier sessions [~]

### Phase 3: GA (Oct 2026)

**Avatar-specific entry criteria:**
- iOS and Android apps render avatar correctly
- Uncanny valley rate <5%
- All appearance/dialect options available for English

**Rollback plan:**
- Feature flag disables avatar per-user, per-tier, or globally
- Fallback: audio-only mode with transcript - same AI engine, no render
- Rollback trigger: render latency >200ms sustained, uncanny valley rate >10%, or avatar render cost >2x target

---

## 10. Decisions Requiring PDRs

| Decision | Current position | Why it needs a PDR | When |
|----------|-----------------|-------------------|------|
| **Tiered avatar vendor strategy** | Simli for Plus-Career, HeyGen for Premium/Enterprise | Locks vendor negotiations and architecture integration. Switching post-launch is expensive. | Before engineering starts (Jul 1 2026) |
| **Avatar style** | Open - evidence favors stylized (spec research 3.3) | Visual identity of the product's flagship feature; affects brand, engineering, and design. | Before Phase 1 dogfood (Aug 2026) |
| **Build vs buy (Talkio replacement)** | Assumes building in-house (shared with AI Conversation Experience PRD) | Commits ~26k€/year savings against engineering investment. | Before engineering starts (Jul 1 2026) |

---

## 11. Open Questions

| # | Question | Owner | Status | Source |
|---|----------|-------|--------|--------|
| 1 | **Avatar style:** Stylized vs semi-realistic vs photoreal? Evidence favors stylized but needs brand and user preference testing. | Design + Engineering | Open | spec research 3.3 |
| 2 | **Avatar at MVP confirmed?** If not confirmed by Jul 1, audio-only ships first; this PRD is deferred. | PM + Engineering | Open - must resolve by Jul 1 2026 | architecture doc section 6 |
| 3 | **Avatar render technology:** Web-based (Three.js) vs native (Unity/Unreal)? Impacts mobile performance and dev cost. | Engineering | Open - must resolve by Jul 1 2026 | architecture doc section 8 |
| 4 | **Why is avatar usage 10x lower than audio-only on HeyGen?** Is this a UX/quality issue or a fundamental user preference? Needs user research. | PM | Open | Internal HeyGen usage data |
| 5 | **Appearance customisation scope:** How many options at launch? Min viable set for global markets? | Design | Open | |
| 6 | **Dialect/accent availability:** Which accents per language at launch? Tied to TTS vendor capabilities. | Engineering + Content | Open | architecture B4 |

---

## Sources

### Internal
- Spec research: `product-context/ai-avatar-tutor-spec-research.md`
- Architecture: `engineering/design/plans/ai-tutor-architecture.md`
- Feature matrix: `product/PRDs/feature-matrix.md`
- Cost model: `strategy/business-context/berlitz_cost_model_v0.2.8.xlsx`
- AI Conversation Experience PRD: `PRDs/ai-conversation/ai-conversation-prd.md`

### Avatar and multimedia evidence
- Schroeder, Adesope & Gilbert 2013 - Pedagogical agent meta-analysis (g ~= 0.19)
- Mayer 2014 - Voice principle (d ~= 0.74), personalization (d ~= 1.1), image principle (~null)
- Mayer & DaPra 2012 - Gesture/gaze (d ~= 0.4-0.8)
- Davis 2018 - Gesture retention (g ~= 0.36)
- Mori 1970/2012 - Uncanny valley
- Mathur & Reichling 2016 - Uncanny valley empirical confirmation

### Market
- Praktika Series A ($35.5M, May 2024)
- Speak Series C ($1B valuation, Dec 2024)
