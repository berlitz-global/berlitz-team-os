# Berlitz Content Taxonomy

> **Status:** Draft - needs validation by LX team
> **Last Updated:** 2026-06-19
> **Owner:** PM
> **Sources:** Berlitz Flex course structure (Confluence), berlitz.com proficiency levels, AI Tutor architecture doc, PRDs

This document defines the content hierarchy from program level down to atomic activity, with typical quantities and durations. It is the single reference for terminology used across PRDs, architecture docs, and engineering plans.

---

## Content Hierarchy

```
Program
 └─ Level (= 1 Berlitz proficiency level, maps to CEFR)
     └─ Module (quarter of a level)
         └─ Unit (a single teachable chunk - the scheduling atom)
             └─ Activity (what the learner actually does inside a unit)
```

---

## Hierarchy Detail

| Layer | Definition | Typical quantity | Typical duration | Examples |
|-------|-----------|-----------------|-----------------|----------|
| **Program** | A purchased product that bundles one or more levels with a delivery mode | 1-8 levels per program | 6-12 months license | "Berlitz Flex English 1-4", "Berlitz On Demand German 5-8", "Private Online English 3" |
| **Level** | One Berlitz proficiency level (1-10). The primary unit of progression. Contains all content needed to advance one step on the Berlitz scale. | 36 self-paced lessons + 4 checkpoints + 20 live coaching sessions + 36 review units (optional) per level | 66-84 hours total [~] | "English Level 3", "German Level 7" |
| **Module** | A quarter of a level. Groups units into a manageable milestone with a checkpoint at the end. Introduced to reduce learner overwhelm (completing a full level = 60+ items). | 4 modules per level | ~17-21 hours per module [~] | "English Level 3 - Module 2" |
| **Unit** | A single teachable chunk - the atom of scheduling and progress tracking. One unit = one row on the learner path. Has a type that determines its delivery mode and content. | 9 lessons + 1 checkpoint + 5 coaching sessions + 9 reviews per module (24 units per module, ~96 per level including reviews) | Varies by type (see Unit Types below) | "Unit 14: At the Restaurant", "Checkpoint #2", "Live Coaching Session #7" |
| **Activity** | What the learner does inside a unit. The atomic interaction. In self-paced units, activities are sequenced screens/exercises. In AI sessions, an activity is a scenario or drill. | Varies - a self-paced lesson has 10-20 screens/exercises [~]; an AI session runs 1 scenario or multiple drills | 1-45 min depending on type | A vocabulary flashcard, a pronunciation drill, a guided conversation scenario, a grammar fill-in-the-blank |

---

## Unit Types

| Unit type | Delivery mode | Duration | Content source | Description |
|-----------|-------------|----------|---------------|-------------|
| **Lesson** (self-paced) | Async, in-app | 15-30 min [~] | Authored in LMS authoring tool (Lemonade) | Interactive screens: vocabulary introduction, grammar explanation, reading, listening, exercises. Currently tap-based. |
| **Live Coaching Session** | Sync, with instructor (1:1 or group) | 30-60 min [~] | Instructor Guide (IG) | Live session with a Berlitz instructor. Follows the Berlitz Method. Instructor uses IG materials. |
| **Review Unit** | Async, in-app | 15-30 min [~] | Authored in LMS | Revisits content from the preceding lessons. Flex-only (not shown to Live Online / Face-to-Face students). |
| **Checkpoint** | Async, in-app | 15-30 min [~] | Authored in LMS | Assessment at the end of each module (units 10, 20, 30, 40). Tests mastery of the module's content. |
| **Culture Unit** | Async, in-app | 10-15 min [~] | Authored in LMS | Cultural context content. Levels 1-4 only. Displayed below modules regardless of which module is selected. |
| **Curriculum Test** | Sync or async | 30-60 min [~] | Standardized | End-of-level proficiency test. Unlocked when all level content is complete. Gates progression to the next level. |

---

## AI Tutor Activity Types (new for the Learner App)

These are the activity types the AI Tutor introduces. They supplement (and in some cases replace) the existing self-paced lesson activities.

| Activity type | PRD | Duration | Delivery | Description |
|--------------|-----|----------|----------|-------------|
| **Guided Conversation** | AI Conversation Experience | 10-20 min | AI engine + voice (audio-only or avatar) | Scenario-based dialogue following Berlitz curriculum. AI plays instructor role. Has learning objectives, vocabulary bounds, grammar focus, success criteria. |
| **Role-Play** | AI Conversation Experience | 10-20 min | AI engine + voice (audio-only or avatar) | Pre-defined scenario where learner plays one character and AI plays the other (e.g., job interview, hotel check-in). |
| **Pronunciation Drill** | Practice Drills | 1-5 min | AI engine + voice (audio-only) | Listen to native audio, repeat, get phoneme-level scoring. Targets weak phonemes from learner profile. |
| **Vocabulary Drill** | Practice Drills | 1-5 min | AI engine + voice (audio-only) | Flashcard with speech input. Spaced repetition scheduling. |
| **Grammar Exercise** | Practice Drills | 1-5 min | AI engine + voice (audio-only) | Fill-in-the-blank or sentence construction with voice input and instant correction. |
| **Microlearning Lesson** | TBD (post-MVP) | 2-5 min | In-app, tap-based | Babbel/Duolingo-style 10-20 tap exercises. Feeds into AI practice. Not yet scoped for AI Tutor MVP. |

---

## Berlitz Levels to CEFR Mapping

