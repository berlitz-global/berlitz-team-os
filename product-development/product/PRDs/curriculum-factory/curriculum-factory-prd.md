# Curriculum Factory PRD

| Field            | Value                                                                                                                                                                                                                                                                   |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Author**       | Jan Hoffmann, PM                                                                                                                                                                                                                                                        |
| **Status**       | Draft                                                                                                                                                                                                                                                                   |
| **Last Updated** | 2026-06-21                                                                                                                                                                                                                                                              |
| **Related RFC**  | [`PDR-001`](../../decisions/PDR-001-content-generation-approach.md) - LLM vs template vs hybrid generation                                                                                                                                                              |
| **Related Plan** | `engineering/design/plans/ai-tutor-architecture.md` (Layer A)                                                                                                                                                                                                           |
| **Epic**         | [#39 - Content Pipeline](https://github.com/berlitz-global/berlitz-services/issues/39)                                                                                                                                                                                  |
| **Child Issues** | [#26](https://github.com/berlitz-global/berlitz-services/issues/26) PDF Ingestion, [#28](https://github.com/berlitz-global/berlitz-services/issues/28) Prompt/Scenario Generation, [#33](https://github.com/berlitz-global/berlitz-services/issues/33) Scenario Library |

---

## Overview

The Curriculum Factory is the content pipeline that transforms Berlitz's pedagogical source materials into any format Berlitz needs - from Instructor Guides (PDF) to drills in the mobile app to AI-ready conversation scenarios. It runs offline at MVP; the vision is to evolve toward real-time personalized content delivery to increase learner stickiness. It ingests five types of source material - PDF instructor/student guides, CEFR reference specifications, vocabulary-to-lesson mappings (Excel), real lesson transcripts, and the **learner path** (defined by the LX team) - structures them, and uses LLM-powered generation to produce conversation scenarios, pronunciation drills, role-play scripts, and practice exercises. The output feeds the Scenario Library consumed by the AI Tutor at runtime.

**The overriding principle is output quality.** Every piece of generated content must meet the highest possible standards - linguistically correct, pedagogically sound, and rigorously grounded in the Berlitz Method. If the output quality is not to Berlitz instructor standards, nothing else matters. Speed and volume are valuable only after quality is assured.

**Feedback loops** will optimize both the learner path and lesson content over time:
- **Explicit feedback:** learner ratings, teacher observations, reviewer corrections
- **Implicit feedback:** learner progress signals, session completion rates, error pattern clustering, scenario effectiveness scores

**Automated QA** must scale with generation volume. The pipeline needs extensive "Berlitz level-appropriate" checks against the learner path and, ultimately, against actual learner knowledge. This may require a simulated learner agent that models the learning process based on the content provided - validating that a scenario is teachable before a real learner sees it. (See Simulation Engine, post-MVP roadmap #34.)

**Scope: language learning only.** Culture and skills programs are important future Berlitz areas but are out of scope for the MVP and this PRD. The pipeline is designed for English first, with language parameterisation for future expansion.

This PRD covers the **MVP pipeline** (architecture components A1-A5): ingestion, structuring, generation, Berlitz Method encoding, and level-appropriate language constraints - plus the quality assurance model that ensures output meets the bar. Content pipeline metrics (#15), business content modules (#14), and multi-language expansion (#24) are post-MVP.

Currently, the landscape of system looks like this.
![[legacy authoring and delivery.png]]

---

## 1. Problem Statement

1. **Berlitz has 140 years of pedagogical IP locked in static formats.** Instructor guides, student guides, CEFR reference material, vocabulary mappings, and lesson transcripts exist as PDFs, Excel files, and audio/text transcripts. None of this material is machine-readable or queryable. The AI Tutor cannot use any of it without manual extraction and reformatting. Every scenario created today is hand-authored from scratch - the existing curriculum is effectively invisible to the AI system. (architecture doc, Layer A)

2. **Hand-authored scenarios do not scale.** The AI Avatar PRD requires 5 guided conversations and 3 role-plays by Aug 2026 (dogfood), 15 guided conversations and 8 role-plays by Oct 2026 (GA), spanning CEFR levels A1-B2. Hand-authoring each scenario takes hours of instructional design time [~]. At steady state, the AI Tutor needs hundreds of scenarios across levels, skill types, and topics to avoid learner repetition and maintain engagement. Manual creation cannot reach this volume at acceptable cost or speed. (AI Avatar PRD, Section 9)

3. **Without structured content, the AI Tutor cannot enforce the Berlitz Method or respect CEFR bounds.** The AI Tutor's system prompts need vocabulary lists, grammar scoping, lesson objectives, and dialog patterns drawn from the Berlitz curriculum - not generic LLM knowledge. If the Tutor generates content from its own training data rather than Berlitz-specific material, it will drift from the Berlitz Method and produce level-inappropriate output. The content pipeline is what makes the AI Tutor a *Berlitz* tutor rather than a generic language chatbot. (architecture doc, A4-A5; competitive-matrix.md, Section B)

4. **Berlitz's richest pedagogical asset - real lesson transcripts - is untapped.** Transcripts of live face-to-face lessons capture how expert Berlitz instructors actually teach: their questioning patterns, correction timing, scaffolding techniques, and vocabulary choices by level. This is ground truth for what good Berlitz teaching looks like. Today, these transcripts sit unused. The Curriculum Factory can mine them for teaching patterns that inform scenario generation and evaluation rubrics. (architecture doc, Section 5) *Note: transcript ingestion is P1, not P0, because legal consent must be confirmed before processing - see Section 9.*

5. **Existing content is not mobile-friendly.** Berlitz's current learning materials - PDF instructor/student guides, LMS-authored Flex/On Demand units - were designed for desktop web delivery. They do not render well on mobile and cannot be consumed as bite-sized practice in a native app. The Learner App (web Sep 2026, mobile Oct 2026) needs content in a format that works across devices. The Curriculum Factory produces structured, device-agnostic scenarios that the app renders natively.

6. **Content creation is too slow to scale the language offering.** Updating or creating content for a single language currently takes over a year and requires a team of multiple LX designers plus external writers [~]. At this pace, expanding beyond the current language set (English, German, French, Spanish) is impractical, and keeping existing content fresh is a constant resource bottleneck. The pipeline must compress this cycle dramatically to make new languages and content updates viable.

7. **There is no way to measure content effectiveness today.** Current content lives in static PDFs and LMS units with no structured metadata, no learner-level telemetry, and no feedback loop. Berlitz cannot answer basic questions: which lessons drive the most speaking practice? Which scenarios do learners abandon? Where do error patterns cluster by level? The Curriculum Factory produces tagged, structured content linked to the Scenario Library, enabling per-scenario effectiveness scoring and data-driven content iteration for the first time.

---

## 2. Business Opportunity

### Strategic positioning

The competitive matrix (Section B: Content & Pedagogy) shows Berlitz targeting **5/5 on Structured Curriculum** - the highest score of any competitor, tied only with Duolingo, Babbel, and Lingoda. But unlike those competitors, Berlitz has a proprietary teaching methodology and 140 years of structured curriculum materials. The Curriculum Factory is what converts that historical advantage into an AI-native moat. (competitive-matrix.md)

> **[~] Assumption:** No AI-native competitor (Speak, Praktika, TalkPal, ELSA) has publicly disclosed a content pipeline grounded in proprietary pedagogical IP. Their content appears to be LLM-generated from generic training data or manually authored. Note: Speak scores 4/5 on Structured Curriculum - their content source is unknown, not confirmed absent. This assumption is inferred from public product analysis; no competitor has disclosed their pipeline architecture.

### Competitive differentiation

The architecture doc states: "This is where Berlitz's 140-year content advantage becomes a defensible AI moat." The reasoning:

- **AI-native competitors** (Speak 5/5 AI, Praktika 5/5 avatar) have strong technology but score 2-4/5 on Structured Curriculum and 1-2/5 on CEFR Alignment. They lack deep pedagogical content. (competitive-matrix.md)
- **Legacy competitors** (Rosetta Stone, Babbel, Lingoda) have structured content but score 1-2/5 on AI Capabilities. They lack the technology to use it dynamically.
- **Berlitz's play** is to combine both: deep content + strong AI. The Curriculum Factory is the bridge.

### Business levers

| Business lever | Impact |
|---------------|--------|
| Content velocity | Pipeline batch-generates scenarios ~8-16x faster than manual authoring [~]. Baseline: ~4-8 hours per scenario manually. Target: <30 min per scenario including validation. Batch generation amplifies this further - 10 scenarios in <30 min vs. 40-80 hours manual [~]. |
| Berlitz Method enforcement | Scenarios generated from Berlitz source material and constrained by Berlitz Method encoding are structurally compliant - not relying solely on LLM system prompts at runtime. (architecture doc, A4) |
| CEFR precision | Vocabulary and grammar constraints drawn from CEFR reference material and the vocabulary-to-lesson Excel mapping, not LLM approximations. Enables the >=95% known-vocabulary target in the Avatar PRD (NFR-04). |
| Competitive moat | Competitors cannot replicate Berlitz's source materials. Even if they build similar pipelines, they lack the input corpus. |
| Multi-language path | An English-first pipeline designed for language parameterization reduces marginal cost of expanding to Spanish, German, Japanese (post-MVP, #24). [~] |
| Cost reduction | Replaces manual instructional design labor for scenario creation. Cost per scenario drops from hours of expert time to ~$0.50-2.00 LLM inference cost [~] + 15-30 min review time [~]. |
| Mobile-native content | Transforms static PDFs and desktop-only LMS units into structured, device-agnostic scenarios the Learner App renders natively on web and mobile. Unblocks the mobile launch (Oct 2026). |
| Content cycle compression | Current cycle: 1+ year per language with multiple LX people + external writers [~]. Pipeline target: weeks, not years. Makes new language launches and content refreshes viable at scale. |
| Measurability | Structured, tagged content linked to the Scenario Library enables per-scenario effectiveness scoring, engagement tracking, and data-driven iteration - none of which is possible with today's static content. |

---

## 3. Why Now

1. **The AI Avatar launches Sep 2026 and needs scenarios to teach with.** The avatar is a conversation engine without content of its own. Without the Curriculum Factory, every scenario is hand-authored, creating a bottleneck that limits the avatar's launch scope and post-launch freshness. (AI Avatar PRD, Phase 1-3)

2. **Initial scenarios will be hand-crafted; the pipeline must take over before GA.** Dogfood (Aug 2026) can ship with hand-authored scenarios. But GA (Oct 2026) needs 15+ guided conversations and 8+ role-plays across A1-B2, and post-GA growth requires a continuous content supply. The pipeline must be producing validated scenarios by Sep 2026 to feed GA. (AI Avatar PRD, Section 9)

3. **Berlitz's content advantage is perishable.** AI-native competitors are generating content from LLMs at scale. As general-purpose LLMs improve at language teaching, the quality gap between generic and Berlitz-specific content narrows. The window to establish a structured content pipeline grounded in proprietary IP - before competitors close the gap with pure AI - is now. (strategic-positioning.md)

4. **Source material inventory is complete.** Four source types are available today: PDF instructor/student guides (extensive, multi-level), CEFR reference specifications, vocabulary-to-lesson Excel mappings, and real lesson transcripts. No new content needs to be created before the pipeline can start ingesting.

5. **The Simulation Engine (#34) and Berlitz Method Compliance (#13) depend on pipeline output.** Both require structured scenarios with annotated learning objectives, vocabulary bounds, and grammar focus to function. The pipeline's structured output is their input. Delaying the pipeline delays the entire evaluation framework.

---

## 4. Customer Requests

> All entries below are internal signals. No customer call transcripts exist for the content pipeline specifically. The pipeline is infrastructure - learners experience its output (scenarios) rather than the pipeline itself.

| Customer / Segment                | Verbatim                                                                                                                                             | Date        | Source               |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | -------------------- |
| Chayan Roy / Internal Engineering | "Raised question on MVP scope for micro-lessons and how existing course content flows into AI avatar practice" [~] (paraphrase)                      | Jun 3 2026  | Teams message        |
| Internal / Engineering            | "Berlitz's pedagogical IP (PDF instructor/student guides) feeds a Content Pipeline that generates AI-usable scenarios" - identified as Essential MVP | Jun 7 2026  | Architecture doc     |
| Internal / Product                | Avatar launch plan gates on scenario availability: 5 guided + 3 role-play for dogfood, scaling to 15+8 for GA                                        | Jun 16 2026 | AI Avatar PRD        |
| Market signal                     | Berlitz targets 5/5 on Structured Curriculum; no AI-native competitor exceeds 4/5. The gap is closable - urgency to formalize the content advantage. | Jun 2026    | Competitive analysis |

**Learner evidence plan:**
- **Owner:** PM
- **Deadline:** Post-GA (Dec 2026)
- **Scope:** Analyze scenario completion rates, learner feedback, and CEFR progression data to validate that pipeline-generated content performs comparably to hand-authored content.
- **Output:** Quality comparison report; findings feed back into pipeline tuning.

---

## 5. Goals & Success Metrics

### Users

**Content Author (Instructional Designer / Berlitz Method Expert):** The primary user of the pipeline. Today, content authors manually write scenarios from scratch by reading PDF guides and applying their knowledge of the Berlitz Method and CEFR levels. They are experienced language teaching professionals - typically 5+ years of Berlitz Method experience [~]. There are approximately 2-5 people in this role at launch [~]. Their current workflow is: read PDF guide → mentally map to CEFR level → write scenario in a document → peer review → hand off to engineering for integration. The pipeline replaces the "read → write" steps with "ingest → generate → review."

> **Learner personas** (the end consumers of generated content) are defined in [Personas & Tiers](../../product-context/personas-and-tiers.md).

### Goals @JH: review

1. **Build a repeatable pipeline that converts Berlitz source materials into AI-ready scenarios at 8-16x the speed of manual authoring** [~].
2. **Produce enough validated scenarios to meet the AI Avatar launch requirements** - 15 guided conversations and 8 role-plays across A1-B2 by GA (Oct 2026).
3. **Ensure every generated scenario is grounded in Berlitz curriculum** - vocabulary, grammar, and teaching patterns drawn from source materials, not generic LLM knowledge.
4. **Design the pipeline for language parameterization** so that multi-language expansion (post-MVP) requires new source material input, not a pipeline rebuild.

### Success Metrics

| Metric | Definition | Baseline | Target | Timeframe | Measurement |
|--------|-----------|----------|--------|-----------|-------------|
| Scenario generation time | Elapsed time from generation trigger to draft scenario passing validation | Manual: ~4-8 hours per scenario [~] (to be validated by timed authoring sessions in Phase 1) | <30 minutes per scenario (generation + automated validation) [~] | Pipeline v1 | Pipeline log: timestamp delta between `generation.started` and `validation.completed` events per scenario |
| Scenario volume | Total scenarios in the Scenario Library, tagged and ready for the AI Tutor | 0 (hand-authored scenarios tracked separately) | >=50 scenarios (guided + role-play + drills) across A1-B2 [~] | GA (Oct 2026) | Scenario Library query: COUNT where status = approved |
| Source material coverage | % of Berlitz English curriculum units with at least one generated scenario | 0% (denominator: total A1-B2 unit count to be confirmed from vocabulary-to-lesson Excel in Phase 1) | >=60% of A1-B2 curriculum units [~] | GA + 90 days | Scenario Library query: COUNT DISTINCT curriculum_unit / total curriculum units. Denominator confirmed as Phase 1 exit criterion. |
| Schema validation pass rate | % of generated scenarios that pass automated schema validation (required fields, CEFR tagging, vocabulary bounds) before entering review | N/A | >=95% | Pipeline v1 | Automated: schema validator output logged per generation run. COUNT(pass) / COUNT(total) |
| Berlitz Method alignment | % of generated scenarios that pass Berlitz Method compliance checks when avatar delivers them in a simulated session | N/A | >=85% [~] | GA | Expert spot-check: 3 reviewers score a random sample of >=50 scenarios against the 5-dimension rubric from AI Conversation Experience PRD Section 8. At n=50, 85% target has +/-10pp confidence interval. Post-MVP (Q4 2026): automated via Simulation Engine #34. |

### Guardrail Metrics

| Metric | Definition | Threshold | Breach action | Instrumentation |
|--------|-----------|-----------|---------------|-----------------|
| Vocabulary bound violation rate | % of generated scenario avatar utterances containing vocabulary above the tagged CEFR level | <5% (aligned with Avatar PRD NFR-04: >=95% within level band) | Scenario blocked from Scenario Library; returned to draft. If >10% of a generation batch exceeds threshold, generation pipeline paused for prompt review. | `validation.vocabulary_breach` event per scenario; aggregated per batch in pipeline logs. PM alerted via pipeline summary if batch rate >5%. |
| Factual/cultural error rate | % of scenarios flagged by reviewers for factual inaccuracy or cultural insensitivity | <2% [~] | Flagged scenario immediately removed from library if live; escalated to content lead. If >5% of reviewed scenarios are flagged in a batch, batch generation suspended pending prompt and source material review. | `review.flagged` event with `flag_type: factual_error | cultural_sensitivity` per scenario. Aggregated per review batch. Content lead alerted if batch rate >2%. |
| Pipeline-generated vs hand-authored quality delta | Learner session completion rate for pipeline-generated scenarios minus hand-authored scenarios | No statistically significant negative delta (measured post-GA) | If delta is negative and significant (p<0.05, n>=100 sessions per group), pipeline-generated scenarios flagged for quality audit. PM reviews and adjusts generation prompts or source material selection. | Scenario Library tags each scenario `source: pipeline | hand_authored`. Analytics query joins `avatar.session.ended` (from Avatar PRD instrumentation) with scenario source tag. PM runs comparison monthly post-GA. |

### Non-Goals

- **Culture and Skills content** - out of scope entirely. This PRD covers language learning only. Culture programs (localization, etiquette, cross-cultural communication) and skills programs (compliance, negotiation, presentation) are important future Berlitz areas but are not short-term and are not covered here.
- **Content Pipeline Metrics dashboard** (#15) - post-MVP. MVP tracks metrics manually or via basic queries.
- **Business Content Modules** (#14) - post-MVP. MVP covers general English curriculum only; industry-specific content (finance, healthcare, tech, legal) follows.
- **Multi-Language Expansion** (#24) - post-MVP. Pipeline is English-first but designed for language parameterisation.
- **Theming / engagement skins** - post-MVP. The idea of placing abstract lesson definitions into themed environments (e.g., "Star Trek", "Game of Thrones", "The Office") to increase engagement is a future extension. MVP content uses standard Berlitz scenarios.
- **Language-specific formality registers** - post-MVP. Languages like German and French have formal/informal address distinctions (Sie/Du, vous/tu) that affect content generation. This and other language-specific pragmatic rules must be accounted for when expanding beyond English, but are not in scope for the English-first MVP.
- **Automated content generation without human review** - not a goal at any phase. The pipeline generates drafts; humans validate. The adversarial agent reduces review load over time but does not replace human sign-off. "AI Suggests. Humans Decide." (architecture doc, A6)
- **Automated content removal based on telemetry** - post-MVP. MVP flags underperforming content for human review; automated removal requires higher confidence in the telemetry signal.

---

## 6. User Stories

### Content Author (Instructional Designer / Berlitz Method Expert)

**US-1: Ingest Berlitz source material**
As a content author, I want to upload Berlitz PDF guides, CEFR reference documents, vocabulary Excel mappings, and lesson transcripts into the pipeline, so that the system can extract structured content without me manually copying and reformatting.

*Acceptance criteria:*
- System accepts PDF, Excel (.xlsx), and text/transcript file uploads
- Extracted content is structured into queryable entities: lesson goals, vocabulary lists, grammar points, dialog scripts, story outlines, teaching patterns
- Each extracted entity is tagged with CEFR level, lesson unit, skill type, and topic
- Parse failures are flagged with the source location and error type for manual review
- Re-ingestion of updated source files detects changes and updates only the affected entities in the content store. Given a previously ingested PDF that has been updated, re-ingestion produces a changeset (added/modified/removed entities) that matches a manual diff of the two document versions for a spot-checked sample

**US-2: Generate scenarios from structured content**
As a content author, I want to trigger scenario generation for a specific curriculum unit and CEFR level, so that I get draft conversation scenarios, role-play scripts, and drill exercises grounded in Berlitz material.

*Acceptance criteria:*
- Author selects: target CEFR level, curriculum unit, skill type (conversation/role-play/pronunciation/grammar/vocabulary), and topic
- System generates one or more draft scenarios using the structured content for that unit
- Each generated scenario includes: learning objectives, vocabulary bounds, grammar focus, success criteria, and CEFR level tag. Format varies by skill type:
 - **Conversation/role-play:** dialog flow with character roles, scenario context, and branching points
 - **Pronunciation drill:** target phonemes/words/phrases, native reference audio IDs (if available), and pass/fail scoring criteria
 - **Grammar/vocabulary exercise:** prompt text, expected answer patterns, and explanation text for corrections
- Generated scenarios reference the source material they were derived from (traceability)
- Generation completes in <5 minutes per scenario [~]

**US-3: Review and approve generated content (two-stream model)**

Generated content follows two review streams depending on content type:

**Stream A - Instructor Guide (IG) content:** Content that instructors use in lessons (conversation scenarios, role-play scripts, teaching prompts). This reaches instructors naturally through their workflow. A **pilot group of ~20-50 instructors** [~] (selected for review skill, not random) receives generated IG content, uses it in real lessons, and provides structured feedback via a scorecard. Their feedback constitutes sign-off. Reviewing generated content is a skill - not all instructors are suited for it.

**Stream B - Student-facing content:** Content learners see directly but instructors don't use in sessions (micro-learning snippets, interactive practice elements, learning videos). This requires **explicit review by the LX team** since there is no natural instructor touchpoint. Instructors from the pilot group can supplement LX review but the LX team owns sign-off.

As a content author or reviewer, I want to review each generated scenario, edit it if needed, and approve or reject it, so that only validated content enters the Scenario Library.

*Acceptance criteria:*
- Reviewer can view the generated scenario alongside the source material it was derived from
- Reviewer can edit any field (dialog, vocabulary, objectives, level tag)
- Reviewer can approve (promotes to Scenario Library) or reject (returns to draft with notes)
- All edits are versioned and auditable
- Rejected scenarios include reviewer notes explaining the rejection reason
- Stream A content: instructor pilot group feedback captured via structured scorecard (rubric-aligned, not free-text only)
- Stream B content: LX team review tracked separately with explicit sign-off

**US-4: Adversarial review agent (automated quality gate)**
As the pipeline, I want an automated adversarial agent that reviews every generated scenario before it enters the human review queue, so that obvious quality issues are caught early and human review load decreases over time.

*Acceptance criteria:*
- **MVP scope (basic):** Agent checks vocabulary against CEFR level word lists (clearly defined, readily available). Scenarios with >5% out-of-level vocabulary are auto-rejected back to generation with flagged words.
- **MVP scope (basic):** Agent checks grammar structures against CEFR level grammar scope. Scenarios with structures above the tagged level are flagged.
- **Data collection for future sophistication:** Every human review decision (approve/reject/edit) and the reason is captured in structured format, linked to the scenario and the agent's pre-review assessment. This builds the training dataset for a more capable adversarial agent.
- **Post-MVP extension:** Agent expands to check Berlitz Method compliance dimensions (correction strategy, Q&A patterns, encouragement), trained on accumulated human review data. Target: reduce human review to flagged-only scenarios by 2027.
- Agent findings are logged as `review.agent.finding` events with `finding_type`, `severity`, `auto_action` (block / flag / pass)

**US-5: Browse and query the Scenario Library**
As a content author, I want to search and filter the Scenario Library by CEFR level, skill type, topic, and curriculum unit, so that I can see what content exists and identify gaps.

*Acceptance criteria:*
- Filter by: CEFR level, skill type, topic, lesson unit, status (draft/approved/live), review stream (IG / student-facing)
- Search by keyword across scenario text
- Gap view: curriculum units with no approved scenarios are visually flagged

### AI Tutor (System - runtime consumer)

**US-6: Load scenario at session start**
As the AI Tutor session orchestrator, I want to query the Scenario Library for an approved scenario matching the learner's CEFR level, curriculum position, and session type, so that I can initialize a session with the right content.

*Acceptance criteria:*
- Query accepts: CEFR level, skill type, topic preference (optional), curriculum position (from learner path)
- Returns an approved scenario with all required fields: learning objectives, vocabulary bounds, grammar focus, success criteria, dialog flow, Berlitz Method system prompt parameters
- Scenario selection respects the learner path: the returned scenario fits the learner's current position in the lesson sequence, building on what they have practised previously
- If multiple scenarios match, selection avoids repeating any scenario the learner has completed within their last 5 sessions. If all matching scenarios have been completed within the lookback window, the least-recently-completed scenario is selected and a `scenario_pool.exhausted` event is logged (feeds content gap tracking and OQ-5 velocity planning)
- Query response time <200ms p95 at expected MVP load (~50 concurrent sessions [~])

### Berlitz Instructor (pilot group reviewer)

**US-7: Provide structured feedback on IG content**
As a Berlitz instructor in the review pilot group, I want to receive generated IG content for my level/language, use it in real lessons, and submit structured feedback, so that the content is validated by practitioners before wider rollout.

*Acceptance criteria:*
- Instructor sees assigned content for review, filtered to their language and level expertise
- After using content in a lesson, instructor fills out a structured scorecard (aligned with the 5-dimension eval rubric: L2 immersion, correction accuracy, correction strategy, CEFR bounding, Q&A cycle adherence)
- Instructor can flag specific issues (linguistic errors, pedagogical concerns, cultural sensitivity) with inline annotations
- Review takes <10 minutes per scenario [~]
- Feedback is captured in structured format (not free-text only) so it can train the adversarial agent

### Telemetry consumer (System - feedback loop)

**US-8: Rank scenarios by learning effectiveness**
As the analytics system, I want to rank scenarios by how well they achieve their teaching/learning goal based on telemetry data, so that underperforming content is flagged for review or replacement.

*Acceptance criteria:*
- Each scenario in the Scenario Library has an effectiveness score computed from six telemetry signals:
 - **Leading (available per-session):**
   - *Scenario goal reached* - did the learner hit the scenario's defined success criteria? (binary, from `ai.scenario.goal_reached`)
   - *Session completion* - did the learner finish or bail early? (from `ai.session.ended.end_reason`)
   - *Speaking time* - did the learner speak enough? (from `ai.utterance.learner.duration_ms`)
 - **Lagging (cross-session, requires weeks of data):**
   - *Vocabulary acquisition* - did the learner use the scenario's target vocabulary correctly in subsequent sessions?
   - *Error pattern reduction* - did the grammar errors the scenario targets decrease in future sessions?
 - **Explicit:**
   - *Learner feedback* - session rating if provided (optional, low response rate expected [~])
- Leading signals are available immediately post-GA; lagging signals require >=4 weeks of data [~] before they are meaningful
- **Launch-day score** uses the three leading signals only (goal reached, completion, speaking time) as an unweighted average of normalized values. Lagging signals added once >=4 weeks of data accumulate. Weighting and computation method finalized as a Phase 3 exit criterion.
- Scenarios below a threshold (bottom 10th percentile [~] of effectiveness score, or completion rate <40% [~]) are automatically flagged for review
- Flagged scenarios appear in a "needs review" queue visible to content authors and the LX team
- At MVP, flagging is automatic but action is manual (human reviews and decides to revise, replace, or keep). Automated removal is post-MVP.
- Effectiveness scores are recomputed weekly [~] as new telemetry accumulates

---

## 7. Requirements

### Functional Requirements

| ID | Requirement | Priority | Component | Source |
|----|------------|----------|-----------|--------|
| FR-01 | System shall ingest Berlitz PDF instructor guides and student guides, extracting: lesson goals, vocabulary lists, grammar points, dialog scripts, story outlines, and exercise instructions. | P0 | A1 (PDF Ingestion) | #26; architecture A1 |
| FR-02 | System shall ingest CEFR reference specifications and extract vocabulary and grammar constraints per CEFR level (A1-C2). | P0 | A1 | Clarification Q2 |
| FR-03 | System shall ingest vocabulary-to-lesson Excel mappings and associate vocabulary items with their curriculum lesson position. | P0 | A1 | Clarification Q2 |
| FR-04 | System shall ingest lesson transcripts (text format) and extract teaching patterns: question types, correction timing, scaffolding techniques, vocabulary choices, and encouragement patterns. | P1 | A1 | Clarification Q2 |
| FR-05 | All extracted content shall be structured and tagged by: CEFR level, lesson unit/sequence position, skill type (grammar, vocabulary, pronunciation, conversation, reading, listening), and topic. | P0 | A2 (Structuring) | Architecture A2 |
| FR-06 | System shall store extracted content in a structured, queryable format (JSON/database) for downstream generation. | P0 | A2 | Architecture A2 |
| FR-07 | LLM-powered generation pipeline shall transform structured lesson content into runtime-ready scenarios: conversation scenarios, role-play scripts, pronunciation drills, and practice exercises. | P0 | A3 (Generation) | #28; architecture A3 |
| FR-08 | Each generated scenario shall include: learning objectives, vocabulary bounds, grammar focus, CEFR level, success criteria, and source material reference. | P0 | A3 | Architecture A3 |
| FR-09 | Generated scenarios shall pass automated schema validation before entering the review queue. Validation checks: all required fields present, vocabulary within CEFR level band, grammar structures within level scope, valid skill type and topic tags. | P0 | A3 | Guardrail metrics |
| FR-10 | System prompts for the AI Tutor shall encode the Berlitz Method: immersive L2 use, question-answer cycles, graduated difficulty, correction by salient prompts (not implicit recasts), and encouragement patterns. System prompts shall be generated from structured Berlitz Method rules - the rules are the single source of truth. | P0 | A4 (Method Encoding) | #13; architecture A4 |
| FR-11 | AI Tutor output constraints shall be derived from CEFR reference material and vocabulary-to-lesson mappings: vocabulary restricted to level-appropriate word lists, grammar structures bounded by level, sentence complexity and speaking speed calibrated to CEFR level. | P0 | A5 (Level Constraints) | #22; architecture A5 |
| FR-12 | Approved scenarios shall be stored in a versioned Scenario Library, tagged and filterable by CEFR level, skill type, topic, lesson unit, and status. | P0 | Scenario Library | #33 |
| FR-13 | Scenario Library shall support version history per scenario. Updates to a live scenario do not break active learner sessions. | P1 | Scenario Library | #33 |
| FR-14 | System shall ingest the learner path (lesson sequence, prerequisites, topic progression) as defined by the LX team. Generated scenarios shall reference their position in the learner path so the AI Tutor can select scenarios that build on prior learning. | P0 | A2 (Structuring) | US-6 |
| FR-15 | Content author or reviewer shall be able to review, edit, approve, or reject generated scenarios through a review interface. Two review streams: IG content routed to instructor pilot group, student-facing content routed to LX team. Rejected scenarios return to draft with reviewer notes. All edits versioned. | P0 | Review | #16 (MVP subset); US-3 |
| FR-16 | An adversarial review agent shall automatically check every generated scenario before it enters the human review queue. MVP scope: vocabulary-level check (flag >5% out-of-level vocabulary) and grammar-scope check (flag structures above tagged CEFR level). Scenarios failing the agent check are auto-rejected back to generation with flagged issues. | P0 | Review (adversarial agent) | US-4 |
| FR-17 | Every human review decision (approve/reject/edit) and the structured reason shall be captured and linked to the scenario and the adversarial agent's pre-review assessment. This builds the training dataset for future agent sophistication. | P0 | Review (data collection) | US-4 |
| FR-18 | Each scenario in the Scenario Library shall have a telemetry-derived effectiveness score based on learner session data (completion rate, speaking time, CEFR progression delta). Scenarios below threshold are automatically flagged in a "needs review" queue. | P1 | Telemetry loop | US-8 |
| FR-19 | Re-ingestion of updated source files shall detect changes and update the structured content store without full re-processing. | P1 | A1 | #26 |
| FR-20 | Generation pipeline shall support batch generation: given a curriculum unit, generate scenarios for all skill types in that unit in a single run. | P2 | A3 | US-2 |
| FR-21 | Each generated scenario shall reference the source materials it was derived from (PDF page, Excel row, transcript segment) for traceability and IP audit. | P0 | A3 | Legal/IP requirement |

### Non-Functional Requirements

| ID | Requirement | Target | Priority | Rationale |
|----|------------|--------|----------|-----------|
| NFR-01 | **Generation latency:** Time from generation trigger to draft scenario available | <5 minutes per scenario [~] | P0 | Must not bottleneck content velocity. Batch of 10 scenarios should complete in <30 minutes [~]. |
| NFR-02 | **Schema validation pass rate** | >=95% of generated scenarios pass automated validation | P0 | Reduces reviewer burden. Failed validations indicate generation quality issues. |
| NFR-03 | **Scenario Library query latency** | <200ms p95 for runtime queries from AI Tutor at expected MVP load (~50 concurrent sessions [~]) | P0 | Session start must not be blocked by slow content retrieval. (Avatar PRD US-3: <30s app-to-speaking) |
| NFR-04 | **Vocabulary bound accuracy** | >=95% of vocabulary in generated scenarios within the tagged CEFR level band | P0 | Aligned with Avatar PRD NFR-04 (Hu & Nation 2000: 95-98% known vocabulary threshold). |
| NFR-05 | **Source material traceability** | 100% of generated scenarios link back to at least one source document | P0 | Required for IP audit and Legal review. |
| NFR-06 | **Language parameterization** | Pipeline architecture supports adding a new target language by providing new source materials, without pipeline code changes | P1 | Multi-language expansion (#24) is post-MVP but the architecture must not be English-hardcoded. |
| NFR-07 | **Ingestion robustness** | PDF/Excel parse failures flagged and isolated - one bad page/sheet does not block the rest of the ingestion run | P1 | Source materials may have inconsistent formatting across editions. |
| NFR-08 | **Data isolation** | Source materials (PDFs, transcripts) and generated content stored with access controls. Lesson transcripts containing instructor/student data are access-restricted. | P0 | Transcripts contain instructor and student speech data - privacy-sensitive. See Section 9. |

---

## 8. AI Evaluation Plan

> **Berlitz Method rubric:** The 5-dimension evaluation rubric is defined in [Berlitz Method & Eval Rubric](../../product-context/berlitz-method-and-eval-rubric.md). This section specifies how the content pipeline applies it to generated scenarios.

The Curriculum Factory's generation pipeline (FR-07) is LLM-powered - the same structured input can produce different scenario outputs on each run. This section defines how we evaluate generation quality, what model capabilities are required, and how we handle failure modes.

### Evaluation methodology

**Layer 1 - Adversarial review agent (automated, run on every scenario before human review):**

1. **Schema validation** (FR-09): Every generated scenario is validated against the scenario schema. Checks: required fields present, valid tags, well-formed structure. Hard gate - failures are blocked.

2. **Vocabulary bound check** (FR-16): Automated comparison of all vocabulary against the CEFR-level word list from ingested reference material. Flags any word outside the level band + 1 level tolerance. Scenarios with >5% out-of-level vocabulary are auto-rejected.

3. **Grammar scope check** (FR-16): Automated comparison of grammar structures against CEFR-level grammar scope. Structures above tagged level are flagged.

4. **Source grounding check**: Automated verification that the scenario's objectives, vocabulary, and grammar focus trace to at least one ingested source document. Scenarios with no source grounding are flagged as potentially hallucinated.

> The adversarial agent starts basic (vocabulary + grammar + schema + grounding) but is designed to grow. Every human review decision is captured (FR-17) to build the training dataset. Post-MVP, the agent expands to check Berlitz Method compliance dimensions, trained on the accumulated review data. The goal: progressively reduce human review to flagged-only scenarios.

**Layer 2 - Human review (two-stream, run on every scenario at MVP):**

5. **Stream A - IG content via instructor pilot group**: A pilot group of ~20-50 instructors [~] (selected for review skill) receives generated IG content, uses it in real lessons, and provides structured feedback via a scorecard aligned with the 5-dimension rubric (L2 immersion, correction accuracy, correction strategy, CEFR bounding, Q&A cycle adherence). Their structured sign-off validates the content.

6. **Stream B - Student-facing content via LX team**: Micro-learning snippets, interactive practice, and learning videos are reviewed by the LX team with explicit sign-off. Instructors from the pilot group can supplement but LX owns the decision.

   **Reviewer calibration:** Before the first formal review round, all reviewers independently score a calibration set of 5 scenarios. Inter-rater agreement must reach >=70% (simple agreement on pass/fail per dimension). If below threshold, the rubric is refined and calibration repeated.

   **Reviewer pool contingency:** Calibration requires 3 reviewers. If fewer than 3 are available, minimum viable calibration is 2 reviewers with >=80% agreement. If only 1, an external Berlitz Method expert must be brought in.

**Layer 3 - QA'd recordings as ground truth:**

7. **Ground truth benchmark**: QA'd recordings of real Berlitz lessons - already scored against the Berlitz Teaching Rubric - serve as the gold standard for what good content looks like when delivered. These recordings show how CEFR level definitions + storyboarding + learner path turn into actual instructor-student interaction. They are used as:
  - **(a) Few-shot training examples** for the generation pipeline - "here is how a real Berlitz instructor teaches this A2 restaurant scenario"
  - **(b) Eval benchmark** for generated content - "does this generated scenario produce teaching interactions comparable to what we see in the QA'd recordings?"
  - **(c) Pattern mining** for Berlitz Method encoding - extracting questioning patterns, correction timing, scaffolding techniques

**Layer 4 - Telemetry-driven content ranking (post-GA):**

8. **Effectiveness scoring**: Each live scenario accumulates telemetry: session completion rate, learner speaking time, CEFR progression delta, explicit feedback. Scenarios below threshold (bottom 10th percentile [~] or completion rate <40% [~]) are auto-flagged for human review. At MVP, flagging is automatic but action is manual. Post-MVP: underperformers are auto-removed from rotation.

**Simulated learner validation (post-MVP, Q4 2026):**

9. **Simulation Engine integration**: Generated scenarios are run through the Simulation Engine (#34) with synthetic learner personas before human review. Scores pedagogical quality and catches issues schema validation cannot (confusing dialog, unreachable goals). Replaces some human review load once available.

### Eval thresholds

| Level | Schema validation | Vocabulary bounds | Method compliance | When |
|-------|------------------|-------------------|-------------------|------|
| **Launch (Phase 2 exit)** | >=90% | >=90% | >=80% (expert spot-check) | Aug 2026 |
| **GA target** | >=95% | >=95% | >=85% (expert spot-check) | Oct 2026 |
| **Aspirational** | >=98% | >=98% | >=90% (automated via Simulation Engine) | Q1 2027 |

If schema validation drops below 90% or vocabulary bounds below 90% on any generation batch, generation is paused and prompts are reviewed before resuming.

### Model capability requirements

| Capability | Requirement | Rationale |
|-----------|------------|-----------|
| Context window | >=64k tokens | Must fit: full lesson unit content (vocabulary lists, grammar rules, dialog scripts, story outlines) + CEFR level constraints + Berlitz Method rules + generation instructions + few-shot examples. A single curriculum unit's extracted content can be 10-20k tokens [~]; combined with system prompt and examples, 64k provides headroom. |
| Structured output | JSON or function-calling support | Generated scenarios must conform to a strict schema (FR-08, FR-09). Structured output avoids post-hoc parsing of free-text generation. |
| Instruction following | Reliable adherence to vocabulary bounds and format constraints | Vocabulary bound accuracy (NFR-04) depends on the model respecting explicit word-list constraints in the prompt. Models that frequently ignore constraints are not viable. |
| Multilingual fluency | Native-quality output in target language at CEFR C2 | Scenario dialog must be linguistically correct in the target language. Generation quality is the ceiling for AI Tutor output quality. |
| Cost at scale | <=$0.50 per scenario (input + output tokens) [~] | At >=50 scenarios for GA and hundreds post-GA, generation cost must be marginal relative to review time. At ~10k input tokens and ~5k output tokens per scenario, this is achievable with current model pricing [~]. |

### AI failure modes and guardrails

| Failure mode | Detection | Threshold | Action | Fallback |
|-------------|-----------|-----------|--------|----------|
| **Hallucinated vocabulary** - scenario uses words not in the CEFR level band or not present in source materials | Automated vocabulary bound check against ingested CEFR word lists | >5% of scenario vocabulary outside level band | Scenario blocked from library; returned to draft with flagged words highlighted | Content author manually replaces flagged words; if >10% of batch fails, prompt review required |
| **Fabricated teaching content** - scenario includes grammar rules, cultural claims, or factual information not grounded in source materials | Source grounding check (automated); expert review (manual) | Any scenario with 0 source document references; any factual claim flagged by reviewer | Scenario blocked; source grounding failure logged | Author verifies claims against source material or removes them; prompt updated to strengthen grounding instructions |
| **Cultural insensitivity** - scenario contains stereotypes, inappropriate role-play contexts, or culturally loaded content | Expert review (manual); post-MVP: content safety classifier | Any instance flagged by reviewer | Scenario immediately removed from library if live; escalated to content lead within 24 hours | Scenario replaced with a hand-authored alternative; generation prompt updated with negative examples |
| **Schema validation failure** - scenario missing required fields, invalid tags, or malformed structure | Automated schema validator (FR-09) | <95% pass rate per batch (GA target) | Failed scenarios returned to generation queue for retry (1 retry); if retry fails, flagged for manual authoring | Hand-authored scenario fills the gap |
| **CEFR level drift** - scenario dialog is too easy or too hard for the tagged level | Automated vocabulary/grammar complexity check; expert review | >5% of dialog turns outside level band | Scenario returned to draft; level tag adjusted or dialog regenerated | Expert manually adjusts dialog complexity |
| **Generation timeout** - LLM call exceeds time limit | Pipeline timeout monitor | >5 minutes per scenario | Retry once; if second attempt times out, log and skip | Scenario gap filled by hand-authoring or lower-priority generation |

---

## 9. Source Material Inventory

> This section documents what source materials are available. Exact counts to be confirmed during ingestion spike.

| Source Type | Format | Content | Volume | Status |
|-------------|--------|---------|--------|--------|
| Instructor guides (IG) | PDF | Lesson plans, teaching instructions, dialog scripts, grammar explanations | Extensive - multi-level [~] | Available |
| Student guides (SG) | PDF | Exercises, vocabulary, reading passages, dialog prompts | Extensive - multi-level [~] | Available |
| CEFR reference specs | PDF / structured | Vocabulary lists and grammar structures per CEFR level (A1-C2) | Complete A1-C2 [~] | Available |
| Vocabulary-to-lesson mapping | Excel (.xlsx) | Maps vocabulary items to specific lessons in the curriculum | Covers English curriculum [~] | Available |
| Lesson recordings (QA'd) | Video + audio + text transcripts | Recordings of live Berlitz lessons, individually scored as part of the QA process with a detailed rubric (not just good/bad). An existing assessment agent scores sessions and mostly agrees with human assessment - **but agent quality is unverified and needs review/testing before reliance**. Currently used mainly to rank instructors. These are **ground truth** for what good Berlitz teaching looks like - questioning patterns, correction timing, scaffolding techniques, vocabulary choices by level. Used as (a) few-shot training examples for generation, (b) eval benchmark for generated content quality, (c) pattern mining for Berlitz Method encoding. | Tens of thousands across languages and levels. Of those, some % are QA-reviewed. | Available, access-restricted. **90-day retention limit** - transcripts deleted after 90 days for privacy. Structured pattern extractions must happen within this window and persist after source deletion. |
| Learner path | Structured (defined by LX team) | The sequence of lessons a learner progresses through - what comes before and after each unit, how topics build on each other, prerequisite knowledge per scenario. This is the creative input from the LX team. The curriculum factory consumes it; it does not generate it. | To be defined per language/level [~] | Input from LX team - not yet formalised as structured data |

**Ingestion priority order:**
1. Learner path + CEFR reference specs + vocabulary Excel (establishes the skeleton: what to teach in what order, constrained by level - A5)
2. Instructor/student guide PDFs (populates lesson content - A1/A2)
3. QA'd lesson transcripts (enriches teaching patterns - A4, feeds evaluation benchmarks, provides few-shot examples for generation)

> **Note on QA'd recordings:** These recordings show us how CEFR level definitions + storyboarding + learner path turn into the material Berlitz already offers (IG, SG, interactive practice, presentation videos). They capture the actual instructor-student interaction - not just what to teach, but *how* it is taught. This is the strongest training signal for generation quality and the most credible eval benchmark.

> **Critical constraint - 90-day retention:** Because transcripts are deleted after 90 days, the ingestion pipeline (FR-04) must extract and store teaching patterns in structured form *within* the retention window. The structured extractions (teaching patterns, few-shot examples, rubric scores) persist in the content store after the source transcripts are deleted. This means ingestion is not a one-time event but a **continuous process** - new recordings arrive, get scored, get pattern-extracted, then expire. The pipeline must run regularly (at least weekly [~]) to capture value from the rolling window.

> **Existing assessment agent:** An agent already scores sessions and mostly agrees with human assessment. This is a potential starting point for the adversarial review agent (US-4), but its quality is unverified - needs review and testing before any reliance. Evaluating and potentially adapting this agent is a Phase 1 activity.

---

## 10. Privacy & Legal Constraints

| Constraint | Requirement | Owner | Deadline | Status |
|-----------|------------|-------|----------|--------|
| **IP ownership of generated content** | Legal must confirm that LLM-generated scenarios derived from Berlitz-owned source materials are Berlitz IP. Generation traceability (FR-17) supports this by linking output to source. | Legal | Sep 2026 (before Phase 3 / GA) | Open |
| **Lesson transcript consent** | Transcripts contain instructor and student speech. Legal must confirm: (a) consent was obtained for use in AI training/content generation, (b) if not, what anonymization or re-consent is required. | Legal | Jul 2026 (before transcript ingestion in Phase 1) | Open - blocks FR-04 |
| **Instructor data in transcripts** | Instructor names, teaching styles, and voice patterns may be identifiable in transcripts. Access controls required (NFR-08). Anonymization or pseudonymization before use in generation pipeline. | Legal + Engineering | Jul 2026 (before transcript ingestion) | Open |
| **Source material licensing** | Confirm Berlitz has unrestricted rights to use all PDF guides and CEFR materials for AI content generation (no third-party licensing restrictions). | Legal | Jul 2026 (before Phase 1 ingestion) | Open |

---

## 11. Launch Plan

### Phase 1: Ingestion Spike (Jul 2026)

**Objective:** Prove the pipeline can extract structured content from all four source types.

**Entry criteria:**
- Source material inventory completed (exact document counts, formats confirmed)
- Learner path for English A1-B2 available in structured format from LX team, or scope reduced to unsequenced scenarios for Phase 1 with sequencing added in Phase 3
- Legal review initiated for transcript consent, IP ownership, and source material licensing
- Manual authoring baseline established: time 2-3 scenario authoring sessions with content experts to validate the 4-8 hour baseline [~] (feeds Goal 1 velocity claim)

**Activities:**
- Build PDF parsing for instructor/student guides - extract lesson goals, vocabulary, grammar, dialogs
- Build Excel parser for vocabulary-to-lesson mapping
- Parse CEFR reference material into structured level constraints
- Prototype transcript parsing (teaching pattern extraction)
- Validate extracted content against source material (spot-check accuracy)

**Exit criteria:**
- Structured content store populated for >=3 curriculum units across A1-B1
- Extraction accuracy >=90% on spot-checked entities [~]
- CEFR vocabulary and grammar constraints loaded for A1-B2
- Legal confirmation received for source material licensing (OQ-3), or licensing risk documented and accepted by PM
- Manual authoring baseline measured and recorded (validates velocity claim)
- Total A1-B2 curriculum unit count confirmed from vocabulary-to-lesson Excel (establishes denominator for source material coverage metric)

### Phase 2: Generation Pipeline (Jul-Aug 2026)

**Objective:** Generate scenarios from structured content and validate quality.

**Entry criteria:**
- Phase 1 exit criteria met
- Berlitz Method rules documented in structured format (A4 input)

**Activities:**
- Build LLM generation pipeline: structured content in, draft scenarios out
- Implement Berlitz Method encoding in system prompts (A4)
- Implement level-appropriate language constraints (A5)
- Implement automated schema validation (FR-09) and vocabulary bound check
- Generate first batch of scenarios for avatar dogfood (5 guided + 3 role-play)
- Content expert review of generated scenarios against 5-dimension rubric
- **Generation quality iteration:** If schema validation <90% or method compliance <80%, tune prompts, adjust few-shot examples, and regenerate before exit

**Exit criteria:**
- >=8 scenarios generated and expert-approved for avatar dogfood
- Schema validation pass rate >=90%
- Vocabulary bound accuracy >=90%
- Generated scenarios pass Berlitz Method compliance expert spot-check >=80%

### Phase 3: Scenario Library & Scale (Aug-Sep 2026)

**Objective:** Build the Scenario Library and scale generation to meet avatar beta/GA requirements.

**Entry criteria:**
- Phase 2 exit criteria met
- Scenario Library storage and query API implemented (FR-12)

**Activities:**
- Populate Scenario Library with approved scenarios
- Scale generation across A1-B2 curriculum units
- Implement review interface for content experts (FR-15, lightweight)
- Integrate Scenario Library with AI Tutor session orchestrator (US-6)
- Validate runtime query latency (NFR-03)
- **Generation quality ramp:** Continue prompt tuning and few-shot example refinement to close the gap from Phase 2 exit (90%/90%/80%) to GA targets (95%/95%/85%). Run at least 3 quality-focused generation-review-tune cycles [~]. Track improvement per cycle.

**Exit criteria:**
- >=50 approved scenarios in Scenario Library across A1-B2 [~], with minimum per skill type: >=15 guided conversations, >=8 role-plays, >=10 pronunciation drills, >=10 grammar/vocabulary exercises. At least 3 of the 4 CEFR levels (A1, A2, B1, B2) must have scenarios in every skill type.
- AI Tutor successfully loads scenarios from library in <200ms
- Avatar beta (Sep 2026) has >=10 guided conversations and >=5 role-plays available
- Avatar GA (Oct 2026) has >=15 guided conversations and >=8 role-plays available
- Schema validation pass rate >=95%
- Vocabulary bound accuracy >=95%
- Berlitz Method compliance >=85% (expert spot-check)

### Success Criteria for GA

- Scenario Library meets avatar GA content requirements
- Pipeline can generate a new scenario in <5 minutes
- Schema validation pass rate >=95%
- No P0 or unresolved P1 bugs in the pipeline
- Legal review completed for IP ownership and transcript consent

### Rollback Plan

- The pipeline is offline infrastructure - it does not affect runtime if disabled
- If pipeline-generated scenarios have quality issues, fall back to hand-authored scenarios for the avatar
- Scenario Library can serve hand-authored scenarios alongside pipeline-generated ones (same schema)
- Individual scenarios can be unpublished from the library without affecting other content

---

## 12. Post-MVP Roadmap

These are scoped out of this PRD but documented as the planned evolution. **Differentiator** = builds competitive advantage post-launch (Q4 2026). **Enhancement** = deepens the moat (2027). Classification follows the architecture doc's Essential/Differentiator/Enhancement tiers.

| Phase | Feature | Issue | Timing |
|-------|---------|-------|--------|
| Differentiator | Advanced adversarial agent - expand beyond vocabulary/grammar checks to Berlitz Method compliance, trained on accumulated human review data. Target: reduce human review to flagged-only scenarios. | - | Q4 2026 |
| Differentiator | Content Pipeline Metrics (auto-approval rate, reviewer workload, time-to-publish, adversarial agent precision/recall) | #15 | Q4 2026 |
| Differentiator | Simulated learner validation (use Simulation Engine #34 to test scenarios before human review) | #34 | Q4 2026 |
| Differentiator | Automated telemetry-driven content removal (underperforming scenarios auto-pulled from rotation, not just flagged) | - | Q4 2026 |
| Enhancement | Theming / engagement skins - place abstract lesson definitions into themed environments (e.g., "Star Trek", "Game of Thrones", "The Office") to increase engagement | - | 2027 |
| Enhancement | Language-specific formality registers - Sie/Du (German), vous/tu (French), and other pragmatic rules baked into generation for non-English languages | - | 2027 |
| Enhancement | LX-agent learner path generation - AI agent proposes learner paths based on CEFR requirements, reviewed by LX team | - | 2027 |
| Enhancement | Business Content Modules (finance, healthcare, tech, legal scenarios) | #14 | 2027 |
| Enhancement | Multi-Language Expansion (Spanish, German, Japanese) | #24 | 2027 |
| Enhancement | Culture & Skills content pipeline - extends the factory to non-language content types | - | 2027+ |
| Enhancement | A/B testing of scenario variants | - | 2027 |

---

## 13. Decisions Requiring PDRs

The following cross-team, hard-to-reverse decisions are embedded in this PRD and require explicit sign-off. Once the project establishes a `decisions/` directory, each should be extracted into a standalone Product Decision Record (PDR).

| Decision | Current position in PRD | Why it needs a PDR | When |
|----------|------------------------|-------------------|------|
| **LLM-powered generation vs template-based / rule-based / hybrid** | FR-07 assumes LLM-powered generation. PDR: [`PDR-001`](../../decisions/PDR-001-content-generation-approach.md) | This determines cost structure, quality variance, evaluation complexity, and the human review workflow. Template-based generation would produce more predictable output at the cost of variety and adaptability. A hybrid (templates for structure + LLM for dialog) may be optimal. The choice is hard to reverse once the pipeline is built and content experts are trained on the workflow. | Before Phase 2 starts (Jul 2026) |

> **PDR-001 is still Open.** This PRD assumes LLM-powered generation (Option A). If the decision lands on Option B (template-based) or Option C (hybrid): the adversarial agent scope changes (templates need different checks), the cost model changes (no LLM inference cost per scenario), and eval thresholds for "hallucinated vocabulary" and "fabricated content" may need recalibration. Phase 1 (ingestion) is unaffected by the decision. **PDR-001 must be accepted before Phase 2 entry.**

---

## 14. Open Questions

| # | Question | Owner | Deadline | Status |
|---|----------|-------|----------|--------|
| 1 | **IP ownership:** Are LLM-generated scenarios derived from Berlitz source materials considered Berlitz IP? What documentation/traceability is required? | Legal | Sep 2026 | Open |
| 2 | **Transcript consent:** Do existing lesson transcripts have consent for use in AI content generation? If not, what re-consent or anonymization is required? | Legal | Jul 2026 | Open - blocks FR-04 |
| 3 | **Source material licensing:** Are there any third-party licensing restrictions on the PDF guides or CEFR reference materials that limit use in AI generation? | Legal | Jul 2026 | Open |
| 4 | **Auto-approval rate target:** Can we reach 80%+ auto-approval (pass schema validation + compliance check, skip human review)? Or must every scenario be human-reviewed at MVP? | PM + Content | After Phase 2 prototype | Open - answer after Phase 2 |
| 5 | **Steady-state content velocity:** How many new scenarios per month does the AI Tutor need post-GA to maintain content freshness and avoid learner repetition? | PM + Analytics | GA + 90 days | Open [~] - set from post-GA usage data |
| 6 | **Berlitz Method rules owner:** Who is the designated Berlitz Method expert to validate the structured compliance spec (A4)? Same open question as Avatar PRD OQ-8. | PM | Jul 2026 | Open |
| 7 | **Transcript volume and format:** Tens of thousands of recordings exist across languages and levels (video + audio + text). Some % are QA-reviewed. Exact breakdown by language/level/QA-status needs inventory. | PM + Content | Jul 2026 | Partially answered - inventory needed during Phase 1 spike |
| 8 | **Instructor guide consistency:** Are PDF guides consistently formatted across editions, or will the parser need to handle multiple layouts? | Engineering | Jul 2026 | Open - resolve during Phase 1 spike |
| 9 | **Existing assessment agent quality:** An agent exists that scores sessions and mostly agrees with human assessment. Needs review and testing: (a) what rubric dimensions does it cover? (b) what is its precision/recall vs human reviewers? (c) can it be adapted for the adversarial review agent (US-4) or is a rebuild needed? | Engineering + QA | Jul 2026 | Open - evaluate during Phase 1 |
| 10 | **QA'd recording assessment rubric detail:** What dimensions does the current QA rubric score? How does it map to the 5-dimension eval rubric in the AI Conversation Experience PRD (L2 immersion, correction accuracy, correction strategy, CEFR bounding, Q&A cycle adherence)? | PM + QA | Jul 2026 | Open - need to review the rubric (attachment pending) |
| 11 | **Instructor pilot group recruitment:** Who selects the ~20-50 pilot instructors for IG content review? What criteria define "review skill"? Is there compensation or is this part of existing duties? Note: Phase 2 review is performed by the content author team (2-5 IDs); the instructor pilot group is needed for Phase 3 / steady-state. | PM + Ops | Jul 2026 | Open |

---

## 15. Sources

### Internal
- Architecture: `engineering/design/plans/ai-tutor-architecture.md` (Layer A - Content Pipeline)
- AI Avatar PRD: `PRDs/ai-avatar/ai-avatar-prd.md` (scenario requirements, launch timeline)
- Feature matrix: `product/PRDs/feature-matrix.md`
- Competitive matrix: `competitive-research/competitors/competitive-matrix.md` (Section B: Content & Pedagogy)
- Strategic positioning: `competitive-research/strategic-positioning.md`
- GitHub issues: #26 (PDF Ingestion), #28 (Prompt/Scenario Gen), #33 (Scenario Library), #16 (Content QA), #15 (Pipeline Metrics), #14 (Business Content), #24 (Multi-Language)
- Teams: Chayan Roy on micro-lessons and course content flow (Jun 3 2026)

### Learning science
- Hu & Nation 2000 - 95-98% vocabulary comprehension threshold (applied as CEFR bounding heuristic)
- Lyster & Ranta 1997 - Corrective feedback types (informs Berlitz Method encoding)
- Krashen 1982/1985 - Comprehensible input (informs level-appropriate language constraints)
