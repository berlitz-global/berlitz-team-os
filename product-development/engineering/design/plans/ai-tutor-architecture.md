# Berlitz Learner App & AI Tutor - Architecture Model

**Created:** 2026-06-07
**Status:** Draft
**Audience:** Product, Engineering, Design leadership

---

## 1. Overview

This document defines the building-block architecture for the Berlitz Learner App and its strategic core -- the AI Tutor module. It separates essential MVP components from future enhancements, giving the team a shared mental model for what we're building and how it grows.

**Two-level scope:**
- **Learner App** (web + mobile): the outer shell, described at a coarse level
- **AI Tutor Module**: the strategic core, described in depth

The AI Tutor will progressively take over more of the learning experience. Today it's one module among many; by 2027 it's the primary way learners interact with Berlitz.

**Key architectural facts:**
- The AI Tutor has two interaction modes: **Audio-Only** (drill-level) and **Avatar** (conversation-level)
- Berlitz's pedagogical IP (PDF instructor/student guides) feeds a Content Pipeline that generates AI-usable scenarios
- The AI Tutor must follow the Berlitz Method and speak at the learner's CEFR level
- Real teacher-learner recordings serve as ground truth for evaluation

---

## 2. System Context -- The Learner App

The Learner App is the container. Web ships Sep 2026; mobile Oct 2026.

```
Berlitz Learner App (Web + Mobile)
|
+-- Authentication & Onboarding        [Essential]
+-- Home / Dashboard                   [Essential]
+-- AI Tutor Module                    [Essential] <-- strategic core, see section 3
+-- Human Session Booking & Delivery   [Differentiator]
+-- Progress & Assessment              [Essential]
+-- Content Library Browser            [Differentiator]
+-- Settings & Profile                 [Essential]
+-- Credit & Subscription Management   [Essential]
+-- Notifications & Engagement         [Differentiator]
```

### App Module Descriptions

| Module | Description | Tier |
|--------|-------------|------|
| Authentication & Onboarding | Social login (B2C), SSO/SAML (B2B), placement test, L1/L2 selection, learning goal setting | Essential |
| Home / Dashboard | Daily activity, next lesson suggestion, streak, credit balance, upcoming human sessions | Essential |
| AI Tutor Module | Audio-only drills + avatar conversations. See section 3. | Essential |
| Human Session Booking & Delivery | Browse available teachers, book with credits, join video session, post-session feedback | Differentiator |
| Progress & Assessment | CEFR level tracker, skills radar, lesson history, vocabulary mastery, certificates | Essential (basic), Differentiator (CEFR cert) |
| Content Library Browser | Browse available lessons by topic, level, skill type; preview before starting | Differentiator |
| Settings & Profile | Language preferences, notification settings, subscription management, data export | Essential |
| Credit & Subscription Management | View balance, purchase credits, manage subscription tier, view usage history | Essential |
| Notifications & Engagement | Streak reminders, daily goals, milestone celebrations, session reminders | Differentiator |

### App-Level Integration Points

| System | Purpose |
|--------|---------|
| Metronome | Credit consumption, usage metering |
| Stripe | Payments, subscription billing |
| Scheduling service | Human teacher session booking |
| Identity provider | SSO/SAML (enterprise), social login (B2C) |
| Analytics pipeline | Event streaming, product analytics |
| Push notification service | Engagement, reminders |

---

## 3. AI Tutor Module -- Detailed Architecture

The AI Tutor is broken into four layers plus an evaluation framework.

```
+---------------------------------------------------------------+
|                    Layer C: Presentation                       |
|   +---------------------------+  +-------------------------+  |
|   |    Audio-Only Mode        |  |     Avatar Mode         |  |
|   |  (drills, pronunciation)  |  |  (conversation, RP)     |  |
|   +---------------------------+  +-------------------------+  |
|   |              Shared Session UI                          |  |
+---------------------------------------------------------------+
                            |
+---------------------------------------------------------------+
|                    Layer B: AI Engine                          |
|  Session Orchestrator | Conversational AI | ASR | TTS         |
|  Pronunciation Analysis | Grammar Feedback | Adaptive Diff.  |
|  CEFR Assessment                                              |
+---------------------------------------------------------------+
                            |
+---------------------------------------------------------------+
|                    Layer A: Content Pipeline                   |
|  PDF Ingestion | Content Structuring | Prompt Generation      |
|  Berlitz Method Encoding | Level-Appropriate Language         |
|  Content QA | Versioning & Rollout                            |
+---------------------------------------------------------------+
                            |
+---------------------------------------------------------------+
|                    Layer D: Learning Intelligence              |
|  Learner Profile | Event Pipeline | Teacher Context Bridge    |
|  Adaptive Curriculum Engine                                   |
+---------------------------------------------------------------+
                            |
+---------------------------------------------------------------+
|           Evaluation & Simulation Framework                   |
|  Simulation Engine | Ground Truth Benchmark | Eval Pipeline   |
+---------------------------------------------------------------+
```

