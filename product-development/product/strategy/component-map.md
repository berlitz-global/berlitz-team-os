# Berlitz Learner App - Component Map

> **Status:** Draft
> **Last Updated:** 2026-06-19
> **Purpose:** MECE list of app components for roadmap planning. Each component can be planned independently: what's MVP, what comes next, what's future.

---

## Component List

18 components across 5 areas. Each row is independently plannable.

### A. App Shell (the container every user touches)

| # | Component | What it does | MVP | Next | Future |
|---|-----------|-------------|-----|------|--------|
| 1 | **Auth & Onboarding** | Login (social B2C, SSO/SAML B2B), placement test, L1/L2 selection, learning goal setting | Social login, basic placement test, language selection | SSO/SAML for enterprise, SCIM provisioning | HRIS integration (Kombo), multi-language onboarding |
| 2 | **Home & Dashboard** | Daily activity, next lesson, streak, credit balance, upcoming sessions | Next AI session recommendation, basic streak, credit balance | Personalized daily plan, upcoming human sessions | Adaptive home based on learner behaviour |
| 3 | **Progress & Assessment** | CEFR tracking, skills radar, lesson history, certificates | Basic progress bar per level, lesson history | Per-skill CEFR breakdown (speaking, listening, grammar, vocabulary), skills radar | CEFR certificates, enterprise ROI measurement, pre/post assessment |
| 4 | **Credits & Billing** | Purchase credits, manage subscription, view usage | Stripe integration, Metronome metering, tier management | Credit pooling for enterprise, usage analytics | Multi-currency, invoicing, volume discounts |
| 5 | **Notifications & Engagement** | Streak reminders, daily goals, milestones, session reminders | Basic push reminders (session, streak) | Daily goals, milestone celebrations, re-engagement campaigns | Adaptive notification timing, social features |

### B. Content Pipeline (offline - what feeds the AI)

| # | Component | What it does | MVP | Next | Future |
|---|-----------|-------------|-----|------|--------|
| 6 | **Content Ingestion** | Extracts structured content from Berlitz source materials (PDF guides, CEFR specs, vocabulary Excel, lesson transcripts) | PDF + Excel + CEFR ingestion for English A1-B2 | Transcript ingestion (teaching pattern extraction), incremental re-ingestion | Multi-language source ingestion, automated change detection |
| 7 | **Scenario Generation** | LLM-powered pipeline that transforms structured content into AI-ready scenarios (conversations, role-plays, drills) | Generate >=50 scenarios across A1-B2 with schema validation and vocab bound checking | Adversarial review agent (automated quality gate), batch generation | Simulation Engine validation pre-review, auto-approval for high-confidence scenarios |
| 8 | **Scenario Library** | Versioned store of approved scenarios - the runtime content source for AI sessions | Searchable library with CEFR/skill/topic filtering, <200ms query latency | Content versioning, effectiveness scoring from telemetry, gap tracking | A/B testing of scenario variants, automated removal of underperformers |

### C. AI Engine (real-time - what powers the session)

| # | Component | What it does | MVP | Next | Future |
|---|-----------|-------------|-----|------|--------|
| 9 | **Conversation Engine** | LLM-driven dialogue: scenario loading, Berlitz Method compliance, turn management, conversation memory | Guided conversation + role-play with Berlitz Method system prompts, CEFR-bounded output | Open conversation mode (free topic within level), cross-session memory | Mode switching (guided to open mid-session), crosstalk (L1<>L2) |
| 10 | **Speech Pipeline (ASR + TTS)** | Voice in (learner speech to text) and voice out (AI response to speech) | Streaming ASR (Deepgram/Azure), streaming TTS (Azure Neural), <500ms voice-to-first-audio | Accent-specific ASR tuning for non-native speakers, TTS voice selection per dialect | On-device ASR for offline drills, custom Berlitz voice cloning |
| 11 | **Pronunciation Scoring** | Phoneme-level pronunciation analysis and feedback | Word-level and phoneme-level scoring with heatmap feedback (Azure/Deepgram) | Stress and intonation analysis, targeted drill generation for weak phonemes | Phoneme progress tracking over time, accent-aware scoring |
| 12 | **Grammar & Vocabulary Feedback** | Real-time correction during conversation + post-session review | Inline grammar correction (salient prompts, not recasts), post-session grammar/vocab notes | Error pattern tracking across sessions, vocabulary mastery tracking | Adaptive correction strategy per learner (more/less scaffolding) |
| 13 | **CEFR Assessment** | Level estimation and progression | Basic placement test at onboarding, manual level setting | Continuous level estimation from session performance, level-up triggers | Certification readiness scoring, formal assessment integration, enterprise pre/post measurement |

