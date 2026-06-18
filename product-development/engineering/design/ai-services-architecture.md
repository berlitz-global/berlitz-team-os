# AI Tutor — Services Architecture Diagram

> Derived from `ai-tutor-architecture.md`, AI Conversation PRD, Practice Drills PRD, Curriculum Factory PRD.

```mermaid
%%{init: {
  "theme": "base",
  "themeVariables": {
    "primaryColor": "#003478",
    "primaryTextColor": "#ffffff",
    "primaryBorderColor": "#001f4d",
    "lineColor": "#E31837",
    "secondaryColor": "#EDF2F8",
    "clusterBkg": "#EDF2F8",
    "clusterBorder": "#003478",
    "edgeLabelBackground": "#ffffff",
    "fontFamily": "Arial, sans-serif"
  }
}}%%
flowchart TB
    classDef pres      fill:#E31837,stroke:#b5122c,color:#fff
    classDef session   fill:#003478,stroke:#001f4d,color:#fff
    classDef speech    fill:#1a5ca8,stroke:#003478,color:#fff
    classDef infer     fill:#003478,stroke:#001f4d,color:#fff
    classDef intel     fill:#2e7d9c,stroke:#1a5c73,color:#fff
    classDef curric    fill:#1a5ca8,stroke:#003478,color:#fff
    classDef evalNode  fill:#5a6e8a,stroke:#3d4f63,color:#fff
    classDef ext       fill:#f0f4f8,stroke:#8da5bf,color:#003478
    classDef store     fill:#001f4d,stroke:#001f4d,color:#fff

    %% ── Presentation ──────────────────────────────────────────────────────
    subgraph PRES["  Presentation  "]
        direction LR
        AUDIO_UI["Audio-Only\nDrills · Phoneme Viz\n1–5 min"]
        AVATAR_UI["Avatar\nConversation · Role-Play\n5–20 min"]
        SESS_UI["Session UI\nControls · Hints · Post-Session Review"]
    end

    %% ── Session Service (real-time coordinator) ───────────────────────────
    subgraph SESSION["  Session Service  "]
        ORCH["Orchestrator\nLifecycle · Turn State · Credit Check\nAdaptive Difficulty (in-session)"]
    end

    %% ── Speech I/O Service ────────────────────────────────────────────────
    subgraph SPEECH["  Speech I/O Service  "]
        ASR["ASR  ·  Deepgram Nova-3\nStreaming · Non-Native Accents\nLanguage Detection · Confidence Score"]
        TTS["TTS  ·  Azure Neural\nNative Voice · Speed Adaptation\nStreaming Output"]
        PRON["Pronunciation  ·  Azure Speech\nPhonem-Level · Stress · Intonation\n(runs parallel to ASR on same audio)"]
    end

    %% ── Inference Service ─────────────────────────────────────────────────
    subgraph INFER["  Inference Service  "]
        LLM["Claude Sonnet  ·  ≥32k ctx\nConversation + Grammar/Vocab Feedback\nBerlitz Method System Prompts injected here"]
    end

    %% ── Data Stores ───────────────────────────────────────────────────────
    SCLIB[("Scenario Library\nScenarios · Drills · Role-Plays\nVersioned, CEFR-tagged")]
    PROF[("Learner Profile\nCEFR · Lesson History · Error Patterns\nVocab Mastery · Pronunciation Weak Spots")]

    %% ── Event Pipeline ────────────────────────────────────────────────────
    EVT[["  Event Pipeline\nai.session.* · ai.utterance.* · ai.correction.*\n ai.eval.compliance · ai.feedback.*  "]]

    %% ── Learner Intelligence Service ──────────────────────────────────────
    subgraph INTEL["  Learner Intelligence Service  "]
        CEFR_SVC["CEFR Assessment\nPlacement · Continuous Estimation\nLevel-Up · Cert Readiness"]
        RECO["Curriculum Engine\nNext-Best Scenario · Gap Analysis\nSpaced Repetition"]
        TCB["Teacher Bridge\nStruggle Areas · Readiness Signals\nAI → Human Handoff Package"]
    end

    %% ── Curriculum Service (offline) ──────────────────────────────────────
    subgraph CURRIC["  Curriculum Service  (Offline / Batch)  "]
        PDF["PDF Ingestion\nInstructor + Student Guides\nLesson Goals · Vocab · Dialog Scripts"]
        STRUCT["Content Structuring\nTagged: CEFR · Unit · Skill · Topic"]
        PGEN["Prompt Generation\nLLM-Powered\nScenarios · Drills · Role-Plays · Exercises"]
        METHOD["Berlitz Method Config\nSystem Prompts · CEFR Language Bounds\nImmersion Rules · Correction Style"]
        CQA["Content QA & Versioning\nHuman Expert Review · Staged Rollout\nA/B Variants · Rollback"]
    end

    %% ── Eval Service (offline / batch) ───────────────────────────────────
    subgraph EVAL["  Eval Service  (Offline / Batch)  "]
        GT["Ground Truth\nAnnotated Teacher Recordings\nBerlitz Teaching Rubric"]
        SIM["Simulation Engine\nSynthetic Learner Profiles\nAutomated Session Runs"]
        JUDGE["LLM Judge + Human Audit\n5-Dimension Rubric\n≥ 85% blocks model/prompt deploy"]
    end

    %% ── External ──────────────────────────────────────────────────────────
    subgraph EXT["  External Services  "]
        direction LR
        METRO["Metronome\nUsage Metering"]
        STRIPE["Stripe · IdP\nBilling · Auth"]
        SCHED["Teacher Scheduling\nHuman Session Booking"]
    end

    %% ══ DATA FLOWS ════════════════════════════════════════════════════════

    %% Curriculum Service → Scenario Library
    PDF --> STRUCT --> PGEN
    METHOD --> PGEN
    PGEN --> CQA --> SCLIB

    %% Session bootstrap (Scenario Library and Learner Intelligence are
    %% both upstream of Session Service)
    SCLIB  -->|"scenario + system prompts\n+ CEFR constraints"| ORCH
    PROF   -->|"learner context\n+ weak spots"| ORCH
    RECO   -->|"recommended scenario"| ORCH

    %% Real-time conversation loop
    %% Audio in: Session → ASR (transcript) → LLM → TTS (audio) → Presentation
    %% Pronunciation runs parallel to ASR on the same audio stream
    ORCH   -->|"audio stream"| ASR
    ASR    -->|"transcript"| LLM
    LLM    -->|"response text"| TTS
    ASR    -->|"raw audio"| PRON

    %% Outputs to Presentation
    TTS    -->|"audio  ·  p95 < 500 ms"| AVATAR_UI
    TTS    -->|"audio"| AUDIO_UI
    PRON   -->|"phoneme scores + waveform"| AUDIO_UI
    LLM    -->|"corrections + vocab\nsuggestions"| SESS_UI
    ORCH   -->|"hints · prompts\nsession state"| SESS_UI

    %% Event bus: Session Service emits → Learner Intelligence consumes
    ORCH   -->|"all session events"| EVT
    EVT    --> PROF
    EVT    --> CEFR_SVC
    EVT    --> TCB
    EVT    --> RECO

    %% Billing
    ORCH   -->|"credit check + metering"| METRO

    %% Eval quality loops
    GT     --> JUDGE
    SIM    --> JUDGE
    JUDGE  -->|"compliance gate\n≥ 85% to deploy"| INFER
    JUDGE  -->|"content quality\nfeedback"| CURRIC

    %% External app-level
    STRIPE -.->|"billing · auth"| PRES
    SCHED  -.->|"teacher handoff"| TCB

    %% Apply styles
    class AUDIO_UI,AVATAR_UI,SESS_UI pres
    class ORCH session
    class ASR,TTS,PRON speech
    class LLM infer
    class CEFR_SVC,RECO,TCB intel
    class PDF,STRUCT,PGEN,METHOD,CQA curric
    class GT,SIM,JUDGE evalNode
    class METRO,STRIPE,SCHED ext
    class SCLIB,PROF store
```