---

### Layer A -- Content Pipeline (offline, pre-session)

Transforms Berlitz's pedagogical IP into AI-usable material. This is where Berlitz's 140-year content advantage becomes a defensible AI moat.

#### Components

**A1. PDF Ingestion Engine**
Extracts structured content from Berlitz instructor guides and student guides: lesson goals, story outlines, vocabulary lists, grammar definitions, dialog scripts, exercise instructions.

**A2. Content Structuring & Tagging**
Organizes extracted content by:
- CEFR level (A1 through C2)
- Lesson unit and sequence position
- Skill type (grammar, vocabulary, pronunciation, conversation, reading, listening)
- Topic (travel, business, daily life, etc.)

Output: a structured content store that the Prompt Generation Engine can query.

**A3. Prompt Generation Engine**
LLM-powered pipeline that transforms structured lesson content into runtime-ready material:

| Output Type | What It Contains |
|-------------|-----------------|
| Conversation scenarios | Goal, context, character roles, vocabulary bounds, grammar focus, CEFR level, success criteria |
| Pronunciation drills | Target phonemes, words, phrases, native reference audio IDs |
| Role-play scripts | Character description, setting, objectives, expected dialog flow, success criteria |
| Practice exercises | Fill-in, translation, comprehension questions, answer keys |

