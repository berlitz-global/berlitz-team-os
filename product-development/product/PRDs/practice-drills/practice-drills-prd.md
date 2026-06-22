# Practice Drills - PRD

| Field | Value |
|-------|-------|
| **Author** | Jan Hoffmann, PM |
| **Status** | Draft |
| **Last Updated** | 2026-06-21 |
| **Related Plan** | `engineering/design/plans/ai-tutor-architecture.md` (Layer C - Presentation, Audio-Only Mode) |
| **Dependencies** | Upstream: `curriculum-factory/curriculum-factory-prd.md` (content). Sibling: `ai-conversation/ai-conversation-prd.md` (conversation is a separate experience) |

---

## Overview

Practice Drills are the short, focused, voice-driven practice activities in the Berlitz Learner App: pronunciation, vocabulary, and grammar drills with a lightweight voice UI and phoneme-level feedback. They are distinct from AI conversation - drills are listen/repeat/score/retry reps, not multi-turn dialogue.

- Default practice mode for the free tier, at near-zero marginal cost (no avatar render, no full conversation LLM loop)
- Covers pronunciation, vocabulary, and grammar drills plus the Wordbook  
- Conversation (guided + role-play, in either audio or avatar mode) is a separate experience - see `ai-conversation/ai-conversation-prd.md`
- Content (words, phrases, exercises) comes from the Curriculum Factory

---

## 1. Problem Statement

1. **Not every practice session is a conversation.**
   - Short audio driven drills (1-5 min) targeting pronunciation, vocabulary, or grammar are better served by a focused voice UI than a full conversation flow
   - Interaction pattern is listen, repeat, get feedback, try again - a multi-turn AI dialogue adds cost and load time without value for this use case
1. **The free tier needs unlimited practice at near-zero marginal cost.**
   - Cost model (v0.2.8): free-tier voice-only practice at 0.078 EUR/session vs 0.507 EUR/session with avatar (Simli)
   - Drills are the cheapest practice we can offer and enable unlimited free practice without destroying unit economics
1. **Drills are the high-frequency habit that feeds the conversion funnel.**
   - A learner can fit several 1-5 min drills into a day where they would not start a full conversation
   - High-frequency drill practice builds the daily habit that converts free users into paid conversation users

---

## 2. Business Opportunity

| Business lever | Impact |
|---------------|--------|
| Free-tier unlimited practice | Drills are the cheapest AI practice (~0.08 EUR/session free tier). See [Cost Model Summary](../../product-context/cost-model-summary.md) for full breakdown. |
| Conversion to paid | Free users who build a drill habit are the conversion pool for Plus/Career tiers. Target: >=5% free-to-paid conversion [~] |
| Session volume | Drills are expected to carry the majority of practice sessions by count (short, repeatable). Quality here drives aggregate engagement metrics |

---

## 3. Users & Personas

> **Shared reference:** See [Personas & Tiers](../../product-context/personas-and-tiers.md) for full persona definitions and tier entitlements.

- **Explorer (Free)** - Primary drills user. Drills are the only AI practice available at this tier.
- **Hobbyist Hana (Plus)** - Uses drills between conversation sessions
- **Professional Pedro (Pro)** - Pronunciation drills for accent polish between meetings

---

## 4. Scope

### In scope (MVP) - !!! JH: list out all types of drills!!!

- **Pronunciation drills** - listen to native audio, repeat word/phrase, get phoneme-level scoring with visual feedback (feature matrix B1)
- **Vocabulary drills** - flashcard with speech input, spaced repetition scheduling (B2)
- **Grammar exercises** - fill-in-the-blank and sentence construction with voice input, instant correction (B3)
- **Drill session summary** - words practiced, accuracy rate, pronunciation scores, time spent (B5)
- **Wordbook** - personal vocabulary collection with SRS review (B6)
- **Voice-only drill UI** - waveform vizualisation, phoneme heatmap (green/yellow/red per sound), recording state indicator, vocabulary flashcard display