## Service map

| Service | Runtime | Owns | Downstream of |
|---------|---------|------|---------------|
| **Curriculum Service** | Offline / batch | Scenario Library | — |
| **Session Service** | Real-time | Session lifecycle · adaptive difficulty | Scenario Library, Learner Profile, Curriculum Engine |
| **Speech I/O** | Real-time | ASR · TTS · Pronunciation | Session Service |
| **Inference Service** | Real-time | LLM conversation · corrections | Session Service (via ASR transcript) |
| **Learner Intelligence** | Async / cross-session | Learner Profile · CEFR · curriculum recs · teacher bridge | Event Pipeline |
| **Eval Service** | Offline / batch | Quality gate · compliance score | Curriculum Service outputs; Inference Service (gates deploys) |

## Design decisions recorded here

- **B8 CEFR Assessment moved to Learner Intelligence.** It reads session events and writes to the Learner Profile — that's Learning Intelligence, not AI Engine.
- **Grammar Feedback (B6) folded into Inference Service.** It is LLM output structuring, not a separate service.
- **Adaptive Difficulty (B7) stays in Session Service.** In-session real-time; distinct from the cross-session Curriculum Engine (D4).
- **Pronunciation runs parallel to ASR**, not downstream of it — both consume the same raw audio stream.
- **Eval Service feeds back to Curriculum Service**, not only to Inference — this closes the content quality loop.
- **Event Pipeline is the sole channel between Session Service and Learner Intelligence** — nothing in the real-time path writes to the Learner Profile directly.
