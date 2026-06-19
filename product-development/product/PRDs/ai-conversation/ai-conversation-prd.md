# AI Conversation Experience - PRD

| Field | Value |
|-------|-------|
| **Author** | Jan Hoffmann, PM |
| **Status** | Draft |
| **Last Updated** | 2026-06-18 |
| **Related RFC** | TBD |
| **Related Plan** | `engineering/design/plans/ai-tutor-architecture.md` (Layer B - AI Engine owns the runtime contract) |
| **Related Research** | `product-context/ai-avatar-tutor-spec-research.md`, `product/PRDs/feature-matrix.md`, `competitive-research/strategic-positioning.md` |
| **Dependencies** | Upstream: `curriculum-factory/curriculum-factory-prd.md` (content pipeline). Delivery modes: `ai-avatar/ai-avatar-prd.md` (avatar visual layer). Sibling: `practice-drills/practice-drills-prd.md` (drills, separate experience) |

---

## Overview

The AI Conversation Experience is the guided-conversation and role-play product in the Berlitz Learner App - the learner talks, and an AI that behaves like a trained Berlitz instructor steers the conversation, delivers corrections, enforces the Berlitz Method, adapts to CEFR level, and gives real-time feedback. It is delivered in two **modes**: audio-only (voice + transcript) and avatar (animated visual character). Both modes are the same conversation product; they differ only in presentation.

- Consumes structured scenarios from the Curriculum Factory
- Owns the conversation product end-to-end: user stories, success metrics, eval, and Berlitz Method compliance, across both delivery modes
- The **avatar visual layer** is specified as a delta in `ai-avatar/ai-avatar-prd.md`; **practice drills** (pronunciation, vocabulary, grammar) are a separate experience in `practice-drills/practice-drills-prd.md`
- The runtime engineering contract (mode-agnostic session API, swappable ASR/TTS/LLM/pronunciation components) is owned by Engineering - see architecture doc Layer B
- If the avatar slips from MVP, the conversation product still ships in audio-only mode

---

## 1. Problem Statement

1. **Current third-party dependency is costly, limiting, and a data dead-end.**
   - Berlitz spends ~26k EUR [~] on Talkio for conversation practice (Jan Hoffmann, Teams, May 18 2026)
   - Talkio cannot enforce the Berlitz Method, follow Berlitz curriculum, or integrate with the learner profile
   - No access to session-level data - learner utterances, error patterns, speaking time, and engagement signals stay locked in a third-party system
   - This blocks the feedback loop needed for an in-house AI tutor and makes it impossible to measure learning outcomes
   - Building in-house unlocks: curriculum integration, method compliance, data ownership, lower unit costs (spec research 1.4)

