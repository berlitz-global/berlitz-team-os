# AI Avatar Conversation Mode — PRD

| Field | Value |
|-------|-------|
| **Author** | Jan Hoffmann, PM |
| **Status** | Draft |
| **Last Updated** | 2026-06-16 |
| **Related RFC** | TBD |
| **Related Plan** | `engineering/design/plans/ai-tutor-architecture.md` |
| **Related Research** | `product-context/ai-avatar-tutor-spec-research.md`, `PRDs/feature-matrix.md`, `competitive-research/strategic-positioning.md` |

---

## Overview

The AI Avatar is the animated conversation partner inside the Berlitz Learner App's AI Tutor module. It delivers guided conversation, role-play, real-time feedback, and Berlitz Method-compliant teaching through a visual 3D character with lip-sync, expressions, and voice. This PRD covers Avatar conversation mode only — the seven MVP features from the feature matrix (C1, C2, C4, C5, C7, C8, C9). Audio-Only drill mode is a separate PRD.

The primary target user is **Professional Pedro** (Pro tier, $49/mo) — the core profit driver. The avatar's job is to maximize low-stakes speaking practice volume while delivering salient, self-repair-eliciting feedback grounded in the Berlitz Method.

---

## 1. Problem Statement

1. **Speaking anxiety limits practice volume.** Speaking is consistently learners' most anxiety-inducing activity (MacIntyre & Gardner; Young 1990). Krashen's affective filter hypothesis holds that anxiety blocks input processing — and by extension, output willingness. Learners who need to speak more avoid doing so because speaking raises anxiety. (spec research 2.2)

2. **Classroom settings cannot deliver enough speaking reps.** Swain's output hypothesis demonstrates that producing language forces syntactic processing via noticing gaps, hypothesis-testing, and reflection — input alone is insufficient. Yet in a typical group class, individual speaking time is measured in single-digit minutes per hour. An AI conversation partner can deliver 10-20x more speaking reps per session at zero marginal instructor cost. (spec research 2.2)

3. **The productive tension between these two problems is the core opportunity.** Swain says *push* speaking; Krashen warns pushing speaking *raises* anxiety. An AI avatar uniquely resolves both — high-volume, low-stakes speaking reps mitigate both objections at once. No classroom or human tutoring model can match this combination of volume and safety. (spec research 2.2, line 99)

4. **Current third-party dependency is costly and limiting.** Berlitz currently spends ~EUR26k [~] on Talkio for avatar-based conversation practice (Jan Hoffmann, Teams, May 18 2026). This spend buys a generic tool that cannot enforce the Berlitz Method, follow Berlitz curriculum, or integrate with the learner profile. Building in-house unlocks curriculum integration, method compliance, and a path to lower unit costs. (spec research 1.4)

---

## 2. Business Opportunity

### Strategic positioning

Berlitz targets the **unoccupied top-right quadrant** (High AI + High Human) in the competitive landscape. No competitor combines deep AI conversation practice with deep human coaching today. The avatar is the flagship AI-depth feature that anchors this position. (strategic-positioning.md)

### Competitive threat

- **Praktika** ($35.5M Series A, May 2024; claims 20M+ learners [vendor-claim]) is the only competitor rated 5/5 on AI Avatar. They are the direct benchmark. (spec research 5.1)
- **Speak** ($1B valuation, $162M raised; OpenAI-backed) is 5/5 on voice but has no visual avatar. They threaten on speech quality. (spec research 5.1)
- **Preply** (moving right toward AI) and **Speak** (moving up toward B2B/teachers) are converging on Berlitz's target quadrant. Speed to market matters. (strategic-positioning.md)

### Revenue model

The avatar is available across all tiers as part of unlimited AI practice. Revenue comes from tier subscriptions, not per-avatar-minute billing to the learner:

| Tier | Price/mo | Target persona | Est. profit/user |
|------|----------|---------------|-----------------|
| Free | EUR0 | Acquisition hook | -$3 to -$8 |
| Plus | $19 | Hobbyist Hana | ~$9-12 |
| Career | $39 | Career Carla | ~$14-17 |
| Pro | $49 | Professional Pedro | ~$22-26 |
| Premium | $99 | Executive Elena | ~$38-45 |
| Enterprise | Custom | Buyer Ben | Highest, NRR ~120% |

(roadmap; business-info.md)

### Business levers

| Business lever | Impact |
|---------------|--------|
| Free-to-paid conversion | Avatar is the highest-engagement feature in the free tier; exposure drives upgrade to Plus/Pro. Target: +20% relative conversion lift [~]. |
| Competitive positioning | Anchors the "High AI" axis of Berlitz's target quadrant. Without avatar, Sep 2026 launch lacks a flagship AI differentiator. (strategic-positioning.md) |
| Talkio cost elimination | Replaces ~EUR26k/year [~] third-party spend with an owned, integrated capability. (spec research 1.4) |
| Retention / engagement | Avatar sessions drive habit formation through immersive practice. Session return rate target: >=40% within 7 days [~]. |
| Enterprise deal enablement | AI avatar conversation is a top-line demo feature for enterprise sales; validates the "AI + Human" pitch to Buyer Ben. [~] |

