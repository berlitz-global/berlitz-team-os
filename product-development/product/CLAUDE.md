# AI Tutor Product Context

## Overview

AI Tutor is Berlitz's [product description].

**North Star:** [To be defined]

---

## Folder Structure

```
product/
├── competitive-research/
│   └── competitors/          # Competitor audits and feature matrices
├── customers/                # Account context, calls, feature requests
├── strategy/                 # Roadmaps, vision, business context
├── product-context/          # Reference docs for AI Tutor systems
├── PRDs/                     # Product requirement documents
├── sales-enablement/         # Sales-facing docs, onboarding
├── processes/                # Operational processes
├── meetings/                 # Meeting notes
└── workflows/                # Workflow specs
```

---

## Core Pillars

| Pillar | Purpose | P0 Features |
|--------|---------|-------------|
| | | |
| | | |
| | | |

---

## Key Documents

| Purpose | Path |
|---------|------|
| Competitive Research | `competitive-research/CLAUDE.md` |
| Competitive Feature Matrix | `competitive-research/competitors/competitive-matrix.md` |
| Customer Accounts | `customers/CLAUDE.md` |
| PRDs | `PRDs/CLAUDE.md` |
| Analytics | `../analytics/CLAUDE.md` |

---

## Terminology

| Term | Definition |
|------|------------|
| Berlitz Method | Berlitz's proprietary teaching methodology: immersive L2 use, question-answer cycles, graduated difficulty, correction by salient prompts, encouragement patterns. See `product-context/berlitz-method-and-eval-rubric.md` |
| CEFR | Common European Framework of Reference for Languages. Berlitz uses 10 levels (1-10) mapping to CEFR A1-C2. See `product-context/content-taxonomy.md` |
| Phoneme visualisation | Visual feedback showing pronunciation accuracy per individual sound in a word. Displayed as a heatmap (green/yellow/red per sound) so the learner sees which sounds they got right and which need work |
| SRS (Spaced Repetition Scheduling) | Algorithm that decides when to resurface a vocabulary word for review. Words answered correctly appear less frequently; words answered wrong come back sooner. Based on the spacing effect (Cepeda et al. 2006). Classic implementation: SM-2 (Anki family) |
| Scenario | A structured AI conversation or exercise with defined learning objectives, vocabulary bounds, grammar focus, CEFR level, and success criteria. Lives in the Scenario Library. Produced by the Curriculum Factory |
| Learner path | The ordered sequence of units a learner progresses through, defined by the LX team. Determines what comes before and after each unit and what prerequisite knowledge each scenario assumes |
| Drill | A short (1-5 min), focused, voice-driven practice activity: pronunciation, vocabulary, or grammar. Distinct from conversation (multi-turn dialogue) |
| Guided conversation | A scenario-based AI dialogue (10-20 min) following Berlitz curriculum, where the AI steers toward learning objectives while responding to the learner's actual utterances |
| Role-play | A pre-defined scenario where the learner plays one character and the AI plays the other (e.g., job interview, hotel check-in) |