### Out of scope

- **Listen & Comprehend** (B4) - post-MVP
- **Conversation (guided + role-play)** - AI Conversation Experience PRD (delivered audio-only or with avatar)
- **Avatar rendering** - AI Avatar PRD
- **Content generation** - Curriculum Factory PRD

---

## 5. Goals & Success Metrics

### Goals

1. **Deliver a high-quality drill experience** that drives pronunciation, vocabulary, and grammar practice for free and paid tiers
2. **Build the daily practice habit** that anchors retention and feeds the conversation funnel
3. **Enable the free-tier conversion funnel** - high-volume practice (effectively unlimited, pending the cap decision in OQ-5) at near-zero cost that hooks learners into the paid tiers

### Success Metrics

| Metric | Definition | Baseline | Target | Timeframe |
|--------|-----------|----------|--------|-----------|
| Drill completion rate | % of drills where learner completes all items (does not abandon mid-drill) | N/A (new) | >=60% [~] | GA + 30 days |
| Weekly drill sessions per active user | Average drill sessions (pronunciation + vocabulary + grammar) per WAU | N/A (new) | >=3 sessions/week [~] | GA + 90 days |
| Drill-to-conversation funnel | % of free-tier users who complete >=5 drills and then start a conversation session | N/A (new) | >=15% [~] | GA + 90 days |

### Guardrails

| Guardrail                                                              | Threshold                                          | Action                                                                                     |
| ---------------------------------------------------------------------- | -------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| Pronunciation scoring accuracy (false positive rate on phoneme errors) | <10% false positive rate [~] on calibration corpus | Alert Engineering; if >15%, suppress scoring and show "Try again in a quieter environment" |
| Cost per drill session                                                 | Must not exceed 0.15 EUR (paid) or 0.08 EUR (free) | Alert PM + Engineering; investigate cost spike                                             |
|                                                                        |                                                    |                                                                                            |

### Non-goals

- **Pronunciation scoring model training** - we use an existing ASR/pronunciation API (Azure, Deepgram); we do not train our own model
- **Gamification** (streaks, leaderboards, XP) - post-MVP
- **Offline drill mode** - post-MVP

---

## 6. User Stories

### Explorer (Free)

**US-1: Pronunciation drill**
As a free-tier learner, I want to hear a native-speaker example, repeat it, and see phoneme-level feedback showing which sounds I got right and which need work, so that I can improve my pronunciation systematically.

*Acceptance criteria:*
- Native reference audio plays for each target word/phrase
- Learner records their attempt via microphone
- Phoneme-level scoring displayed as a heatmap (green/yellow/red per sound)
- Learner can retry immediately
- Drill targets weak phonemes identified from the learner profile
- **Failure case:** If mic fails or background noise is too high (ASR confidence <0.4), show "We couldn't hear you clearly - try a quieter spot" instead of a bad score
- **Failure case:** If pronunciation scorer returns low confidence (<0.5), show "Score uncertain" indicator rather than potentially wrong feedback

**US-2: Vocabulary drill with speech input**
As a free-tier learner, I want to see a vocabulary flashcard, say the word aloud, and get pronunciation + meaning feedback, so that I practise both recall and pronunciation together.

*Acceptance criteria:*
- Flashcard shows word/phrase with translation and example sentence
- Learner speaks the word; system scores pronunciation
- Spaced repetition scheduling surfaces words at optimal intervals (Cepeda et al. 2006)
- Words marked "mastered" require fewer reviews; words marked "learning" appear more frequently
- **Cold start:** New users with no word history see a starter set of high-frequency words for their CEFR level

### Hobbyist Hana (Plus)

**US-3: Grammar drill between conversations**
As Hana, I want quick grammar fill-in and sentence-construction exercises with voice input and instant correction, so that I can shore up a specific structure in a few minutes without starting a full conversation.