### Build-vs-buy trigger

Current ~EUR26k [~] avatar spend on Talkio. The cost model targets $0.01/min (Simli) to $0.10/min (HeyGen LiveAvatar Lite) for avatar render, with an on-device path at ~$0.005/min. All-in enterprise avatar minute (avatar + voice + LLM + pronunciation) at roughly $0.10-0.15/min [~], dominated by the avatar render. Self-hosted render/TTS by 2027 would drive all-in cost toward ~$0.005/min. (spec research 1.4, 4.2)

### Unit economics constraint

At 120 min/week (high-engagement user) = ~516 min/month:

| All-in cost/min | Monthly cost | vs Pro ($49) | vs Plus ($19) |
|-----------------|-------------|-------------|--------------|
| $0.10 | $51.60 | Exceeds revenue | 2.7x revenue |
| $0.05 | $25.80 | 53% of revenue | 1.4x revenue |
| $0.01 | $5.16 | 11% of revenue | 27% of revenue |

At 60 min/week (realistic heavy avatar use) = ~258 min/month: $0.05/min = $12.90/month — sustainable across Pro and Premium tiers.

The cost model already tiers by plan: Simli ($0.01/min render) for Free-Career, HeyGen ($0.10/min) for Premium/Enterprise. This drives the NFR cost targets below.

---

## 3. Why Now

1. **Praktika and Speak are well-funded and growing.** Praktika raised $35.5M (May 2024) with a purpose-built avatar product; Speak is at $1B valuation with OpenAI backing. Both are gaining market share in the speaking-practice segment Berlitz must own. (spec research 5.1)

2. **Sep 2026 web launch needs a flagship differentiator.** The Learner App web launch is Sep 2026. The avatar is the highest-visibility feature that demonstrates Berlitz's AI investment and anchors the "High AI + High Human" positioning. Without it, the launch looks like another courseware app. (roadmap)

3. **Avatar technology is now viable at enterprise cost.** Real-time avatar APIs (Simli, HeyGen, Tavus) have reached sub-$0.10/min at volume, with latency approaching the ~500ms natural turn-taking threshold. Open-source alternatives (MuseTalk, LivePortrait) are approaching real-time on consumer GPUs. The tech was not cost-viable 18 months ago. (spec research 4.2)

4. **Talkio replacement is urgent.** ~EUR26k [~] annual spend on a tool that cannot enforce Berlitz Method, follow Berlitz curriculum, or feed the learner profile. Every month on Talkio is wasted spend and missed integration. (spec research 1.4; Jan Hoffmann, Teams, May 18 2026)

5. **Convergence threat from both directions.** Preply is adding AI to its human-tutoring marketplace; Speak is adding B2B and enterprise features to its AI platform. Both are moving toward Berlitz's target quadrant. The window to establish the top-right position is narrowing. (strategic-positioning.md)

---

## 4. Customer Requests

> All customer quotes below are marked `[~]` — no customer call transcripts have been recorded yet. Internal signals from Teams discussions serve as proxies.

| Source | Customer / Segment | Date | Verbatim |
|--------|-------------------|------|----------|
| Teams message | Jan Hoffmann / Internal PM | May 18 2026 | "is that the avatar we pay 26k for?" [~] (paraphrase — exact wording from Teams, not a customer quote) |
| Teams message | Chayan Roy / Internal Engineering | Jun 3 2026 | Raised question on MVP scope for micro-lessons and how existing course content flows into AI avatar practice [~] (paraphrase) |
| Competitive intel | Praktika / Market signal | Mid-2026 | 20M+ claimed learners [vendor-claim] and 5/5 avatar rating in competitive matrix — validates market demand for visual AI conversation partners |

[~] Customer verbatims to be collected during beta. Placeholder for quotes from learners on speaking anxiety, practice volume needs, and avatar engagement.

---

## 5. Goals & Success Metrics

### Baseline collection plan

No avatar-mode baselines exist today. Baselines will be set in two passes:

1. **Pre-build (by Jul 15 2026) — owner: PM + Analytics.** Extract from Talkio usage data: average session duration, learner speaking time per session (if available), session return rate, and session completion rate. If Talkio does not expose speaking-time breakdowns, the baseline is "unknown" and Phase 2 beta becomes the baseline window.
2. **Phase 2 beta (Sep 2026) — owner: Analytics.** First two weeks of beta are the baseline collection period. All GA targets below are provisional until beta baselines are confirmed. If a beta baseline materially changes the target (e.g., speaking time baseline is already 8+ min), PM will revise targets before GA.

### Primary metric