**A4. Berlitz Method Encoding**
System prompts and guardrails that encode the Berlitz teaching methodology:
- Immersive target-language use (minimize L1, maximize L2)
- Question-answer cycles (teacher asks, student answers, teacher corrects/expands)
- Graduated difficulty (scaffold up, don't jump levels)
- Error correction style (gentle, contextual, not interrupting flow)
- Encouragement patterns (praise effort, celebrate progress)

These are injected into every AI Tutor session as system-level instructions.

**A5. Level-Appropriate Language Constraints**
Ensures the AI Tutor's own output matches the learner's CEFR level:
- A1: simple present, basic vocabulary (~500 words), short sentences
- A2: past tense introduced, ~1,000 words, compound sentences
- B1: all common tenses, ~2,500 words, expressing opinions
- B2: complex grammar, ~5,000 words, nuanced discussion
- C1/C2: near-native complexity

Vocabulary and grammar in the AI's responses are bounded by what the learner has been exposed to in their curriculum position.

**A6. Content QA & Review**
Human-in-the-loop review of generated prompts/scenarios before they go live. Pedagogical experts verify:
- Berlitz Method compliance
- Level-appropriateness
- Cultural sensitivity
- Factual accuracy
Aligns with the "AI Suggests. Humans Decide." principle.

**A7. Content Versioning & Rollout**
- Version control for all generated scenarios
- Staged rollout (internal -> beta users -> general availability)
- A/B testing framework for scenario variants
- Rollback capability if quality issues surface

#### Content Pipeline Data Flow

```
Berlitz PDF Materials (Instructor Guide + Student Guide)
    |
    v
PDF Ingestion Engine (extract text, tables, dialog scripts)
    |
    v
Structured Content Store
  (lesson goals, vocabulary, grammar, story outlines)
  (tagged by CEFR level, unit, skill type)
    |
    v
Prompt Generation Engine (LLM transforms structured content into:)
    +-- Conversation scenarios
    +-- Pronunciation drills
    +-- Role-play scripts
    +-- Practice exercises
    |
    v
Content QA Review (human reviewer approves/edits)
    |
    v
Scenario Library (versioned, tagged, ready for runtime)
    |
    v
AI Tutor Session
  (scenario loaded with Berlitz Method system prompts + level constraints)
```

---

### Layer B -- AI Engine (real-time, in-session)

The runtime AI powering both audio-only and avatar modes.

#### Components

**B1. Session Orchestrator**
Manages the full session lifecycle:
- Mode selection (audio-only vs avatar)
- Scenario loading from the Scenario Library
- Conversation state management (turn tracking, topic threading)
- Session timing and pacing
- Credit/entitlement checks (via Metronome)
- Graceful session ending (goal met, time up, learner exits)

**B2. Conversational AI Core**
LLM-powered dialogue engine. The heart of the AI Tutor.
- Scenario context injection (goals, vocabulary bounds, grammar focus from Content Pipeline)
- Berlitz Method system prompts (from Layer A)
- Conversation memory: within-session (full context) + cross-session (learner history summary)
- Guided mode: follows scenario script with branching based on learner responses
- Open-ended mode: free conversation within topic/level constraints
- Mode switching: tutor can shift from guided to open-ended mid-session based on learner confidence

**B3. Speech-to-Text / ASR**
Real-time voice input processing.
- Must handle accented, non-native speech well (primary use case)
- Streaming transcription for low-latency conversation flow
- Language detection (confirm learner is speaking target language)
- Confidence scoring on transcription (flag uncertain words)

**B4. Text-to-Speech / TTS**
Natural voice output for the tutor.
- Native speaker voice for target language
- Accent modeling (e.g., neutral American English, British English, Castilian Spanish)
- Adjustable speed (slower for A1, natural for B2+)
- Multiple voice personas (match avatar personality)
- Streaming output for low-latency response

**B5. Pronunciation Analysis**
Core to audio-only mode; also active in avatar mode.
- Phoneme-level scoring against native reference
- Stress and intonation pattern analysis
- Comparison visualization (learner vs native waveform)
- Targeted drill generation for weak phonemes
- Progress tracking per phoneme over time

**B6. Grammar & Vocabulary Feedback**
- Real-time inline correction during conversation (gentle, in-context)
- Post-session detailed review with explanations
- Error pattern tracking (recurring mistakes get extra practice)
- Vocabulary usage tracking (new words used correctly, words still not attempted)

**B7. Adaptive Difficulty**
Adjusts in real-time and across sessions:
- Conversation complexity (sentence length, vocabulary range)
- Error tolerance (more scaffolding for struggling learners)
- Scaffolding level (hints, sentence starters, vocabulary prompts)
- Pacing (more repetition for slow learners, faster progression for strong ones)
- Input: learner performance in current session + historical profile data

**B8. CEFR Assessment Engine**
- Placement test at onboarding (estimate initial CEFR level)
- Continuous level estimation from session performance
- Level-up decisions (consistent performance triggers level progression)
- Certification readiness scoring (is the learner ready for a formal assessment?)
- Pre/post assessment for enterprise ROI measurement

#### Session Data Flow (runtime)

```
Learner opens AI Tutor
    |
    v
Credit/entitlement check (Metronome)
    |
    v
Mode selection: Audio-Only or Avatar
    |
    v
Scenario selection
  (from Scenario Library, filtered by learner level + curriculum position)
    |
    v
Session Orchestrator initializes:
  - Loads scenario definition (goals, vocabulary bounds, grammar focus)
  - Injects Berlitz Method system prompt
  - Sets level-appropriate language constraints
  - Loads learner context (history, weak spots, preferences)
    |
    v
Conversation Loop:
  Learner speaks -> ASR -> text
      -> Conversational AI (generates response + inline feedback)
      -> TTS -> audio output
      -> [Avatar mode: lip-sync + expressions + gestures]
      -> [Audio-only mode: phoneme scoring + visual feedback]
  (repeat until session goal met or time/turns exhausted)
    |
    v
Post-session:
  - Session summary generated (LLM summarizes performance)
  - Grammar/vocabulary notes compiled
  - Pronunciation scores aggregated
  - Learning events stored (every utterance, correction, score)
  - Learner profile updated (level estimate, mastery progress)
  - Teacher context updated (for next human session)
  - Credit consumed / usage metered
```

---

### Layer C -- Presentation (what the learner sees)

Two distinct interaction modes sharing the same AI Engine (Layer B).

#### Audio-Only Mode (drill-level interaction)

Targeted, short practice sessions focused on pronunciation, vocabulary, and grammar drills.

- **Interaction pattern:** Listen -> Repeat -> Get feedback -> Try again
- **Session length:** 1-5 minutes
- **UI elements:**
  - Word/phrase display with phonetic transcription
  - Voice input indicator (waveform, recording state)
  - Phoneme-level feedback visualization (green/yellow/red per sound)
  - Repeat-after-me flow with native reference audio
  - Vocabulary flashcard drills with speech input
  - Grammar fill-in exercises with voice response
- **Key differentiator from avatar:** No visual character. Simpler UI. Faster to load. Focused on accuracy over fluency.

#### Avatar Mode (conversation-level interaction)

Multi-turn dialogue and role-play with an animated AI character.

- **Interaction pattern:** Conversation -> Correction -> Continue -> Review
- **Session length:** 5-20 minutes
- **UI elements:**
  - 3D animated avatar with lip-sync, facial expressions, gestures, personality
  - Scene/environment rendering (coffee shop, office, airport, etc.)
  - Real-time transcript alongside avatar
  - Inline correction highlights (grammar, vocabulary)
  - Visual cues and prompts (when learner is stuck)
  - Conversation recording and playback with avatar replay
- **Key differentiator from audio-only:** Visual engagement. Longer, open-ended conversations. Immersive context. Role-play with characters.

#### Shared UI (both modes)

- Session setup: scenario browsing, mode selection, difficulty preference
- In-session controls: pause, repeat last, slow down, request hint, translate word
- Post-session review: full transcript, grammar notes, new vocabulary list, pronunciation scores, session summary, XP earned
- Progress integration: streak update, level progress bar, skills radar update

---

### Layer D -- Learning Intelligence (cross-session, background)

The data and intelligence layer that makes the AI Tutor personalized and connected to human teaching.

**D1. Learner Profile & State**
Persistent per-learner data:
- Current CEFR level (overall + per-skill)
- L1 and L2
- Lesson history and curriculum position
- Error patterns (grammar, pronunciation, vocabulary)
- Vocabulary mastery (known, learning, not yet introduced)
- Pronunciation weak spots (by phoneme)
- Learning goals and pace preferences
- Session frequency and engagement patterns

**D2. Learning Event Pipeline**
Every interaction is logged for analytics and personalization:
- Utterances (learner + AI, with timestamps)
- Corrections applied (type, accepted/ignored)
- Pronunciation scores (per phoneme, per utterance)
- Session timing (duration, pauses, drop-offs)
- Scenario completion (goal met, partial, abandoned)
- Credit consumption events

**D3. Teacher Context Bridge**
Surfaces AI session insights to human teachers:
- What the learner practiced since last human session
- Where they struggled (specific grammar, pronunciation, vocabulary)
- Readiness signals ("learner has mastered past tense in AI practice, ready for B1 conversation")
- Error patterns that need human coaching attention
- Ensures the human teacher picks up where the AI left off -- no wasted time.

**D4. Adaptive Curriculum Engine**
Recommends what to learn next:
- Gap analysis: what's in the curriculum that the learner hasn't mastered?
- Next-best-scenario selection based on learner state
- Spaced repetition for vocabulary and grammar review
- Curriculum sequence awareness (follows Berlitz textbook progression)

---

## 4. Human Bridge & Enterprise

These sit at the app level, not inside the AI Tutor module, but integrate tightly with it.

### Human Bridge

| Component | Description | Tier |
|-----------|-------------|------|
| AI-Human Handoff | Escalation triggers (learner frustrated, topic too complex, assessment needed). Context package transferred to teacher. | Differentiator |
| Scheduling Integration | Book human sessions from within the AI Tutor ("Want to practice this with a real teacher?") | Differentiator |
| Session Continuity | Teacher sees AI practice history, error patterns, readiness signals before session starts | Differentiator |
| Teacher Quality Loop | Teacher observations (corrections, level assessments, notes) feed back into AI Tutor personalization | Enhancement |

### Enterprise

| Component | Description | Tier |
|-----------|-------------|------|
| Admin Dashboard | Team management, credit pool allocation, usage reporting | Differentiator |
| ROI Measurement | Pre/post CEFR assessment, business impact metrics, time-to-fluency tracking | Enhancement |
| Learning Analytics | Org-level progress, skills gaps, compliance completion | Enhancement |
| Identity & Access | SSO/SAML, SCIM provisioning, HRIS integration via Kombo | Enhancement |
| LMS/LTI Bridge | SCORM, xAPI export for enterprise learning management | Enhancement |

---

## 5. Evaluation & Simulation Framework

Critical infrastructure for validating that the AI Tutor actually teaches well. Built in parallel with the AI Tutor -- not as an afterthought.

### Simulation Engine

- **Synthetic learner profiles:** Varying CEFR levels, L1 backgrounds (Japanese, Spanish, Arabic, etc.), error patterns, learning styles
- **Automated session runner:** Simulates a learner interacting with the AI Tutor across scenarios
- **Measures:**
  - Pedagogical correctness (does the tutor follow the Berlitz Method?)
  - Level-appropriateness (is the AI's language within CEFR bounds?)
  - Error correction quality (timely, accurate, gentle?)
  - Conversation naturalness (does it feel like a real teacher?)
  - Goal completion rate (does the session achieve its learning objective?)
- **Use cases:** Regression testing after model/prompt changes, evaluating new content pipeline output, comparing LLM providers, benchmarking avatar vs audio-only effectiveness

### Ground Truth Benchmark

Berlitz has recordings of real teacher-learner sessions -- the gold standard for what good teaching looks like.

- Transcribe and annotate recordings: tag teacher moves (correction style, scaffolding, question types, praise patterns, error handling)
- Build an evaluation rubric derived from real teacher behavior
- Compare AI Tutor sessions against this rubric: "How close does the AI get to what a real Berlitz teacher would do?"
- Track improvement over time as prompts, models, and content are refined

### Eval Pipeline

```
Real teacher-learner recordings
    |
    v
Transcription + annotation
  (teacher moves, learner errors, correction patterns, pedagogical techniques)
    |
    v
Berlitz Teaching Rubric
  (derived from annotated sessions: what does good look like?)
    |
    v
AI Tutor sessions (simulated or real)
    |
    v
Rubric scoring (automated via LLM judge + human spot-check)
    |
    v
Quality dashboard
  (per-scenario, per-level, per-skill scores tracked over time)
```

**Tier:** Essential infrastructure. Without this framework, we cannot measure whether the AI Tutor is teaching or just chatting.

---

## 6. Essential vs Optional -- Full Classification

### ASSUMPTION (flag for review)

Both audio-only and avatar modes ship at MVP (Sep 2026). Audio-only handles drill-level interactions (pronunciation, vocabulary, short phrases). Avatar handles conversation-level interactions (multi-turn dialogue, role-play). This depends on avatar technology feasibility -- revisit after avatar tech evaluation.

### Essential (MVP Sep 2026)

Will not launch without these.

| Layer | Components |
|-------|-----------|
| Content Pipeline | PDF ingestion, content structuring, prompt generation (English curriculum), Berlitz Method encoding, level-appropriate language constraints |
| AI Engine | Session orchestrator, conversational AI core, ASR, TTS, basic grammar feedback, basic adaptive difficulty, basic pronunciation analysis |
| Presentation | Audio-only mode (drills) + avatar mode (conversation), shared session UI, post-session review |
| Learning Intelligence | Learner profile, basic event logging |
| App | Authentication, home dashboard, AI Tutor module, basic progress tracking, credit management |
| Evaluation | Simulation engine (basic), ground truth benchmark setup |

### Differentiator (Q4 2026)

Builds competitive advantage after launch.

| Layer | Components |
|-------|-----------|
| AI Engine | Advanced pronunciation analysis (phoneme-level), CEFR assessment engine |
| Human Bridge | AI-human handoff, teacher context bridge, scheduling integration |
| Content Pipeline | Content QA review workflow, content versioning |
| Enterprise | Basic admin dashboard, team reporting |
| App | Human session booking, content library browser, notifications/engagement |

### Enhancement (2027)

Deepens the moat.

| Layer | Components |
|-------|-----------|
| Content Pipeline | A/B testing of scenarios, automated content generation for new languages/skills |
| AI Engine | Advanced adaptive difficulty, accent training, writing assistance |
| Enterprise | ROI measurement, SSO/SAML/SCIM, LMS/LTI, compliance |
| App | Offline mode, gamification, multi-language expansion, skills & culture programs |
| Learning Intelligence | Adaptive curriculum engine, cross-learner analytics |
| Evaluation | L1 interference modeling in simulations, multi-language benchmark corpus |

---

## 7. Key Integration Points

| System | What | Protocol / Notes |
|--------|------|-----------------|
| LLM providers | Conversation engine, content generation, feedback, eval scoring | API (OpenAI, Anthropic -- evaluate both) |
| Speech providers | ASR + TTS | Streaming API (Deepgram, Azure Speech, Google, ElevenLabs) |
| Avatar engine | 3D rendering, lip-sync, expressions | TBD (web-based vs native engine -- key open question) |
| Metronome | Usage metering, credit consumption | API |
| Stripe | Payments, subscriptions | API |
| Kombo | HRIS integration for enterprise | API |
| HubSpot | CRM, lead tracking | API |
| Scheduling service | Human teacher session booking | Internal API |
| LMS/LTI | Enterprise learning management export | SCORM, xAPI, LTI |

---

## 8. Open Questions

### Technology Decisions

| Question | Impact | When to Decide |
|----------|--------|---------------|
| Avatar technology: web-based (Three.js) vs native (Unity/Unreal)? | Mobile performance, dev cost, time to market | Before MVP engineering starts |
| LLM provider: single vs multi-model routing? | Latency, cost, quality, vendor lock-in | Before MVP engineering starts |
| ASR provider: which handles non-native accented speech best? | Core UX quality for pronunciation features | Needs eval benchmark (2-3 week spike) |
| TTS provider: which delivers most natural target-language voice? | Learner experience, avatar believability | Needs eval benchmark |
| Real-time conversation latency target? | Sub-500ms for natural conversation feel | Architecture constraint -- decide early |

### Content Pipeline

| Question | Impact | When to Decide |
|----------|--------|---------------|
| How much human QA review per generated scenario? Can we hit 80%+ auto-approval? | Content velocity, cost, quality | After initial pipeline prototype |
| Who owns generated scenarios (IP rights)? | Legal, content licensing | Before content pipeline ships |
| Can the content pipeline generalize to new languages or must it be rebuilt per language? | 2027 multi-language expansion cost | After English pipeline is stable |

### Evaluation

| Question | Impact | When to Decide |
|----------|--------|---------------|
| How many teacher-learner recordings exist? What languages/levels? | Ground truth benchmark coverage | Inventory needed now |
| Are recordings already transcribed? Consent/privacy for benchmarking? | Legal, timeline for annotation | Legal review needed |
| How realistic do synthetic learner profiles need to be? Model L1 interference patterns? | Simulation fidelity, eval quality | After first simulation prototype |

### Product

| Question | Impact | When to Decide |
|----------|--------|---------------|
| Avatar at MVP: confirmed essential or contingent on tech feasibility? | MVP scope, timeline risk | After avatar tech evaluation |
| If avatar slips, what's the fallback? Audio-only + text-based conversation? | MVP launch risk | Before MVP engineering starts |
| Berlitz Method encoding: who validates the system prompts? | Pedagogical quality | Need designated Berlitz Method expert |

---

## 9. Relationship to Competitive Landscape

This architecture is informed by the competitive analysis of 13 competitors (see `product-development/product/competitive-research/`). Key competitive mapping:

| Architecture Component | Why It Matters Competitively |
|----------------------|----------------------------|
| Content Pipeline | No competitor has Berlitz's 140 years of structured pedagogical IP. This is the defensible moat. |
| Avatar Mode | Praktika (5/5) is the direct avatar competitor. Berlitz must match visual quality while adding curriculum depth. |
| Audio-Only Mode | ELSA (5/5 pronunciation) and Speak (5/5 conversation) set the quality bar for speech AI. |
| Berlitz Method Encoding | No AI-native competitor has a proprietary teaching methodology. This differentiates from GPT wrappers (TalkPal, Jumpspeak). |
| Human Bridge | No competitor connects AI practice to human coaching. This is the unique "top-right quadrant" play. |
| Evaluation Framework | Speak (OpenAI partnership) likely has sophisticated evals. Berlitz needs comparable rigor using its real teacher recordings. |
| Enterprise Layer | Rosetta Stone (4/5) and EF English Live (4/5) are the enterprise benchmarks. Must match for displacement deals. |