*Acceptance criteria:*
- Exercise presents a target grammar structure with fill-in-the-blank or sentence construction
- Learner responds by voice; system transcribes and corrects instantly with a short explanation
- Drill can be completed in under 5 minutes
- Errors feed the learner profile so the structure resurfaces until mastered

---

## 7. Requirements

### Functional Requirements

| ID    | Requirement                                                                                                                   | Priority | Source               |
| ----- | ----------------------------------------------------------------------------------------------------------------------------- | -------- | -------------------- |
| FR-01 | System shall play native reference audio and score learner pronunciation at the phoneme level with visual heatmap feedback.   | P0       | Feature matrix B1    |
| FR-02 | System shall deliver vocabulary drills with speech input and spaced repetition scheduling.                                    | P0       | Feature matrix B2    |
| FR-03 | System shall deliver grammar exercises with voice input and instant correction with explanation.                              | P0       | Feature matrix B3    |
| FR-04 | Post-drill summary shall show: words practiced, accuracy rate, pronunciation scores, time spent.                              | P1       | Feature matrix B5    |
| FR-05 | Wordbook shall allow learners to save words/phrases from any session, browse, search, and review via SRS scheduling.          | P2       | Feature matrix B6    |
| FR-06 | !!!JH review !!!<br>Voice UI shall display waveform visualisation, recording state, and phoneme-level feedback during drills. | P0       | Architecture Layer C |

### Non-Functional Requirements

| ID | Requirement | Target | Rationale |
|----|------------|--------|-----------|
| NFR-01 | **Drill start latency** | <3 seconds from tap to first reference audio | Drills must feel instant for short-burst practice |
| NFR-02 | **Cost per drill session** | <=0.15 EUR/session (paid tiers); <=0.08 EUR/session (free tier) | Cost model v0.2.8 |
| NFR-03 | **Pronunciation scoring latency** | <1 second from end of learner utterance to feedback display | Must feel responsive for drill-level interaction |

### Privacy

Inherits all privacy constraints from [Privacy & Data Requirements](../../product-context/privacy-and-data-requirements.md). Drills record and score learner speech under the same consent, retention, and GDPR requirements. **Note:** a free-tier learner may reach drills before ever starting a conversation, so the voice-recording consent gate must fire on the first *drill* session, not only the first conversation session.

---

## 8. AI Evaluation Plan (Pronunciation Scoring)

Pronunciation scoring is probabilistic - the same utterance can receive different phoneme scores depending on accent, background noise, and model confidence.

### Evaluation methodology

- **Calibration corpus:** >=50 utterances [~] from native and non-native speakers at A1-B2, covering multiple accents (American English, British English, Indian English, German-accented English, Japanese-accented English at minimum)
- **Scoring:** Each utterance has a human-annotated phoneme-level ground truth. Automated scorer is evaluated against this ground truth
- **Cadence:** Run on every pronunciation model or API change

### Eval thresholds

| Metric | Launch | Target | Aspirational |
|--------|--------|--------|-------------|
| Phoneme-level accuracy (agreement with human annotation) | >=75% [~] | >=85% | >=90% |
| False positive rate (flagging correct pronunciation as wrong) | <15% | <10% | <5% |
| False negative rate (missing actual errors) | <25% [~] | <15% | <10% |

### Guardrails

| Rule | Threshold | Action | Fallback |
|------|-----------|--------|----------|
| Low ASR confidence | Confidence <0.4 | Suppress scoring | "We couldn't hear you clearly - try again in a quieter spot" |
| Low pronunciation scorer confidence | Confidence <0.5 | Show "Score uncertain" indicator | Allow retry; do not penalize in SRS scheduling |
| Unsupported accent detected | Accuracy drops >20pp vs calibration corpus for a user segment | Alert Engineering; flag for accent-specific tuning | Show word-level score only (suppress phoneme detail) |
| Background noise | SNR <10dB [~] | Suppress scoring entirely | "Background noise is too high for scoring" |

