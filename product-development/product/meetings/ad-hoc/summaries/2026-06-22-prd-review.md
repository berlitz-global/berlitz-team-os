# PRD Review — 2026-06-22
**Attendees:** Jan Hoffmann, Michal Sobocinski, Rob Zinkov
**Date:** 2026-06-22

## TL;DR
- The team walked through four PRDs (Curriculum Factory, Practice Drills, AI Conversation, AI Avatar), with the primary focus on Curriculum Factory and Practice Drills.
- Rob's recurring theme: the PRDs are comprehensive but don't yet clearly signal what goes into MVP — the team needs to agree on a prioritized 10–15-item list before sprint planning can happen.
- The team decided to defer full Curriculum Factory authoring tooling; the short-term MVP path is ingesting existing On Demand English content and making it mobile-friendly.
- A follow-up session was agreed for 2026-06-23 morning to negotiate MVP scope before Jan's Q3 planning PM meeting on Thursday.

## Discussion

### Tooling & Workflow for PRD Editing
The meeting opened with Jan sharing that he had used Claude to sync the PRDs to Confluence, but noted formatting losses (numbered lists, tables) in the round-trip. Obsidian was raised as an alternative — better table rendering, nicer formatting — but sharing links externally is still unsolved. The team agreed a background sync service (daily or on-demand) would reduce friction. Jan expressed frustration with the GitHub web UI; Rob suggested building lightweight GitHub dashboards or editing via Claude Code.

### Curriculum Factory PRD
Jan walked through the PRD structure: problem statement, non-goals, user stories, output formats, functional requirements, non-functional requirements, and evaluation plan. Rob's main feedback: the PRD tries to cover everything from dogfood through post-launch, and he always jumps to the "dogfood / MVP" section first. He suggested adding dependency tracking to requirements alongside priorities (P0/P1). The team agreed the MVP path is: (1) ingest existing On Demand English content as-is, (2) use AI to transform it to be mobile-friendly, treating that transformation as an early Curriculum Factory spike. Building a full CMS/LMS authoring UI is deferred. Michal raised the open question of whether the MVP will use the current LMS or a new one; this needs alignment with the mobile app team.

### Practice Drills PRD
Jan surfaced the definitional question: what counts as a "drill"? Rob's position: grammar drills, fill-in-the-blank, multiple choice — all are drills. Rob pushed back gently on multiple choice as not obviously fitting the Berlitz method (which emphasizes speaking); Jan noted an activity taxonomy document includes multiple choice. The team agreed drills should skew toward voice/speaking output. Jan pointed out a misplaced "instrumentation schema" section in the PRD; Rob agreed it's too low-level for a PRD and it was removed. The practice drills PRD maps to what Srikant is calling the "practice tab" in the mobile app.

### AI Conversation & AI Avatar PRDs
These were only briefly touched. The AI Avatar PRD is the least pressing — it is downstream of both the AI Conversation and Practice Drills work, and a product can ship without it. The AI Conversation PRD review was started near the end of the meeting.

### Annotation & Review Workflow
A side thread ran throughout on how to leave inline comments on markdown PRDs. Options explored: Confluence comments, Obsidian inline comment plugin (visible only in edit mode), GitHub PR comments, and Rob's custom CSS/div-based comment macros. No definitive answer reached.

### Content Ingestion Architecture
Michal pushed for clarity on whether the MVP will introduce a new LMS or extend the current one. Rob's framing: because so much lesson content already exists and meets CEFR/Berlitz-level requirements, step one is just ingest and transform it — skip the authoring problem. Jan agreed, framing it as two steps: (1) take existing On Demand content and put it into whatever LMS the mobile app will use; (2) AI-transform it to be mobile-friendly. SCORM was mentioned as a possible atomic unit format for Curriculum Factory output.

### Diagrams
Jan shared a system architecture diagram in Obsidian showing how Gold, Lemonade, Noodle, Hyperwave, Flex, and P5 fit together. Rob was enthusiastic about it and plans to share it more widely. Jan has the PowerPoint source and will store it in the repo.

## Decisions
- Defer full LMS/CMS authoring UI to post-MVP.
- MVP content path: ingest existing On Demand English content directly; transform to mobile-friendly using AI as a Curriculum Factory spike.
- Remove the "instrumentation schema" section from the Practice Drills PRD (too low-level; belongs in a schema doc or ADR).
- Product context (Berlitz method, cost model, personas) to be consolidated into a shared `product-context/` folder rather than duplicated across PRDs.
- Jan will stop editing PRDs in the old repo; Rob will migrate them to `berlitz-knowledge-base`.
- AI Avatar PRD is lowest priority — deprioritize until AI Conversation and Practice Drills are further along.

## Action items
| Owner | Action | Status |
|-------|--------|--------|
| Rob Zinkov | Share Jan's learner-system architecture diagram in a broader channel | pending |
| Rob Zinkov | Migrate PRDs from berlitz-team-os to berlitz-knowledge-base repo | pending |
| Jan Hoffmann | Clone berlitz-knowledge-base repo and stop editing in berlitz-team-os | pending |
| Jan Hoffmann | Rewrite Curriculum Factory ingestion steps (step 1: ingest On Demand content; step 2: AI mobile-friendly transform) | pending |
| Jan Hoffmann | Update Practice Drills PRD: define scope of "drills", add priorities, clarify FR1 vs FR6 overlap | pending |
| Jan Hoffmann | Store architecture diagram PowerPoint in the repo | pending |
| Rob Zinkov / Jan Hoffmann | Hold follow-up session 2026-06-23 morning to negotiate MVP scope (10–15 prioritized items) | pending |
| Rob Zinkov / Jan Hoffmann | Coordinate with mobile app team on presentation layer for drills (endpoint contract) | pending |
| Rob Zinkov | Investigate Obsidian inline-comment plugin options for PRD review workflow | pending |
| Team | Align with mobile app team on new vs. current LMS for MVP | pending |

## Open questions
- Will the MVP use the current LMS or a new one? Who on the mobile app side owns that decision?
- Who has access to the On Demand video content, and what is the transcription/ingestion cost (Andres Mora noted no transcripts exist for learning videos)?
- Is SCORM the right atomic unit format for Curriculum Factory output?
- What is the right inline-comment workflow for reviewing markdown PRDs?
- When will a full detailed walk-through of all PRD functional requirements happen (suggested: when Ali is available)?

## Misc
- The meeting ran ~27 minutes over the scheduled 1 hour (transcript ends at 01:27:19).
- Jan has a Q3 planning PM meeting on Thursday 2026-06-25 and wants MVP scope settled before then.
- Rob has a presentation commitment on expected AI system interfaces that he is behind on — Jan's architecture diagram will be directly useful for that.
- Sergey returns from a trip on 2026-06-23; the engineering meeting at 10 AM will likely run a full hour.