**Speaking time per session** — minutes of active learner speech per avatar session. This is the metric that proves the mode drives the output practice that learning science says matters (Swain's output hypothesis). If learners aren't speaking, the avatar is just a chatbot with a face.

- **Baseline:** ~3-4 min learner speaking in a 15-min Talkio session [~] (to be confirmed from Talkio data by Jul 15 2026; if unavailable, set from Phase 2 beta first two weeks)
- **Target:** >=8 min of learner speaking in a 15-min session [~]
- **Timeframe:** Measured from GA (Oct 2026)

### Engagement metrics

| Metric | Definition | Baseline | Target | Timeframe |
|--------|-----------|----------|--------|-----------|
| Session return rate | % of users who start a 2nd avatar session within 7 days of their 1st | ~25% [~] (Talkio estimate; confirm by Jul 15 or set from beta) | >=40% [~] | GA + 30 days |
| Session completion rate | % of avatar sessions where the learner reaches the scenario goal or natural ending (not early exit) | ~50% [~] (Talkio estimate; confirm by Jul 15 or set from beta) | >=65% [~] | GA + 30 days |
| Weekly avatar sessions | Average avatar sessions per active user per week | ~1.2 [~] (Talkio estimate; confirm by Jul 15 or set from beta) | >=2 [~] | GA + 90 days |

### Business metrics

| Metric | Definition | Baseline | Target | Timeframe |
|--------|-----------|----------|--------|-----------|
| Free-to-paid conversion lift | Conversion rate for users exposed to avatar vs not (A/B) | ~5% free-to-paid conversion [~] (modeled from business-info.md 20% assumption across all tiers; avatar-specific baseline from beta A/B control group) | +20% relative lift (i.e., 5% -> 6%) [~] | GA + 90 days |
| All-in cost per avatar minute (Free-Career) | Total cost of LLM + ASR + TTS + pronunciation + avatar render per minute | N/A (new capability) | <=$0.05/min | Launch |
| All-in cost per avatar minute (Premium/Enterprise) | Same, higher-quality avatar tier | N/A (new capability) | <=$0.15/min | Launch |

### Efficacy metrics (longer-term)

| Metric | Definition | Baseline | Target | Timeframe |
|--------|-----------|----------|--------|-----------|
| CEFR progression rate | Rate of CEFR sub-level advancement for avatar users vs non-avatar users | Set from GA cohort (first 30 days, non-avatar control group) | Avatar users advance CEFR sub-levels at >=1.3x the rate of non-avatar users [~] | GA + 6 months |

Grounded in VanLehn's ITS ceiling of d ~= 0.76 (matching human tutors) and field-RCT realistic range of g ~= 0.3-0.5. The 1.3x target is conservative relative to the literature and reflects the avatar's role as an engagement layer rather than a primary instructional mechanism. Do not expect "2-sigma" outcomes — that claim is contested and has not replicated at scale. (spec research 2.1)

### Guardrails

| Guardrail | Threshold | Rationale |
|-----------|-----------|-----------|
| Voice-to-first-audio latency p95 | <500ms | Stivers et al. (2009): human turn-taking gaps average ~200ms; >500ms feels unnatural. (spec research 4.1) |
| Berlitz Method compliance score | >=90% (internal QA rubric) | Sessions must follow immersive L2, Q&A cycles, gentle correction. Eval framework scores against real teacher benchmark. (architecture doc, section 5) |
| All-in cost per avatar minute | Within tier budget (see Business metrics above) | Exceeding cost targets erodes unit economics — see unit economics section above. |
| Avatar uncanny valley incidents | <5% of session feedback mentions "creepy," "weird," or "unnatural" appearance [~] | Uncanny valley evidence shows near-photoreal faces with imperfect motion create aversion. (spec research 3.3) |

### Instrumentation

Every success metric above must be computable from logged events on launch day. The following events are required in the analytics pipeline. Event names use `snake_case`; all events carry `session_id`, `user_id`, `tier`, `cefr_level`, and `timestamp`.

| Event | Payload (key fields) | Metrics it feeds |
|-------|---------------------|-----------------|
| `avatar.session.started` | `scenario_id`, `scenario_type` (guided / role_play), `mode` (avatar / audio_only) | Session completion rate, weekly sessions, cost |
| `avatar.session.ended` | `end_reason` (goal_reached / time_up / learner_exit / error), `duration_ms` | Session completion rate, return rate |
| `avatar.utterance.learner` | `duration_ms`, `transcript`, `asr_confidence` | Speaking time per session |
| `avatar.utterance.tutor` | `duration_ms`, `latency_ms` (voice-to-first-audio) | Latency guardrail, speaking time ratio |
| `avatar.correction.delivered` | `correction_type` (grammar / pronunciation / vocabulary), `strategy` (prompt / recast / hint), `learner_response` (self_repair / ignored / n/a) | Berlitz Method compliance, feedback quality |
| `avatar.feedback.surfaced` | `feedback_type` (pronunciation_flag / vocab_suggestion / fluency_cue), `severity` | Live feedback coverage (C9) |
| `avatar.scenario.goal_reached` | `scenario_id`, `turns_taken`, `time_to_goal_ms` | Session completion rate |
| `avatar.session.cost` | `avatar_render_cost`, `asr_cost`, `tts_cost`, `llm_cost`, `pronunciation_cost`, `total_cost` | Cost per minute by tier |
| `avatar.session.feedback` | `nps_score`, `free_text`, `appearance_rating` | Uncanny valley guardrail, NPS |
| `avatar.eval.compliance` | `session_id`, `compliance_score`, `violations[]` | Berlitz Method compliance guardrail |

**Derived metrics:**
- **Speaking time per session** = SUM(`avatar.utterance.learner.duration_ms`) per `session_id`
- **Session return rate** = COUNT(users with >=2 `avatar.session.started` within 7 days of first) / COUNT(users with >=1)
- **Session completion rate** = COUNT(`avatar.session.ended` WHERE `end_reason` IN (goal_reached, time_up)) / COUNT(`avatar.session.started`)
- **Latency p95** = PERCENTILE(95, `avatar.utterance.tutor.latency_ms`)
- **Cost per minute** = `avatar.session.cost.total_cost` / (`avatar.session.ended.duration_ms` / 60000)

**Dependency:** Analytics engineering must confirm the event pipeline can ingest these events and compute derived metrics before Phase 2 beta entry. Owner: Analytics + Engineering.

### Non-goals

- **C3: Open Conversation** — post-MVP. MVP delivers guided and role-play scenarios only.
- **C6: Conversation Recording & Playback** — post-MVP. No avatar replay at launch.
- **C10: Crosstalk Mode (L1<->L2 bilingual)** — post-MVP. MVP is immersive L2 only per Berlitz Method.
- **Audio-Only drill features (Section B)** — separate PRD. Different interaction mode.
- **Human Teaching Integration (Section F)** — all post-MVP. Teacher cockpit, handoff, etc.
- **Enterprise Admin (Section I)** — all post-MVP. Admin dashboards, SSO, etc.
- **Multiple avatar personas** — post-MVP. Single avatar at launch.
- **Scene/environment variety** — post-MVP. Single or minimal scene at launch.
- **Photorealism as a goal** — evidence supports investing in voice, gesture, and feedback quality over visual fidelity. (spec research 3.4)

---

## 6. User Stories

### Professional Pedro (primary target — Pro, $49/mo)

**US-1: Guided conversation for work scenarios**
As Professional Pedro, I want to practice a structured business conversation with the AI avatar (e.g., presenting project updates to a client), so that I build speaking confidence for real work situations without the anxiety of practicing with a colleague.

*Acceptance criteria:*
- Avatar presents a scenario with clear objectives and vocabulary focus
- Conversation follows Berlitz curriculum structure for Pedro's CEFR level
- Pedro speaks for >=50% of the session duration
- Avatar provides gentle inline corrections without breaking conversation flow
- Post-session summary shows grammar/vocabulary/pronunciation performance

**US-2: Role-play for meeting preparation**
As Professional Pedro, I want to role-play a specific work scenario (job interview, client negotiation, team standup) with the avatar playing the other role, so that I rehearse real conversations I'll have this week.

*Acceptance criteria:*
- Pedro selects from pre-defined role-play scenarios relevant to business contexts
- Avatar plays the assigned role convincingly (appropriate register, vocabulary, pacing)
- Avatar adapts to Pedro's responses (not scripted — follows scenario intent but responds naturally)
- Corrections are salient and elicit self-repair ("Can you try that again?" rather than silent recast)

**US-3: Efficient practice between meetings**
As Professional Pedro, I want to start an avatar session quickly (under 30 seconds from app open to speaking), so that I can practice during a 15-minute break between work meetings.

*Acceptance criteria:*
- Session start (app open to first avatar utterance) takes <30 seconds
- Pedro can choose "quick start" with a recommended scenario based on his curriculum position
- Session can end naturally at any point without penalty

### Hobbyist Hana (Plus, $19/mo)

**US-4: Low-pressure conversation practice**
As Hobbyist Hana, I want to have a casual conversation with the avatar about everyday topics (ordering coffee, asking for directions, small talk), so that I practice speaking without feeling judged.

*Acceptance criteria:*
- Avatar's tone is encouraging and conversational (Mayer personalization principle, d ~= 1.1)
- Corrections are gentle and contextual, not clinical
- Language is constrained to Hana's CEFR level (~95-98% known vocabulary)
- Hana receives positive reinforcement for attempting difficult structures

### Career Carla (Career, $39/mo)

**US-5: Business role-play for career advancement**
As Career Carla, I want to role-play a job interview in my target industry with the avatar, so that I can practice articulating my experience and skills in the target language.

*Acceptance criteria:*
- Role-play scenarios include business-specific contexts (interviews, presentations, negotiations)
- Avatar asks follow-up questions that push Carla to elaborate (Swain output hypothesis)
- Post-session feedback highlights business-relevant vocabulary and formal register usage

### Executive Elena (Premium, $99/mo)

**US-6: Premium conversation experience**
As Executive Elena, I want the avatar interaction to feel polished and professional — natural voice, responsive timing, no awkward pauses — so that it matches the premium quality I expect at my tier.

*Acceptance criteria:*
- Voice-to-first-audio latency p95 <500ms (Stivers threshold)
- Avatar uses high-quality TTS with natural prosody
- No visible lip-sync artifacts or expression glitches during normal conversation
- Conversation maintains context across the full session (no repetition or topic amnesia)

---

## 7. Requirements

### Functional Requirements

| ID | Requirement | Priority | Feature | Source |
|----|------------|----------|---------|--------|
| FR-01 | System shall render a single animated 3D avatar with lip-sync synchronized to TTS output, facial expressions responsive to conversation context, and voice consistent with Berlitz brand personality. | P0 | C1 | Feature matrix C1; architecture Layer C |
| FR-02 | Avatar shall deliver scenario-based dialogue following Berlitz curriculum: each session has defined learning objectives, vocabulary bounds, grammar focus, and success criteria loaded from the Scenario Library. | P0 | C2 | Feature matrix C2; architecture A3, B1 |
| FR-03 | System shall support pre-defined role-play scenarios from Berlitz curriculum (job interview, client meeting, hotel check-in, etc.) where the avatar plays one character and the learner plays the other. | P0 | C4 | Feature matrix C4; architecture A3 |
| FR-04 | Avatar shall correct grammar errors inline during conversation using salient, self-repair-eliciting prompts (e.g., "Can you try saying that differently?") rather than implicit recasts, consistent with the Berlitz Method's gentle correction style. | P0 | C5 | Feature matrix C5; Lyster & Ranta 1997; spec research 2.3 |
| FR-05 | System prompts shall enforce Berlitz Method compliance: immersive L2 use (minimize L1), question-answer cycles, graduated difficulty, gentle error correction, and encouragement patterns. | P0 | C7 | Feature matrix C7; architecture A4 |
| FR-06 | AI tutor output shall be constrained to the learner's CEFR level: vocabulary, grammar structures, sentence complexity, and speaking speed bounded by what the learner has been exposed to in their curriculum position (~95-98% known vocabulary). | P0 | C8 | Feature matrix C8; Hu & Nation 2000; architecture A5 |
| FR-07 | System shall provide real-time, multi-dimensional feedback during sessions: pronunciation flags, vocabulary suggestions, and fluency cues surfaced alongside grammar correction — gentle and salient, without breaking conversational flow. | P0 | C9 | Feature matrix C9; spec research 2.3 |
| FR-08 | System shall display a real-time transcript alongside the avatar during conversation, with inline correction highlights for grammar and vocabulary. | P1 | C2/C5 | Architecture Layer C |
| FR-09 | Avatar shall provide visual cues and prompts when the learner is stuck (silence >5 seconds [~]): sentence starters, vocabulary hints, or rephrased questions. | P1 | C2 | Architecture B7 |
| FR-10 | Post-session review shall include: full transcript, grammar notes, new vocabulary list, pronunciation scores, session summary, and scenario goal completion status. | P1 | C2/C9 | Architecture Layer C shared UI |
| FR-11 | System shall support "quick start" — learner can begin a recommended scenario within 30 seconds of app open, based on their curriculum position and learner profile. | P2 | C2 | US-3 |

### Non-Functional Requirements

| ID | Requirement | Target | Rationale |
|----|------------|--------|-----------|
| NFR-01 | **Latency:** Voice-to-first-audio response time | p95 <500ms | Stivers et al. (2009): human turn-taking gaps average ~200ms across 10 languages; all means fall within ~500ms. Beyond 500ms feels unnatural; beyond 1s feels laggy. Architecture decision (S2S vs pipeline vs hybrid) is engineering's call — this sets the requirement, not the solution. (spec research 4.1) |
| NFR-02 | **Avatar style:** Must avoid uncanny valley effects | <5% negative appearance feedback [~] | Mori (1970/2012): affinity drops sharply near (not at) full realism, and motion amplifies the dip. Mismatched/atypical features and inconsistent realism (realistic face + imperfect lip-sync) drive eeriness. Evidence favors stylized over photoreal — but avatar style is an **open question for design/engineering**. Present the evidence; don't prescribe the solution. (spec research 3.3) |
| NFR-03 | **Speech:** Must support both natural conversation feel AND pronunciation-level feedback simultaneously | Natural conversation + phoneme/word-level scoring available per utterance | Native S2S (OpenAI Realtime) gives best conversational feel but does not expose phoneme-level pronunciation scores. A pipeline (STT->LLM->TTS) yields transcripts and scoring hooks but adds latency. The architecture is engineering's call — the requirement is that both capabilities must be available within the same session. (spec research 4.4) |
| NFR-04 | **CEFR bounding:** AI output constrained to learner's level | ~95-98% known vocabulary in AI utterances | Hu & Nation (2000): reading comprehension drops sharply below ~95-98% known vocabulary. Applied as a design heuristic for spoken output complexity. (spec research 2.5) |
| NFR-05 | **Cost (Free-Career tiers):** All-in cost per avatar minute | <=$0.05/min | All-in = LLM + ASR + TTS + pronunciation scoring + avatar render. At 60 min/week avatar use (~258 min/month), $0.05/min = $12.90/month — sustainable for Pro ($49) and Career ($39). Simli ($0.01/min render) is the assumed avatar vendor for these tiers. |
| NFR-06 | **Cost (Premium/Enterprise tiers):** All-in cost per avatar minute | <=$0.15/min | Higher-quality avatar render (HeyGen LiveAvatar Lite at $0.10/min) justified by tier revenue ($99-custom). At 60 min/week, $0.15/min = $38.70/month — within Premium margin. |
| NFR-07 | **Component modularity:** Every vendor component independently swappable | Avatar render, ASR, TTS, LLM, pronunciation scoring each swappable without session architecture changes | The avatar/speech market is moving fast — vendor lock-in at this stage is a strategic risk. Session orchestrator must abstract vendor-specific APIs behind stable internal interfaces. |
| NFR-08 | **Self-hosted path:** Architecture must support migration to self-hosted avatar render and TTS | Migration achievable by 2027 without session architecture redesign | Open-source alternatives (MuseTalk, LivePortrait) are approaching real-time. Self-hosted render + TTS drives all-in cost toward ~$0.005/min. Internal `features.md` P2 roadmap already plans this. (spec research 4.5) |
| NFR-09 | **Concurrent sessions:** System must support expected concurrent avatar sessions at launch | >=100 concurrent sessions [~] | Launch-week estimate; scale with demand. |
| NFR-10 | **Accessibility:** Avatar mode must meet WCAG 2.1 AA | Full transcript available as text alternative; keyboard navigation; screen reader compatibility | Feature matrix J6 requires WCAG 2.1 AA across the app. |

---

## 8. AI Evaluation Plan

The avatar's core loop is LLM-driven conversation — the same input produces different outputs. This section defines how we evaluate the AI's pedagogical behavior, what model capabilities are required, and how we handle failure modes.

### Evaluation methodology

**Automated eval suite (run on every model or prompt change):**

1. **Scenario corpus:** A set of >=30 scripted synthetic-learner sessions [~] spanning A1-B2, covering guided conversation and role-play, with known-correct teaching behaviors annotated. Each scenario defines: learner CEFR level, expected correction opportunities, expected L2 immersion, expected Q&A cycle count, and expected encouragement instances.
2. **LLM-as-judge scoring:** Each session is scored by a separate LLM judge against the Berlitz Teaching Rubric (derived from annotated real teacher-learner recordings — architecture doc section 5). The judge scores five dimensions:
   - **L2 immersion:** % of avatar utterances in target language (target: >=98%)
   - **Correction accuracy:** % of grammar corrections that are linguistically correct (target: >=95%)
   - **Correction strategy:** % of corrections using salient prompts vs implicit recasts (target: >=80% prompts)
   - **CEFR bounding:** % of avatar vocabulary within learner's level band (target: >=95%)
   - **Q&A cycle adherence:** % of turns following question-answer-feedback pattern (target: >=70%)
3. **Human audit sample:** 10% of beta sessions [~] are reviewed by a Berlitz Method expert against the same rubric. Inter-rater reliability between LLM judge and human auditor is tracked; if kappa <0.6, recalibrate the judge.

**Composite Berlitz Method compliance score** = weighted average of the five dimensions above. Weights TBD with Berlitz Method expert.

### Eval thresholds

| Level | Compliance score | When |
|-------|-----------------|------|
| **Launch gate** | >=85% | Phase 2 beta entry |
| **Target** | >=90% | GA (Oct 2026) |
| **Aspirational** | >=95% | GA + 6 months |

If compliance drops below 85% on any automated eval run, the prompt/model change is blocked from deployment.

### Model capability requirements

The conversational AI core (FR-02, FR-04, FR-05) requires the following LLM capabilities. These inform model selection but do not prescribe a specific provider.

| Capability | Requirement | Rationale |
|-----------|------------|-----------|
| Context window | >=32k tokens | Full-session memory for a 20-min conversation (~8k-12k tokens of dialogue) plus scenario definition, system prompts, learner profile, and correction history |
| Multilingual fluency | Native-quality output in target language at CEFR C2 | Avatar must model correct target-language usage; output quality cannot be below C2 |
| Instruction following | Reliable adherence to system prompts under adversarial user input | Berlitz Method compliance depends on the LLM following pedagogical system prompts even when the learner goes off-script or speaks L1 |
| Structured output | JSON or function-calling support | Correction events, feedback metadata, and scenario state must be extractable programmatically for logging and eval |
| Latency (TTFT) | <300ms time-to-first-token [~] | Leaves ~200ms budget for ASR + TTS + avatar render to hit the <500ms end-to-end target |

### AI failure modes and guardrails

| Failure mode | Detection | Threshold | Action | Fallback |
|-------------|-----------|-----------|--------|----------|
| **L1 leakage** — avatar speaks in learner's L1 instead of target language | Automated: language detection on every `avatar.utterance.tutor` transcript | >2% of avatar utterances in L1 per session | Alert + session flagged for review; if systemic (>5% of sessions), block prompt/model deployment | Avatar prefixes response with target-language redirect: "[Target language] Let's continue in [language]..." |
| **Incorrect grammar correction** — avatar "corrects" something that was actually correct, or provides a wrong correction | Automated eval suite (correction accuracy dimension); learner feedback flag ("This correction seems wrong") | Correction accuracy <95% on eval suite; or >3% of sessions with learner-flagged incorrect corrections [~] | Review flagged corrections; retrain/adjust prompts; if systemic, increase human audit rate to 25% | Correction is shown with a "not sure about this" visual indicator; post-session review marks it as unverified |
| **Inappropriate or offensive content** — avatar generates content that is culturally insensitive, offensive, or unrelated to language learning | Content safety classifier on every avatar utterance (pre-delivery filter) | Zero tolerance: any flagged utterance is blocked before delivery | Utterance replaced with a safe fallback ("Let me rephrase that..."); session flagged; incident reviewed within 24 hours | Avatar delivers a neutral topic-redirect utterance from a pre-approved bank |
| **ASR misrecognition leading to wrong feedback** — ASR misinterprets learner speech, causing avatar to correct something the learner said correctly | ASR confidence score on `avatar.utterance.learner`; learner feedback flag ("I didn't say that") | ASR confidence <0.6 on an utterance that triggers a correction | Avatar asks learner to repeat ("Could you say that again?") instead of correcting; correction deferred until confident transcription available | Transcript shows "[uncertain]" marker; correction suppressed for low-confidence utterances |
| **Session loop / topic amnesia** — avatar repeats itself, loses conversation context, or asks the same question twice | Automated: duplicate-utterance detection within session; conversation-state tracking | >1 exact or near-duplicate avatar utterance per session | Session orchestrator injects context reminder into LLM prompt; if loop persists (>3 duplicates), graceful session end with apology | "I think we've covered that — let's move on to [next topic]" |
| **CEFR level drift** — avatar output exceeds learner's CEFR level | Automated: vocabulary/grammar complexity check against CEFR level band per utterance | >5% of avatar utterances above learner's level + 1 band | Alert + prompt adjustment; if systemic, block deployment | Avatar self-corrects: rephrases with simpler vocabulary |

### Eval infrastructure dependency

The automated eval suite must be operational before Phase 2 beta entry. This depends on:
- Ground-truth benchmark: >=10 annotated real teacher-learner recordings scored against the Berlitz Teaching Rubric (architecture doc section 5). Owner: PM + Data. Deadline: Aug 1 2026.
- Scenario corpus: >=30 synthetic-learner test scenarios with annotated expected behaviors. Owner: PM + Content. Deadline: Jul 15 2026.
- LLM judge prompt: calibrated against human auditor scores with kappa >=0.6. Owner: Engineering. Deadline: Aug 15 2026.

---

## 9. Launch Plan

### Phase 1: Internal Dogfood (Aug 2026)

**Entry criteria:**
- Avatar renders in browser with lip-sync and expressions
- At least 5 guided conversation scenarios and 3 role-play scenarios available (English)
- Berlitz Method system prompts pass internal pedagogical review
- Voice-to-first-audio latency consistently <1s (relaxed target for dogfood)
- Grammar correction and live feedback functional (accuracy > quality at this stage)

**Activities:**
- Product, engineering, and select Berlitz instructors use avatar mode daily
- Instructors evaluate Berlitz Method compliance against the teaching rubric
- Collect qualitative feedback on avatar style, voice quality, conversation naturalness
- Measure latency, cost per minute, and session stability
- Identify critical bugs and UX issues

**Exit criteria:**
- No P0 bugs blocking core conversation flow
- Berlitz Method compliance score >=80% (internal QA rubric)
- Latency p95 <700ms (on path to 500ms)
- At least 50 internal sessions completed with feedback collected
- Cost per avatar minute within 2x of tier targets (on path to NFR-05/06)

### Phase 2: Beta with Select Learners (Sep 2026 — web launch)

**Entry criteria:**
- Phase 1 exit criteria met
- Avatar latency p95 <500ms
- At least 10 guided conversation and 5 role-play scenarios
- Post-session review functional
- Cost per avatar minute within tier targets
- Feature-flagged rollout infrastructure in place

**Activities:**
- Roll out to 100-500 [~] selected beta learners (mix of Free, Plus, Pro tiers)
- A/B: avatar mode available vs not (for conversion lift measurement)
- Measure primary metric (speaking time per session) and all engagement metrics
- Collect NPS and qualitative feedback on avatar experience
- Monitor cost per minute, error rates, and latency at real-world scale
- Iterate on feedback quality, scenario variety, and avatar behavior

**Exit criteria:**
- Speaking time per session trending toward target (>=6 min in 15-min session [~] — 75% of GA target)
- Session return rate >=30% [~]
- No P0 or unresolved P1 bugs
- Cost per avatar minute within tier targets
- Latency p95 <500ms sustained under beta load
- Berlitz Method compliance >=85%

### Phase 3: GA with Mobile (Oct 2026)

**Entry criteria:**
- Phase 2 exit criteria met
- iOS and Android apps pass app store review with avatar mode
- Berlitz Method compliance >=90%
- All 7 MVP features (C1, C2, C4, C5, C7, C8, C9) functional and stable
- Scenario library has >=15 guided conversations and >=8 role-plays across A1-B2

**Activities:**
- Full rollout to all tiers and markets
- Continue A/B on conversion lift
- Begin CEFR progression tracking (baseline cohort)
- Expand scenario library based on beta learner feedback
- Monitor all success metrics and guardrails

**Rollback plan:**
- Feature flag allows disabling avatar mode per-user, per-tier, or globally
- Fallback: audio-only conversation mode (text-based transcript + voice, no visual avatar) — uses same AI engine without avatar render
- Rollback trigger: p95 latency >1s sustained for >1 hour, cost per minute >2x target, or Berlitz Method compliance <80%

---

## 10. Open Questions

| # | Question | Owner | Status | Source |
|---|----------|-------|--------|--------|
| 1 | **Avatar style:** Stylized vs semi-realistic vs photoreal? Evidence strongly favors stylized to avoid uncanny valley (Mori; Mathur & Reichling 2016), but brand and user preference testing needed. | Design + Engineering | Open | spec research 3.3 |
| 2 | **Speech architecture:** S2S (lowest latency, no pronunciation scores) vs pipeline (higher latency, full scoring) vs hybrid? Requirement is both natural feel AND pronunciation feedback — architecture is engineering's call. | Engineering | Open | spec research 4.4 |
| 3 | **ASR for non-native accents:** Which ASR best handles learners' actual accents? Deepgram Nova-3 vs gpt-4o-transcribe. Needs A/B on real learner audio, not vendor benchmarks. | Engineering | Open | spec research 4.3 |
| 4 | **Avatar at MVP confirmed?** Architecture doc flags: "Both audio-only and avatar modes ship at MVP. This depends on avatar technology feasibility — revisit after avatar tech evaluation." What's the fallback if avatar slips? | PM + Engineering | Open — must resolve before engineering starts | architecture doc section 6 |
| 5 | **Latency budget allocation:** What end-to-end latency can the chosen stack actually hit? How is the <500ms budget allocated across ASR, LLM, TTS, and avatar render? | Engineering | Open | spec research 4.1 |
| 6 | **Microlearning integration:** Do MVP microlearning tap-lessons ship, and how does existing course content flow into AI avatar practice? | PM | Open | Chayan Roy, Teams, Jun 3 2026 |
| 7 | **Efficacy measurement plan:** Ground-truth benchmark + pre/post CEFR assessment that lets Berlitz claim outcomes credibly. How many teacher-learner recordings exist? Consent/privacy for benchmarking? | PM + Data | Open | architecture doc section 5; spec research 6 |
| 8 | **Berlitz Method encoding validation:** Who is the designated Berlitz Method expert to validate AI system prompts? | PM | Open | architecture doc section 8 |
| 9 | **Avatar render technology:** Web-based (Three.js) vs native (Unity/Unreal)? Impacts mobile performance, dev cost, and time to market. | Engineering | Open — must resolve before engineering starts | architecture doc section 8 |
| 10 | **TTS voice selection:** Which TTS delivers the most natural target-language voice? ElevenLabs Flash vs Cartesia Sonic vs Azure Neural TTS. Needs eval benchmark. | Engineering | Open | spec research 4.3 |

---

## Sources

### Internal
- Spec research: `product-context/ai-avatar-tutor-spec-research.md`
- Architecture: `engineering/design/plans/ai-tutor-architecture.md`
- Feature matrix: `PRDs/feature-matrix.md`
- Strategic positioning: `competitive-research/strategic-positioning.md`
- JTBD and personas: `strategy/business-context/berlitz-jtbd-and-users.md`
- Roadmap: `strategy/roadmaps/berlitz-2026-2027-roadmap.md`
- Business info: `strategy/business-context/berlitz-business-info.md`
- Teams: Jan Hoffmann on avatar cost (May 18 2026); Chayan Roy on MVP scope (Jun 3 2026)

### Learning science
- VanLehn 2011 — ITS effectiveness (d ~= 0.76)
- Krashen 1982/1985 — Affective filter, comprehensible input
- Swain & Lapkin 1995 — Output hypothesis
- Lyster & Ranta 1997 — Corrective feedback (prompts > recasts)
- Li 2010 — Corrective feedback meta-analysis (d ~= 0.61)
- Hu & Nation 2000 — 95-98% vocabulary comprehension threshold
- Cepeda et al. 2006 — Spacing effect
- Stivers et al. 2009 — Turn-taking gaps (~200-500ms)

### Avatar and multimedia
- Schroeder, Adesope & Gilbert 2013 — Pedagogical agent meta-analysis (g ~= 0.19)
- Mayer 2014 — Voice principle (d ~= 0.74), personalization (d ~= 1.1), image principle (~null)
- Mori 1970/2012 — Uncanny valley
- Mathur & Reichling 2016 — Uncanny valley empirical confirmation

### Market
- Speak Series C ($1B valuation, Dec 2024)
- Praktika Series A ($35.5M, May 2024)
- Kulik & Fletcher 2016 — Field-RCT ITS effects (g ~= 0.3-0.5)