### Failure modes

| Failure mode | Fallback |
|-------------|----------|
| Pronunciation API timeout (>2s) | Show "Scoring unavailable - practicing without feedback" and let learner continue the drill without scores |
| Pronunciation API down | Degrade to vocabulary/grammar drills only; hide pronunciation drills from menu |
| Mic permission denied | Show setup instructions; offer text-input fallback for vocabulary/grammar drills |

---

## 9. Launch Plan

### Phase 1: Internal Dogfood (Aug 2026)

**Entry criteria:**
- Pronunciation and vocabulary drill flows functional in browser
- Pronunciation scoring API integrated (Azure or Deepgram - see AI Conversation Experience OQ-2)

**Exit criteria:**
- No P0 bugs blocking drill flow
- Pronunciation scoring operational for English
- >=10 drill items per CEFR level (A1-B2) available
- >=30 internal drill sessions completed
- Qualitative feedback collected from >=10 internal users

### Phase 2: Beta (Sep 2026)

**Entry criteria:**
- Phase 1 exit criteria met
- Grammar exercises functional
- Wordbook and SRS scheduling functional
- Pronunciation eval calibration corpus scored (Section 8)

**Exit criteria:**
- Drill completion rate >=50% [~]
- Pronunciation scoring accuracy >=75% on calibration corpus
- Drill start <3 seconds
- Cost per session within tier targets (NFR-02)

### Phase 3: GA (Oct 2026)

**Entry criteria:**
- Phase 2 exit criteria met
- Drill completion rate >=55% [~]
- Pronunciation false positive rate <15%

**Rollback plan:**
- Feature flag disables drills per-user, per-tier, or globally
- If pronunciation scoring degrades, drills degrade to vocabulary/grammar only (no pronunciation drills)
- Rollback trigger: pronunciation false positive rate >20% or cost per session >2x target

---

## 10. Decisions Requiring PDRs

| Decision | Current position | Why it needs a PDR | When |
|----------|-----------------|-------------------|------|
| **SRS algorithm choice** | Open - Anki/SM-2 family vs custom | SRS scheduling is embedded in the product data model and affects learner outcomes. Hard to switch post-launch without data migration. | Before Phase 2 beta (Sep 2026) |

---

## 11. Open Questions

| # | Question | Owner | Status |
|---|----------|-------|--------|
| 1 | **Phoneme visualisation design:** What does the pronunciation heatmap look like? IPA display or simplified? | Design | Open |
| 2 | **SRS algorithm:** Use existing algorithm (Anki/SM-2 family) or build custom? See Decisions Requiring PDRs above. | Engineering | Open |
| 3 | **Drills vs conversation entry points:** Are drills and conversation separate entry points in the app or a unified "practice" flow? | Design + PM | Open |
| 4 | **Pronunciation scoring vendor:** Azure Speech vs Deepgram vs a dedicated pronunciation API. Shared open question with AI Conversation Experience OQ-2. | Engineering | Open |
| 5 | **Free-tier drill limits:** Are drills truly unlimited for free tier, or is there a daily/weekly cap? Impacts cost model and the "unlimited practice" positioning. | PM | Open - by Phase 2 (Sep 2026) |
| 6 | **Free-tier persona:** The cost model assumes a $0 free tier but the canonical persona doc has no free-tier persona. Define "Explorer" (or equivalent) in the canon, or re-scope the free-tier thesis. Foundational to the conversion funnel in this PRD and the Avatar PRD. | PM | Open - by Jul 15 2026 |

---

## Sources

- AI Conversation Experience PRD: `PRDs/ai-conversation/ai-conversation-prd.md`
- Feature matrix: `product/PRDs/feature-matrix.md` (Section B)
- Cost model: `strategy/business-context/berlitz_cost_model_v0.2.8.xlsx`
- Cepeda et al. 2006 - Spacing effect (SRS grounding)