### D. Presentation (what the learner sees and hears)

| # | Component | What it does | MVP | Next | Future |
|---|-----------|-------------|-----|------|--------|
| 14 | **Practice Drills UI** | Voice-only interface for pronunciation, vocabulary, and grammar drills | Pronunciation drills with phoneme heatmap, vocabulary flashcards with SRS, grammar exercises with voice input | Wordbook (personal vocabulary collection), drill session summary | Listen & Comprehend mode, gamification (streaks, XP per drill) |
| 15 | **Conversation UI** | Shared UI for guided conversation and role-play (audio-only and avatar modes) | Real-time transcript with inline corrections, session controls (pause, hint, repeat), post-session review | Conversation recording & playback, session bookmarking | Scene/environment variety, multiple avatar personas |
| 16 | **Avatar Rendering** | 3D animated character with lip-sync, expressions, gestures | Single customizable avatar (appearance, dialect), Simli (Plus-Career) + HeyGen (Premium-Enterprise), graceful degradation to audio-only | Avatar style refinement, gesture library expansion | Self-hosted rendering (cost reduction), on-device avatar, multiple avatar characters |

### E. Intelligence & Integration (cross-session, background)

| # | Component | What it does | MVP | Next | Future |
|---|-----------|-------------|-----|------|--------|
| 17 | **Learner Profile & Analytics** | Per-learner state (CEFR level, error patterns, vocabulary mastery, curriculum position) + event pipeline | Basic learner profile, event logging (all ai.* and drill.* events), analytics queries | Adaptive curriculum engine (next-best-scenario), spaced repetition engine, learning analytics dashboard | Org-level analytics for enterprise, cohort analysis, efficacy measurement (CEFR progression rate) |
| 18 | **Human-AI Bridge** | Connects AI practice with human teacher sessions | None (human sessions exist in current Berlitz Portal, not in new app MVP) | Teacher context bridge (AI session insights surfaced before human session), scheduling integration | AI-human handoff (escalation triggers), teacher quality loop (teacher feedback improves AI), LMS/LTI/SCORM export |

---

## Component Dependency Map

```
                    Content Ingestion [6]
                         |
                    Scenario Generation [7]
                         |
                    Scenario Library [8]
                         |
          +--------------+--------------+
          |                             |
   Conversation Engine [9]      Practice Drills UI [14]
          |                             |
   +------+------+              Pronunciation Scoring [11]
   |             |
Speech Pipeline  Grammar &
  [10]          Vocab Feedback [12]
   |
   +------+------+
   |             |
Conversation  Avatar
  UI [15]     Rendering [16]

Cross-cutting:
- Auth & Onboarding [1] gates everything
- Credits & Billing [4] gates session start
- Learner Profile [17] feeds Conversation Engine [9] + CEFR Assessment [13]
- CEFR Assessment [13] feeds Learner Profile [17] (circular)
- Home & Dashboard [2] reads from Learner Profile [17]
- Progress & Assessment [3] reads from Learner Profile [17]
- Human-AI Bridge [18] reads from Learner Profile [17]
```

---

## How to Use This

1. **Per-component roadmap:** For each component, plan what ships when. The MVP/Next/Future columns are a starting point - refine with engineering estimates.
2. **Dependency planning:** Use the dependency map to sequence work. Content Pipeline must lead AI Engine. Auth must lead everything.
3. **Team allocation:** Each component can be owned by a team or individual. Some components (Speech Pipeline, Avatar Rendering) are vendor-integration heavy; others (Conversation Engine, Scenario Generation) are prompt-engineering heavy.
4. **Feature requests:** When a new feature request comes in, map it to a component. If it doesn't fit, either the component list needs updating or the request is out of scope.