| Berlitz Level | CEFR | Name | Description |
|:---:|:---:|------|-------------|
| 1 | A1 | Beginner | Introduce yourself, ask simple questions, basic conversations with support |
| 2 | A2.1 | Elementary 1 | Understand general messages, hold simple conversations, describe daily activities |
| 3 | A2.2 | Elementary 2 | Understand familiar topics, initiate/maintain conversations, give simple instructions |
| 4 | A2.3 | Elementary 3 | Understand familiar topics, make professional contacts, write notes and letters |
| 5 | B1.1 | Intermediate 1 | Hold conversations on various topics, explain things contextually, give work instructions |
| 6 | B1.2 | Intermediate 2 | Communicate competently in professional/personal situations, participate with native speakers |
| 7 | B1.3 | Intermediate 3 | Express viewpoints, defend ideas, handle challenging situations, give presentations |
| 8 | B2.1 | Upper Intermediate 1 | Communicate efficiently in complex situations, give professional presentations |
| 9 | B2.2 | Upper Intermediate 2 | Communicate with various audiences, participate confidently in discussions, write error-free texts |
| 10 | C1/C2 | Advanced / Professional | Express spontaneously and fluently, understand complex texts, near-native proficiency |

Source: [berlitz.com/en-de/about/proficiency-levels](https://www.berlitz.com/en-de/about/proficiency-levels)

> **AI Tutor MVP scope:** Levels 1-8 (CEFR A1-B2). Levels 9-10 are post-MVP.

---

## Typical Numbers at a Glance

| Metric | Value | Source |
|--------|-------|--------|
| Berlitz levels | 10 (mapping to CEFR A1-C2) | berlitz.com |
| Modules per level | 4 | Confluence: Berlitz Flex Modules |
| Self-paced lessons per level | 36 (9 per module) | Confluence: Berlitz Flex Modules |
| Live coaching sessions per level | 20 (5 per module) | Confluence: Berlitz Flex Modules |
| Checkpoints per level | 4 (1 per module) | Confluence: Berlitz Flex Modules |
| Review units per level | 36 (optional, 9 per module) | Confluence: Berlitz Flex Modules |
| Total items per level | 60-96 (depending on reviews) | Confluence: Berlitz Flex Modules |
| Hours per level | 66-84 hours | Confluence: Berlitz Flex Modules |
| Hours per module | ~17-21 hours [~] | Derived (level hours / 4) |
| AI conversation session length | 10-20 min | AI Conversation Experience PRD |
| AI drill length | 1-5 min | Practice Drills PRD |
| Microlearning lesson length | 2-5 min | Spec research (Chayan Roy, Jun 3 2026) |
| AI Tutor MVP scenario target | >=50 scenarios across A1-B2 | Curriculum Factory PRD |
| AI Tutor GA scenario target | >=15 guided conversations + >=8 role-plays | AI Conversation Experience PRD |

---

## Term Disambiguation

| Term | Means | Does NOT mean |
|------|-------|--------------|
| **Level** | One Berlitz proficiency level (1-10) | CEFR level (use "CEFR level" when referring to A1-C2) |
| **Module** | A quarter of a Berlitz level (9 lessons + checkpoint + coaching) | A software module or app module |
| **Unit** | A single teachable chunk on the learner path (lesson, coaching session, checkpoint, review) | A CEFR unit or a curriculum unit (use "unit" only for learner path items) |
| **Lesson** | A self-paced learning unit with interactive screens/exercises | A live instructor session (use "coaching session" or "live session") |
| **Session** | A single AI interaction (conversation or drill set) | A live coaching session (use "coaching session" to disambiguate) |
| **Scenario** | A structured AI conversation with objectives, vocab bounds, and success criteria (lives in the Scenario Library) | A vague "use case" - scenarios are concrete, authored content |
| **Drill** | A short, focused, voice-driven practice activity (pronunciation, vocabulary, grammar) | A full conversation session |
| **Activity** | The atomic interaction inside a unit or session | The broader concept of "learner activity" (engagement) |
| **Learner path** | The ordered sequence of units a learner progresses through, defined by the LX team | A marketing term for the customer journey |
| **SCORM package** | A standards-compliant export of content for enterprise LMS integration (post-MVP) | The internal content format (we use JSON scenarios internally) |

---

## Open Questions

| # | Question | Owner | Status |
|---|----------|-------|--------|
| 1 | **Level names:** Are "Elementary 1/2/3", "Intermediate 1/2/3" the official Berlitz names, or just CEFR descriptors? Need official naming from GLP. | PM + GLP | Open |
| 2 | **Unit duration:** Self-paced lessons are estimated at 15-30 min. What is the actual median completion time from LMS data? | Analytics | Open |
| 3 | **Microlearning definition:** Chayan raised whether MVP includes tap-based micro-lessons (Jun 3 2026). How do they relate to self-paced lessons - supplement, replace, or standalone? | PM + LX | Open |
| 4 | **AI activities within existing units:** Do AI conversation scenarios and drills replace self-paced lesson activities, or are they a separate track alongside the existing learner path? | PM + LX | Open |
| 5 | **Levels 5-8 electives:** Levels 5-8 have Core (modules 1-2) + Elective (modules 3-4) structure. Does this affect AI content generation scope? | PM + Content | Open |
| 6 | **Children/teens (IDEAL):** The Berlitz IDEAL system for children/teens has a different level structure. Is this in scope for the AI Tutor? | PM | Open - assumed out of scope for MVP |