2. **An AI conversation partner is the right shape for speaking practice.**
   - Speaking is the most anxiety-inducing language activity (MacIntyre & Gardner; Young 1990; Krashen's affective filter - spec research 2.2)
   - But producing language is what drives acquisition: Swain's output hypothesis shows speaking forces syntactic processing via noticing gaps and hypothesis-testing - input alone is insufficient (spec research 2.2)
   - Classroom cannot solve both: pushing speaking raises anxiety, and group class time limits individual speaking to single-digit minutes per hour
   - An AI instructor resolves this tension - high-volume, low-stakes speaking reps in a private setting, with immediate salient feedback (spec research 2.2, line 99)

---

## 2. Business Opportunity

### Strategic positioning

Berlitz targets the **unoccupied top-right quadrant** (High AI + High Human) in the competitive landscape. AI conversation practice is the core capability that anchors this position - it is what makes AI practice feel like a real Berlitz lesson, not a generic chatbot. (strategic-positioning.md)

### Competitive threat

- **Speak** ($1B valuation, $162M raised; OpenAI-backed) is 5/5 on voice conversation. They set the quality bar for AI speaking practice. (spec research 5.1)
- **Praktika** ($35.5M Series A) delivers avatar conversations with tone-of-voice and emotion. (spec research 5.1)
- Neither competitor has a proprietary teaching methodology. Berlitz's 140-year pedagogical IP encoded as system prompts is the defensible moat. (architecture doc, Layer A)

### Revenue model

AI conversation is a shared cost component across all tiers. Its per-session cost is the non-avatar portion of AI Tutor sessions (the avatar render is the only cost unique to the avatar mode - see `ai-avatar-prd.md`).

**Per-session AI conversation costs (v0.2.8, excluding avatar render):**
- LLM (Claude Sonnet): 0.055€/session (10k tokens)
- ASR (Deepgram Nova): 0.017€/session (4.5 min user speech)
- TTS (Azure Neural): 0.028€/session (4.5 min AI speech)
- Pronunciation (Azure): 0.021€/session (4.5 min user speech)
- **Total AI conversation cost: ~0.121€/session** (~$0.13)

This is the marginal cost of the conversation itself - cheap. The expensive parts are the avatar render (separate PRD) and the human teacher session (8.60€).

(cost model v0.2.8)

---

## 3. Why Now

1. **Sep 2026 web launch requires working AI conversation.** Both audio-only and avatar modes are deliveries of this one conversation product. It is on the critical path. (roadmap)

2. **Talkio replacement is urgent.** ~26k€ [~] annual spend on a tool that cannot enforce Berlitz Method or feed data back. (spec research 1.4)

3. **LLM capabilities now support the requirement.** Frontier-class models (e.g., Claude Sonnet, GPT-4o) offer the context window (>=32k), multilingual fluency, instruction following, and structured output needed for a pedagogically compliant tutor. This was not reliably achievable 18 months ago.

4. **Conversation is the foundation for all AI experiences.** Audio-only, avatar, and future modes (open conversation, crosstalk) are all deliveries of this one product. Building it right and mode-agnostic is the highest-leverage investment.

---

## 4. Customer Requests

- [ ] HeyGen usage data shows audio-only is 10x avatar usage. Suggests AI instructor quality (steering, feedback, corrections) matters more than visual layer. Root cause unconfirmed - see AI Avatar PRD OQ-4
- No direct learner quotes requesting AI conversation practice exist yet. Demand is inferred from Talkio spend (26k EUR/yr [~]), HeyGen usage patterns, and competitive benchmarking (Speak, Praktika)
- **Validation plan:** Collect >=5 qualitative feedback interviews during Phase 1 dogfood. Owner: PM

---

## 5. Goals & Success Metrics

### Baseline collection plan

No AI instructor baselines exist today. Baselines will be set in two passes:

1. **Pre-build (by Jul 15 2026) - owner: PM + Analytics.** Extract from Talkio usage data: average session duration, learner speaking time per session (if available), session return rate, and session completion rate.
2. **Phase 2 beta (Sep 2026) - owner: Analytics.** First two weeks of beta are the baseline collection period. All GA targets are provisional until confirmed.

### Primary metric

**Speaking time per session** - minutes of active learner speech per session (any mode). Proves the product drives output practice (Swain's output hypothesis).

- **Baseline:** ~3-4 min learner speaking in a 15-min Talkio session [~]
- **Target:** >=8 min of learner speaking in a 15-min session [~]
- **Timeframe:** Measured from GA (Oct 2026)

### Engagement metrics

| Metric | Definition | Baseline | Target | Timeframe |
|--------|-----------|----------|--------|-----------|
| Session return rate | % of users who start a 2nd AI session within 7 days of their 1st | ~25% [~] | >=40% [~] | GA + 30 days |
| Session completion rate | % of sessions where the learner reaches the scenario goal or natural ending | ~50% [~] | >=65% [~] | GA + 30 days |
| Weekly AI sessions | Average AI sessions per active user per week | ~1.2 [~] | >=2 [~] | GA + 90 days |

### Efficacy metrics (longer-term)

| Metric | Definition | Baseline | Target | Timeframe |
|--------|-----------|----------|--------|-----------|
| CEFR progression rate | Rate of CEFR sub-level advancement for AI session users vs non-users | Set from GA cohort | >=1.3x the rate of non-users [~] | GA + 6 months |

Grounded in VanLehn's ITS ceiling of d ~= 0.76 and field-RCT realistic range of g ~= 0.3-0.5. (spec research 2.1)

### Guardrails

| Guardrail | Threshold | Action | Rationale |
|-----------|-----------|--------|-----------|
| Voice-to-first-audio latency p95 | <500ms | Alert; if >1s sustained >1h, rollback | Stivers et al. (2009): turn-taking gaps ~200ms; >500ms feels unnatural. (spec research 4.1) |
| Berlitz Method compliance score | >=90% (internal QA rubric) | Block prompt/model change if <85% | Sessions must follow immersive L2, Q&A cycles, gentle correction. (architecture doc, section 5) |
| Conversation-practice WAU | Must not drop below 90% of Talkio baseline during rollout | Alert PM + Engineering; investigate within 48h | Replacing Talkio must not regress overall conversation adoption. Baseline: Talkio WAU as of Jul 15 2026 [~] |

### Instrumentation

Event names use `snake_case`; all events carry `session_id`, `user_id`, `tier`, `cefr_level`, `mode` (audio_only / avatar), and `timestamp`.

| Event | Payload (key fields) | Metrics it feeds |
|-------|---------------------|-----------------|
| `ai.session.started` | `scenario_id`, `scenario_type` (guided / role_play), `mode` | Session completion rate, weekly sessions |
| `ai.session.ended` | `end_reason` (goal_reached / time_up / learner_exit / error), `duration_ms` | Session completion rate, return rate |
| `ai.utterance.learner` | `duration_ms`, `transcript`, `asr_confidence` | Speaking time per session |
| `ai.utterance.tutor` | `duration_ms`, `latency_ms` (voice-to-first-audio) | Latency guardrail |
| `ai.correction.delivered` | `correction_type` (grammar / pronunciation / vocabulary), `strategy` (prompt / recast / hint), `learner_response` (self_repair / ignored / n/a) | Berlitz Method compliance |
| `ai.feedback.surfaced` | `feedback_type` (pronunciation_flag / vocab_suggestion / fluency_cue), `severity` | Diagnostic only (no target metric) |
| `ai.scenario.goal_reached` | `scenario_id`, `turns_taken`, `time_to_goal_ms` | Session completion rate |
| `ai.eval.compliance` | `session_id`, `compliance_score`, `violations[]` | Berlitz Method compliance guardrail |

**Derived metrics:**
- **Speaking time per session** = SUM(`ai.utterance.learner.duration_ms`) per `session_id`
- **Session return rate** = COUNT(users with >=2 `ai.session.started` within 7 days) / COUNT(users with >=1)
- **Session completion rate** = COUNT(`ai.session.ended` WHERE `end_reason` IN (goal_reached, time_up)) / COUNT(`ai.session.started`)
- **Latency p95** = PERCENTILE(95, `ai.utterance.tutor.latency_ms`)

**Dependency:** Analytics engineering must confirm the event pipeline before Phase 2 beta entry. Owner: Analytics + Engineering.

### Non-goals

- **Visual avatar rendering** - delta PRD (`ai-avatar-prd.md`): character, lip-sync, expressions, appearance/dialect, render cost. This PRD owns the conversation; the avatar PRD owns only the visual layer.
- **Practice drills** - separate experience (`practice-drills-prd.md`): pronunciation, vocabulary, and grammar drills, wordbook, phoneme visualisation, SRS. Drills are not conversation.
- **Content/curriculum generation** - separate PRD (`curriculum-factory-prd.md`). This product consumes scenarios, it does not create them.
- **Runtime engineering contract** - the mode-agnostic session API and component-swap design are owned by Engineering (architecture Layer B), not this PRD. This PRD states the requirement (FR-07, NFR-04); the contract itself is an engineering artifact.
- **C3: Open Conversation** - post-MVP.
- **C10: Crosstalk Mode (L1<->L2)** - post-MVP.
- **Human Teaching Integration (Section F)** - all post-MVP.

---

## 6. User Stories

### Professional Pedro (Pro, $49/mo)

**US-1: Guided conversation for work scenarios**
As Professional Pedro, I want to practice a structured business conversation with the AI instructor (e.g., presenting project updates to a client), so that I build speaking confidence for real work situations.

*Acceptance criteria:*
- AI presents a scenario with clear objectives and vocabulary focus
- Conversation follows Berlitz curriculum structure for Pedro's CEFR level
- Pedro speaks for the majority of the session, aligned to the primary metric (>=8 min of a 15-min session, ~53%)
- Corrections use salient prompts >=80% of the time (eval rubric, Section 8)
- Post-session summary shows grammar/vocabulary/pronunciation performance

**US-2: Role-play for meeting preparation**
As Professional Pedro, I want to role-play a specific work scenario (job interview, client negotiation, team standup) with the AI playing the other role, so that I rehearse real conversations I'll have this week.

*Acceptance criteria:*
- Pedro selects from pre-defined role-play scenarios relevant to business contexts
- AI plays the assigned role with appropriate register, vocabulary, and pacing (CEFR bounding >=95%, Section 8)
- AI adapts to Pedro's responses - follows scenario intent but responds to actual learner utterances (Q&A cycle adherence >=70%, Section 8)
- Corrections are salient and elicit self-repair (>=80% prompt strategy, Section 8)

**US-3: Efficient practice between meetings**
As Professional Pedro, I want to start a session quickly (under 5 seconds from app open to speaking), so that I can practice during a 15-minute break.

*Acceptance criteria:*
- Session start takes <5 seconds
- "Quick start" recommends a scenario based on curriculum position
- Session can end at any point without penalty (no negative impact on CEFR level, streak, or progress; partial data saved)

### Hobbyist Hana (Plus, $19/mo)

**US-4: Low-pressure conversation practice**
As Hobbyist Hana, I want to have a casual conversation about everyday topics, so that I practice speaking without feeling judged.

*Acceptance criteria:*
- AI tone is conversational and uses first/second-person language (Mayer personalization principle, d ~= 1.1)
- Corrections use salient prompts >=80% of the time; no correction interrupts mid-utterance
- Language is constrained to Hana's CEFR level (>=95% of vocabulary within level band)
- AI provides explicit positive reinforcement at least once per 5 turns [~] (general conversation behaviour per FR-04 encouragement patterns; stated here as Hana cares most)

### Career Carla (Career, $39/mo)

**US-5: Business role-play for career advancement**
As Career Carla, I want to role-play a job interview in my target industry, so that I can practice articulating my experience and skills in the target language.

*Acceptance criteria:*
- Role-play scenarios include business-specific contexts (interviews, presentations, negotiations)
- AI asks follow-up questions that push Carla to elaborate (Swain output hypothesis)
- Post-session feedback highlights business-relevant vocabulary and formal register usage

### Executive Elena (Premium, $99/mo)

**US-6: Premium conversation experience**
As Executive Elena, I want the conversation to feel polished and professional - natural voice, responsive timing, no awkward pauses.

*Acceptance criteria:*
- Voice-to-first-audio latency p95 <500ms
- High-quality TTS with natural prosody
- Conversation maintains context across the full session (no repetition or topic amnesia)

---

## 7. Requirements

### Functional Requirements

| ID    | Requirement                                                                                                                                                                                                                               | Priority | Source                                                    |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | --------------------------------------------------------- |
| FR-01 | System shall deliver scenario-based dialogue following Berlitz curriculum: each session has defined learning objectives, vocabulary bounds, grammar focus, and success criteria loaded from the Scenario Library.                         | P0       | Feature matrix C2; architecture A3, B1                    |
| FR-02 | System shall support pre-defined role-play scenarios where the AI plays one character and the learner plays the other.                                                                                                                    | P0       | Feature matrix C4; architecture A3                        |
| FR-03 | System shall correct grammar errors inline during conversation using salient, self-repair-eliciting prompts (e.g., "Can you try saying that differently?") rather than implicit recasts, consistent with the Berlitz Method.              | P0       | Feature matrix C5; Lyster & Ranta 1997; spec research 2.3 |
| FR-04 | System prompts shall enforce Berlitz Method compliance: immersive L2 use (minimize L1), question-answer cycles, graduated difficulty, gentle error correction, and encouragement patterns.                                                | P0       | Feature matrix C7; architecture A4                        |
| FR-05 | AI output shall be constrained to the learner's CEFR level: vocabulary, grammar structures, sentence complexity, and speaking speed bounded by curriculum position (~95-98% known vocabulary).                                            | P0       | Feature matrix C8; Hu & Nation 2000; architecture A5      |
| FR-06 | System shall provide real-time, multi-dimensional feedback: pronunciation flags, vocabulary suggestions, and fluency cues surfaced alongside grammar correction - salient, without breaking flow.                                         | P0       | Feature matrix C9; spec research 2.3                      |
| FR-07 | System shall expose a mode-agnostic session API so that both Audio-Only and Avatar presentation layers can connect without duplicating conversation logic.                                                                                | P0       | Architecture doc, Layers B+C                              |
| FR-08 | System shall provide visual cues and prompts when the learner is stuck: sentence starters, vocabulary hints, or rephrased questions. Silence threshold varies by CEFR level (A1-A2: 8-10s [~], B1-B2: 5s [~]) - validated during dogfood. | P1       | Architecture B7                                           |
| FR-09 | Post-session review shall include: full transcript, grammar notes, new vocabulary list, pronunciation scores, session summary, and scenario goal completion status.                                                                       | P1       | Architecture Layer C shared UI                            |
| FR-10 | System shall support "quick start" - begin a recommended scenario within 5 seconds, based on curriculum position and learner profile.                                                                                                     | P2       | US-3                                                      |
@JH: review requirements; add: ensure that guided conversations do not go off track. gently keep the user on target. be able to specify the level of flex that is allowed

### Non-Functional Requirements

| ID | Requirement | Target | Rationale |
|----|------------|--------|-----------|
| NFR-01 | **Latency:** Voice-to-first-audio response time | p95 <500ms | Stivers et al. (2009). Architecture (S2S vs pipeline vs hybrid) is engineering's call. (spec research 4.1) |
| NFR-02 | **Speech:** Must support both natural conversation feel AND pronunciation-level feedback simultaneously | Natural conversation + phoneme/word-level scoring per utterance | S2S gives best feel but no phoneme scores; pipeline gives scores but adds latency. Engineering decides architecture. (spec research 4.4) |
| NFR-03 | **CEFR bounding:** AI output constrained to learner's level | ~95-98% known vocabulary in AI utterances | Hu & Nation (2000). (spec research 2.5) |
| NFR-04 | **Component modularity:** ASR, TTS, LLM, pronunciation scoring each independently swappable | Swap without session architecture changes | Vendor lock-in is a strategic risk. (cost model v0.2.8 shows 4 different vendors in the stack) |
| NFR-05 | **Concurrent sessions** | >=100 concurrent [~] | Launch-week estimate; scale with demand. |
| NFR-06 | **Accessibility** | WCAG 2.1 AA: full transcript as text alternative; keyboard navigation; screen reader compatibility | Feature matrix J6. |

### Privacy & Data Constraints

The product records, transcribes, and scores learner speech. Berlitz operates in the EU (€ pricing, Germany launch market).

| Constraint | Requirement | Owner |
|-----------|------------|-------|
| **Consent for voice recording** | Learner must explicitly consent before their first AI session. Consent revocable at any time. | Legal + Product |
| **Data retention** | Audio recordings retained max 90 days [~], then auto-deleted. Transcripts retained for learner profile lifetime. Learner can request deletion (GDPR Art. 17). | Legal + Engineering |
| **Human audit access controls** | 10% human audit sample anonymized/pseudonymized. Auditors access transcripts, not raw audio unless needed for pronunciation eval (logged, time-limited). | Legal + Data |
| **GDPR DPIA** | Required before Phase 2 beta - voice biometric data is special category (GDPR Art. 9). | Legal |
| **Data residency** | EU user data processed and stored within the EU. | Engineering + Legal |
| **Launch gate** | Privacy review and DPIA approval are Phase 2 beta entry gates. | Legal |

---

## 8. AI Evaluation Plan

The conversation core loop is LLM-driven - the same input produces different outputs. This section defines eval methodology, model requirements, and failure-mode guardrails.

### Evaluation methodology

**Automated eval suite (run on every model or prompt change):**

1. **Scenario corpus:** >=30 scripted synthetic-learner sessions [~] spanning A1-B2, covering guided conversation and role-play, with annotated expected teaching behaviors.
2. **LLM-as-judge scoring** against the Berlitz Teaching Rubric (derived from real teacher-learner recordings - architecture doc section 5). Five dimensions:
  - **L2 immersion:** % of AI utterances in target language (target: >=98%)
  - **Correction accuracy:** % of grammar corrections linguistically correct (target: >=95%)
  - **Correction strategy:** % using salient prompts vs implicit recasts (target: >=80% prompts)
  - **CEFR bounding:** % of AI vocabulary within learner's level band (target: >=95%)
  - **Q&A cycle adherence:** % of turns following question-answer-feedback pattern (target: >=70%)
3. **Human audit sample:** 10% of beta sessions [~] reviewed by a Berlitz Method expert. Inter-rater reliability tracked; if kappa <0.6, recalibrate the judge.

**Composite Berlitz Method compliance score** = weighted average of the five dimensions. Weights TBD with Berlitz Method expert.

### Eval thresholds

| Level | Compliance score | When |
|-------|-----------------|------|
| **Launch gate** | >=85% | Phase 2 beta entry |
| **Target** | >=90% | GA (Oct 2026) |
| **Aspirational** | >=95% | GA + 6 months |

If compliance drops below 85% on any eval run, the prompt/model change is blocked.

### Model capability requirements

| Capability | Requirement | Rationale |
|-----------|------------|-----------|
| Context window | >=32k tokens | Full-session memory (~8k-12k dialogue) + scenario + system prompts + learner profile |
| Multilingual fluency | Native-quality output at CEFR C2 | AI must model correct target-language usage |
| Instruction following | Reliable adherence under adversarial input | Berlitz Method compliance depends on following system prompts when learner goes off-script or speaks L1 |
| Structured output | JSON or function-calling | Correction events, feedback metadata, scenario state must be extractable programmatically |
| Latency (TTFT) | <300ms [~] | Leaves ~200ms for ASR + TTS (+ avatar render if applicable) |

### AI failure modes and guardrails

| Failure mode | Detection | Threshold | Action | Fallback |
|-------------|-----------|-----------|--------|----------|
| **L1 leakage** | Language detection on every AI utterance | >2% L1 per session | Alert + flag; if >5% of sessions, block deployment | Redirect in target language |
| **Incorrect grammar correction** | Eval suite + learner flag ("This seems wrong") | Accuracy <95% or >3% sessions flagged [~] | Review; if systemic, increase audit to 25% | "Not sure about this" indicator |
| **Inappropriate content** | Content safety classifier (pre-delivery) | Zero tolerance | Block utterance; replace with safe fallback; incident review within 24h | Neutral topic-redirect from pre-approved bank |
| **ASR misrecognition** | ASR confidence score + learner flag | Confidence <0.6 triggering a correction | Ask learner to repeat instead of correcting | "[uncertain]" marker; suppress correction |
| **Session loop / amnesia** | Duplicate-utterance detection | >1 near-duplicate per session | Inject context reminder; if >3 duplicates, graceful end | "Let's move on to [next topic]" |
| **CEFR level drift** | Vocabulary/grammar complexity check | >5% above learner's level + 1 band | Alert + prompt adjust; if systemic, block deployment | Rephrase with simpler vocabulary |

### Eval infrastructure dependency

Must be operational before Phase 2 beta:
- Ground-truth benchmark: >=10 annotated real teacher-learner recordings. Owner: PM + Data. Deadline: Aug 1 2026.
- Scenario corpus: >=30 test scenarios. Owner: PM + Content. Deadline: Jul 15 2026.
- LLM judge: calibrated with kappa >=0.6. Owner: Engineering. Deadline: Aug 15 2026.

---

## 9. Launch Plan

### Phase 1: Internal Dogfood (Aug 2026)

**Entry criteria:**
- Talkio baselines confirmed (session duration, speaking time, return rate, completion rate) - owner: PM + Analytics, deadline Jul 15 2026
- At least 5 guided conversation scenarios and 3 role-play scenarios (English)
- Berlitz Method system prompts pass internal pedagogical review
- Voice-to-first-audio latency consistently <1s (relaxed for dogfood)
- Grammar correction and live feedback functional

**Exit criteria:**
- No P0 bugs blocking conversation flow
- Berlitz Method compliance >=80%
- Latency p95 <700ms
- >=50 internal sessions completed

### Phase 2: Beta (Sep 2026 - web launch)

**Entry criteria:**
- Phase 1 exit criteria met
- Latency p95 <500ms
- >=10 guided conversation and 5 role-play scenarios
- Post-session review functional
- Eval suite operational (see Section 8)
- Privacy/DPIA approved

**Exit criteria:**
- Speaking time per session >=6 min in 15-min session [~] (75% of GA target)
- Session return rate >=30% [~]
- No P0 or unresolved P1 bugs
- Latency p95 <500ms sustained
- Berlitz Method compliance >=85%

### Phase 3: GA (Oct 2026)

**Entry criteria:**
- Phase 2 exit criteria met
- Berlitz Method compliance >=90%
- >=15 guided conversations and >=8 role-plays across A1-B2

**Rollback plan:**
- Feature flag disables AI conversation per-user, per-tier, or globally
- Rollback trigger: latency >1s sustained >1 hour, or compliance <80%

---

## 10. Decisions Requiring PDRs

| Decision | Current position | Why it needs a PDR | When |
|----------|-----------------|-------------------|------|
| **Build vs buy (Talkio replacement)** | Building the conversation product in-house | Commits ~26k€/yr Talkio savings against engineering investment; hard to reverse once the engine and data pipeline are built. This PRD owns the decision (the avatar PRD references it). | Before engineering starts (Jul 1 2026) |
| **Mode-agnostic session API contract** | Open - Engineering to propose (see OQ-8) | The API constrains both the avatar and audio delivery layers; switching it post-build is expensive and cross-team. | Before Phase 1 dogfood (Aug 2026) |

---

## 11. Open Questions

| # | Question | Owner | Status | Source |
|---|----------|-------|--------|--------|
| 1 | **Speech architecture:** S2S vs pipeline vs hybrid? Must deliver both natural feel AND pronunciation feedback. | Engineering | Open | spec research 4.4 |
| 2 | **ASR for non-native accents:** Deepgram Nova-3 vs gpt-4o-transcribe. Needs A/B on real learner audio. | Engineering | Open | spec research 4.3 |
| 3 | **Latency budget allocation:** How is <500ms split across ASR, LLM, TTS, and (optionally) avatar render? | Engineering | Open | spec research 4.1 |
| 4 | **Microlearning integration:** Do MVP microlearning tap-lessons ship, and how does content flow into AI practice? | PM | Open | Chayan Roy, Teams, Jun 3 2026 |
| 5 | **Efficacy measurement plan:** Ground-truth benchmark + pre/post CEFR assessment. How many recordings exist? Consent? **Blocks Phase 2 eval** (compliance rubric is derived from these recordings). | PM + Data | Open - by Jul 1 2026 | architecture doc section 5 |
| 6 | **Berlitz Method encoding validation:** Who is the designated Berlitz Method expert? | PM | Open - by Jul 1 2026 | architecture doc section 8 |
| 7 | **TTS voice selection:** ElevenLabs Flash vs Cartesia Sonic vs Azure Neural TTS. Needs eval benchmark. | Engineering | Open | spec research 4.3 |
| 8 | **Session API contract:** Mode-agnostic API (FR-07) constrains both avatar and audio-only layers. Engineering to propose contract and review with both PRD owners. | Engineering | Open - by Jul 15 2026 | architecture doc, Layers B+C |

---

## Sources

### Internal
- Spec research: `product-context/ai-avatar-tutor-spec-research.md`
- Architecture: `engineering/design/plans/ai-tutor-architecture.md`
- Feature matrix: `product/PRDs/feature-matrix.md`
- Cost model: `strategy/business-context/berlitz_cost_model_v0.2.8.xlsx`
- JTBD and personas: `strategy/business-context/berlitz-jtbd-and-users.md`

### Learning science
- VanLehn 2011 - ITS effectiveness (d ~= 0.76)
- Krashen 1982/1985 - Affective filter, comprehensible input
- Swain & Lapkin 1995 - Output hypothesis
- Lyster & Ranta 1997 - Corrective feedback (prompts > recasts)
- Li 2010 - Corrective feedback meta-analysis (d ~= 0.61)
- Hu & Nation 2000 - 95-98% vocabulary comprehension threshold
- Stivers et al. 2009 - Turn-taking gaps (~200-500ms)
