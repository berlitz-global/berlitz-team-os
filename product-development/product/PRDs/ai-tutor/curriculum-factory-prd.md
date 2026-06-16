# Curriculum Factory PRD

| Field | Value |
|-------|-------|
| **Author** | Jan Hoffmann, PM |
| **Status** | Draft |
| **Last Updated** | 2026-06-16 |
| **Related RFC** | TBD — see Section 13 (Decisions Requiring PDRs) |
| **Related Plan** | `engineering/design/plans/ai-tutor-architecture.md` (Layer A) |
| **Epic** | [#39 — Content Pipeline](https://github.com/berlitz-global/berlitz-services/issues/39) |
| **Child Issues** | [#26](https://github.com/berlitz-global/berlitz-services/issues/26) PDF Ingestion, [#28](https://github.com/berlitz-global/berlitz-services/issues/28) Prompt/Scenario Generation, [#33](https://github.com/berlitz-global/berlitz-services/issues/33) Scenario Library |

---

## Overview

The Curriculum Factory is the offline content pipeline that transforms Berlitz's pedagogical source materials into AI-ready scenarios for the AI Tutor. It ingests four types of source material — PDF instructor/student guides, CEFR reference specifications, vocabulary-to-lesson mappings (Excel), and real lesson transcripts — structures them, and uses LLM-powered generation to produce conversation scenarios, pronunciation drills, role-play scripts, and practice exercises. The output feeds the Scenario Library consumed by the AI Tutor at runtime.

This PRD covers the **MVP pipeline** (architecture components A1–A5): ingestion, structuring, generation, Berlitz Method encoding, and level-appropriate language constraints. Content QA review workflow (#16), pipeline metrics (#15), business content modules (#14), and multi-language expansion (#24) are post-MVP.

---

## 1. Problem Statement

1. **Berlitz has 140 years of pedagogical IP locked in static formats.** Instructor guides, student guides, CEFR reference material, vocabulary mappings, and lesson transcripts exist as PDFs, Excel files, and audio/text transcripts. None of this material is machine-readable or queryable. The AI Tutor cannot use any of it without manual extraction and reformatting. Every scenario created today is hand-authored from scratch — the existing curriculum is effectively invisible to the AI system. (architecture doc, Layer A)

2. **Hand-authored scenarios do not scale.** The AI Avatar PRD requires 5 guided conversations and 3 role-plays by Aug 2026 (dogfood), 15 guided conversations and 8 role-plays by Oct 2026 (GA), spanning CEFR levels A1–B2. Hand-authoring each scenario takes hours of instructional design time [~]. At steady state, the AI Tutor needs hundreds of scenarios across levels, skill types, and topics to avoid learner repetition and maintain engagement. Manual creation cannot reach this volume at acceptable cost or speed. (AI Avatar PRD, Section 9)

3. **Without structured content, the AI Tutor cannot enforce the Berlitz Method or respect CEFR bounds.** The AI Tutor's system prompts need vocabulary lists, grammar scoping, lesson objectives, and dialog patterns drawn from the Berlitz curriculum — not generic LLM knowledge. If the Tutor generates content from its own training data rather than Berlitz-specific material, it will drift from the Berlitz Method and produce level-inappropriate output. The content pipeline is what makes the AI Tutor a *Berlitz* tutor rather than a generic language chatbot. (architecture doc, A4–A5; competitive-matrix.md, Section B)

4. **Berlitz's richest pedagogical asset — real lesson transcripts — is untapped.** Transcripts of live face-to-face lessons capture how expert Berlitz instructors actually teach: their questioning patterns, correction timing, scaffolding techniques, and vocabulary choices by level. This is ground truth for what good Berlitz teaching looks like. Today, these transcripts sit unused. The Curriculum Factory can mine them for teaching patterns that inform scenario generation and evaluation rubrics. (architecture doc, Section 5) *Note: transcript ingestion is P1, not P0, because legal consent must be confirmed before processing — see Section 9.*

---

## 2. Business Opportunity

### Strategic positioning

The competitive matrix (Section B: Content & Pedagogy) shows Berlitz targeting **5/5 on Structured Curriculum** — the highest score of any competitor, tied only with Duolingo, Babbel, and Lingoda. But unlike those competitors, Berlitz has a proprietary teaching methodology and 140 years of structured curriculum materials. The Curriculum Factory is what converts that historical advantage into an AI-native moat. (competitive-matrix.md)

> **[~] Assumption:** No AI-native competitor (Speak, Praktika, TalkPal, ELSA) has a structured content pipeline grounded in proprietary pedagogical IP. Their content is either LLM-generated from generic training data or manually authored. This is inferred from public product analysis — no competitor has disclosed their content pipeline architecture.

### Competitive differentiation

The architecture doc states: "This is where Berlitz's 140-year content advantage becomes a defensible AI moat." The reasoning:

- **AI-native competitors** (Speak 5/5 AI, Praktika 5/5 avatar) have strong technology but score 2–4/5 on Structured Curriculum and 1–2/5 on CEFR Alignment. They lack deep pedagogical content. (competitive-matrix.md)
- **Legacy competitors** (Rosetta Stone, Babbel, Lingoda) have structured content but score 1–2/5 on AI Capabilities. They lack the technology to use it dynamically.
- **Berlitz's play** is to combine both: deep content + strong AI. The Curriculum Factory is the bridge.

### Business levers

| Business lever | Impact |
|---------------|--------|
| Content velocity | Pipeline batch-generates scenarios ~8–16x faster than manual authoring [~]. Baseline: ~4–8 hours per scenario manually. Target: <30 min per scenario including validation. Batch generation amplifies this further — 10 scenarios in <30 min vs. 40–80 hours manual [~]. |
| Berlitz Method enforcement | Scenarios generated from Berlitz source material and constrained by Berlitz Method encoding are structurally compliant — not relying solely on LLM system prompts at runtime. (architecture doc, A4) |
| CEFR precision | Vocabulary and grammar constraints drawn from CEFR reference material and the vocabulary-to-lesson Excel mapping, not LLM approximations. Enables the >=95% known-vocabulary target in the Avatar PRD (NFR-04). |
| Competitive moat | Competitors cannot replicate Berlitz's source materials. Even if they build similar pipelines, they lack the input corpus. |
| Multi-language path | An English-first pipeline designed for language parameterization reduces marginal cost of expanding to Spanish, German, Japanese (post-MVP, #24). [~] |
| Cost reduction | Replaces manual instructional design labor for scenario creation. Cost per scenario drops from hours of expert time to ~$0.50–2.00 LLM inference cost [~] + 15–30 min review time [~]. |

---

## 3. Why Now

1. **The AI Avatar launches Sep 2026 and needs scenarios to teach with.** The avatar is a conversation engine without content of its own. Without the Curriculum Factory, every scenario is hand-authored, creating a bottleneck that limits the avatar's launch scope and post-launch freshness. (AI Avatar PRD, Phase 1–3)

2. **Initial scenarios will be hand-crafted; the pipeline must take over before GA.** Dogfood (Aug 2026) can ship with hand-authored scenarios. But GA (Oct 2026) needs 15+ guided conversations and 8+ role-plays across A1–B2, and post-GA growth requires a continuous content supply. The pipeline must be producing validated scenarios by Sep 2026 to feed GA. (AI Avatar PRD, Section 9)

3. **Berlitz's content advantage is perishable.** AI-native competitors are generating content from LLMs at scale. As general-purpose LLMs improve at language teaching, the quality gap between generic and Berlitz-specific content narrows. The window to establish a structured content pipeline grounded in proprietary IP — before competitors close the gap with pure AI — is now. (strategic-positioning.md)

4. **Source material inventory is complete.** Four source types are available today: PDF instructor/student guides (extensive, multi-level), CEFR reference specifications, vocabulary-to-lesson Excel mappings, and real lesson transcripts. No new content needs to be created before the pipeline can start ingesting.

5. **The Simulation Engine (#34) and Berlitz Method Compliance (#13) depend on pipeline output.** Both require structured scenarios with annotated learning objectives, vocabulary bounds, and grammar focus to function. The pipeline's structured output is their input. Delaying the pipeline delays the entire evaluation framework.

---

## 4. Customer Requests

> All entries below are internal signals. No customer call transcripts exist for the content pipeline specifically. The pipeline is infrastructure — learners experience its output (scenarios) rather than the pipeline itself.

| Source | Customer / Segment | Date | Verbatim |
|--------|-------------------|------|----------|
| Teams message | Chayan Roy / Internal Engineering | Jun 3 2026 | "Raised question on MVP scope for micro-lessons and how existing course content flows into AI avatar practice" [~] (paraphrase) |
| Architecture doc | Internal / Engineering | Jun 7 2026 | "Berlitz's pedagogical IP (PDF instructor/student guides) feeds a Content Pipeline that generates AI-usable scenarios" — identified as Essential MVP |
| AI Avatar PRD | Internal / Product | Jun 16 2026 | Avatar launch plan gates on scenario availability: 5 guided + 3 role-play for dogfood, scaling to 15+8 for GA |
| Competitive analysis | Market signal | Jun 2026 | Berlitz targets 5/5 on Structured Curriculum; no AI-native competitor exceeds 4/5. The gap is closable — urgency to formalize the content advantage. |

**Learner evidence plan:**
- **Owner:** PM
- **Deadline:** Post-GA (Dec 2026)
- **Scope:** Analyze scenario completion rates, learner feedback, and CEFR progression data to validate that pipeline-generated content performs comparably to hand-authored content.
- **Output:** Quality comparison report; findings feed back into pipeline tuning.

---

## 5. Goals & Success Metrics

### Users

**Content Author (Instructional Designer / Berlitz Method Expert):** The primary user of the pipeline. Today, content authors manually write scenarios from scratch by reading PDF guides and applying their knowledge of the Berlitz Method and CEFR levels. They are experienced language teaching professionals — typically 5+ years of Berlitz Method experience [~]. There are approximately 2–5 people in this role at launch [~]. Their current workflow is: read PDF guide → mentally map to CEFR level → write scenario in a document → peer review → hand off to engineering for integration. The pipeline replaces the "read → write" steps with "ingest → generate → review."

### Goals

1. **Build a repeatable pipeline that converts Berlitz source materials into AI-ready scenarios at 8–16x the speed of manual authoring** [~].
2. **Produce enough validated scenarios to meet the AI Avatar launch requirements** — 15 guided conversations and 8 role-plays across A1–B2 by GA (Oct 2026).
3. **Ensure every generated scenario is grounded in Berlitz curriculum** — vocabulary, grammar, and teaching patterns drawn from source materials, not generic LLM knowledge.
4. **Design the pipeline for language parameterization** so that multi-language expansion (post-MVP) requires new source material input, not a pipeline rebuild.

### Success Metrics

| Metric | Definition | Baseline | Target | Timeframe | Measurement |
|--------|-----------|----------|--------|-----------|-------------|
| Scenario generation time | Elapsed time from generation trigger to draft scenario ready for review | Manual: ~4-8 hours per scenario [~] | <30 minutes per scenario (generation + basic validation) [~] | Pipeline v1 | Pipeline log: timestamp delta between `generation.started` and `generation.completed` events per scenario |
| Scenario volume | Total scenarios in the Scenario Library, tagged and ready for the AI Tutor | 0 (hand-authored scenarios tracked separately) | >=50 scenarios (guided + role-play + drills) across A1–B2 [~] | GA (Oct 2026) | Scenario Library query: COUNT where status = approved |
| Source material coverage | % of Berlitz English curriculum units with at least one generated scenario | 0% | >=60% of A1–B2 curriculum units [~] | GA + 90 days | Scenario Library query: COUNT DISTINCT curriculum_unit / total curriculum units (total from vocabulary-to-lesson Excel) |
| Schema validation pass rate | % of generated scenarios that pass automated schema validation (required fields, CEFR tagging, vocabulary bounds) before entering review | N/A | >=95% | Pipeline v1 | Automated: schema validator output logged per generation run. COUNT(pass) / COUNT(total) |
| Berlitz Method alignment | % of generated scenarios that pass Berlitz Method compliance checks when avatar delivers them in a simulated session | N/A | >=85% [~] | GA | Expert spot-check at MVP: 3 reviewers score a random sample of 20 scenarios [~] against the 5-dimension rubric from Avatar PRD Section 8. Post-MVP (Q4 2026): automated via Simulation Engine #34. |

### Guardrail Metrics

| Metric | Definition | Threshold | Breach action |
|--------|-----------|-----------|---------------|
| Vocabulary bound violation rate | % of generated scenario avatar utterances containing vocabulary above the tagged CEFR level | <5% (aligned with Avatar PRD NFR-04: >=95% within level band) | Scenario blocked from Scenario Library; returned to draft. If >10% of a generation batch exceeds threshold, generation pipeline paused for prompt review. |
| Factual/cultural error rate | % of scenarios flagged by reviewers for factual inaccuracy or cultural insensitivity | <2% [~] | Flagged scenario immediately removed from library if live; escalated to content lead. If >5% of reviewed scenarios are flagged in a batch, batch generation suspended pending prompt and source material review. |
| Pipeline-generated vs hand-authored quality delta | Learner session completion rate for pipeline-generated scenarios minus hand-authored scenarios | No statistically significant negative delta (measured post-GA) | If delta is negative and significant (p<0.05, n>=100 sessions per group), pipeline-generated scenarios flagged for quality audit. PM reviews and adjusts generation prompts or source material selection. |

### Non-Goals

- **Content QA review workflow** (#16) — post-MVP. MVP uses a lightweight review process (expert spot-check); the full queue/approve/reject workflow ships Q4 2026.
- **Content Pipeline Metrics dashboard** (#15) — post-MVP. MVP tracks metrics manually or via basic queries.
- **Business Content Modules** (#14) — post-MVP. MVP covers general English curriculum only; industry-specific content (finance, healthcare, tech, legal) follows.
- **Multi-Language Expansion** (#24) — post-MVP. Pipeline is English-first but designed for language parameterization.
- **Learner feedback loop into content ranking** — post-MVP. The pipeline will eventually rank content by learner ratings and learning progress data, but v1 does not include this feedback mechanism.
- **Automated content generation without human review** — not a goal at any phase. The pipeline generates drafts; humans validate. "AI Suggests. Humans Decide." (architecture doc, A6)

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
- Re-ingestion of updated source files detects changes (diff) rather than re-processing from scratch

**US-2: Generate scenarios from structured content**
As a content author, I want to trigger scenario generation for a specific curriculum unit and CEFR level, so that I get draft conversation scenarios, role-play scripts, and drill exercises grounded in Berlitz material.

*Acceptance criteria:*
- Author selects: target CEFR level, curriculum unit, skill type (conversation/role-play/pronunciation/grammar/vocabulary), and topic
- System generates one or more draft scenarios using the structured content for that unit
- Each generated scenario includes: learning objectives, vocabulary bounds, grammar focus, success criteria, dialog flow, and CEFR level tag
- Generated scenarios reference the source material they were derived from (traceability)
- Generation completes in <5 minutes per scenario [~]

**US-3: Review and approve generated content**
As a content author, I want to review each generated scenario, edit it if needed, and approve or reject it, so that only validated content enters the Scenario Library.

*Acceptance criteria:*
- Author can view the generated scenario alongside the source material it was derived from
- Author can edit any field (dialog, vocabulary, objectives, level tag)
- Author can approve (promotes to Scenario Library) or reject (returns to draft with notes)
- All edits are versioned and auditable
- Rejected scenarios include author notes explaining the rejection reason

**US-4: Browse and query the Scenario Library**
As a content author, I want to search and filter the Scenario Library by CEFR level, skill type, topic, and curriculum unit, so that I can see what content exists and identify gaps.

*Acceptance criteria:*
- Filter by: CEFR level, skill type, topic, lesson unit, status (draft/approved/live)
- Search by keyword across scenario text
- Gap view: curriculum units with no approved scenarios are visually flagged

### AI Tutor (System — runtime consumer)

**US-5: Load scenario at session start**
As the AI Tutor session orchestrator, I want to query the Scenario Library for an approved scenario matching the learner's CEFR level, curriculum position, and session type, so that I can initialize a session with the right content.

*Acceptance criteria:*
- Query accepts: CEFR level, skill type, topic preference (optional), curriculum position
- Returns an approved scenario with all required fields: learning objectives, vocabulary bounds, grammar focus, success criteria, dialog flow, Berlitz Method system prompt parameters
- If multiple scenarios match, selection avoids repeating any scenario the learner has completed within their last 5 sessions (or all available scenarios if fewer than 5 exist for the query parameters)
- Query response time <200ms [~]

### Berlitz Teacher (idle-time reviewer — post-MVP extension)

**US-6: Review content during idle time**
As a Berlitz teacher with a no-show gap, I want to review and rate generated scenarios from a review queue on my device, so that I contribute to content quality without dedicated review sessions.

*Acceptance criteria:*
- Teacher sees a queue of scenarios pending review, filtered to their language and level expertise
- Teacher can approve, flag issues, or suggest edits
- Review takes <5 minutes per scenario
- Teacher reviews are weighted by their expertise level and contribute to the approval decision

> **Note:** US-6 is a post-MVP extension. MVP review is done by designated content experts only.

---

## 7. Requirements

### Functional Requirements

| ID | Requirement | Priority | Component | Source |
|----|------------|----------|-----------|--------|
| FR-01 | System shall ingest Berlitz PDF instructor guides and student guides, extracting: lesson goals, vocabulary lists, grammar points, dialog scripts, story outlines, and exercise instructions. | P0 | A1 (PDF Ingestion) | #26; architecture A1 |
| FR-02 | System shall ingest CEFR reference specifications and extract vocabulary and grammar constraints per CEFR level (A1–C2). | P0 | A1 | Clarification Q2 |
| FR-03 | System shall ingest vocabulary-to-lesson Excel mappings and associate vocabulary items with their curriculum lesson position. | P0 | A1 | Clarification Q2 |
| FR-04 | System shall ingest lesson transcripts (text format) and extract teaching patterns: question types, correction timing, scaffolding techniques, vocabulary choices, and encouragement patterns. | P1 | A1 | Clarification Q2 |
| FR-05 | All extracted content shall be structured and tagged by: CEFR level, lesson unit/sequence position, skill type (grammar, vocabulary, pronunciation, conversation, reading, listening), and topic. | P0 | A2 (Structuring) | Architecture A2 |
| FR-06 | System shall store extracted content in a structured, queryable format (JSON/database) for downstream generation. | P0 | A2 | Architecture A2 |
| FR-07 | LLM-powered generation pipeline shall transform structured lesson content into runtime-ready scenarios: conversation scenarios, role-play scripts, pronunciation drills, and practice exercises. | P0 | A3 (Generation) | #28; architecture A3 |
| FR-08 | Each generated scenario shall include: learning objectives, vocabulary bounds, grammar focus, CEFR level, success criteria, and source material reference. | P0 | A3 | Architecture A3 |
| FR-09 | Generated scenarios shall pass automated schema validation before entering the review queue. Validation checks: all required fields present, vocabulary within CEFR level band, grammar structures within level scope, valid skill type and topic tags. | P0 | A3 | Guardrail metrics |
| FR-10 | System prompts for the AI Tutor shall encode the Berlitz Method: immersive L2 use, question-answer cycles, graduated difficulty, correction by salient prompts (not implicit recasts), and encouragement patterns. System prompts shall be generated from structured Berlitz Method rules — the rules are the single source of truth. | P0 | A4 (Method Encoding) | #13; architecture A4 |
| FR-11 | AI Tutor output constraints shall be derived from CEFR reference material and vocabulary-to-lesson mappings: vocabulary restricted to level-appropriate word lists, grammar structures bounded by level, sentence complexity and speaking speed calibrated to CEFR level. | P0 | A5 (Level Constraints) | #22; architecture A5 |
| FR-12 | Approved scenarios shall be stored in a versioned Scenario Library, tagged and filterable by CEFR level, skill type, topic, lesson unit, and status. | P0 | Scenario Library | #33 |
| FR-13 | Scenario Library shall support version history per scenario. Updates to a live scenario do not break active learner sessions. | P1 | Scenario Library | #33 |
| FR-14 | Content author shall be able to review, edit, approve, or reject generated scenarios through a review interface. Rejected scenarios return to draft with reviewer notes. All edits versioned. | P1 | Review (lightweight) | #16 (lightweight MVP subset) |
| FR-15 | Re-ingestion of updated source files shall detect changes and update the structured content store without full re-processing. | P1 | A1 | #26 |
| FR-16 | Generation pipeline shall support batch generation: given a curriculum unit, generate scenarios for all skill types in that unit in a single run. | P2 | A3 | US-2 |
| FR-17 | Each generated scenario shall reference the source materials it was derived from (PDF page, Excel row, transcript segment) for traceability and IP audit. | P0 | A3 | Legal/IP requirement |

### Non-Functional Requirements

| ID | Requirement | Target | Priority | Rationale |
|----|------------|--------|----------|-----------|
| NFR-01 | **Generation latency:** Time from generation trigger to draft scenario available | <5 minutes per scenario [~] | P0 | Must not bottleneck content velocity. Batch of 10 scenarios should complete in <30 minutes [~]. |
| NFR-02 | **Schema validation pass rate** | >=95% of generated scenarios pass automated validation | P0 | Reduces reviewer burden. Failed validations indicate generation quality issues. |
| NFR-03 | **Scenario Library query latency** | <200ms p95 for runtime queries from AI Tutor | P0 | Session start must not be blocked by slow content retrieval. (Avatar PRD US-3: <30s app-to-speaking) |
| NFR-04 | **Vocabulary bound accuracy** | >=95% of vocabulary in generated scenarios within the tagged CEFR level band | P0 | Aligned with Avatar PRD NFR-04 (Hu & Nation 2000: 95–98% known vocabulary threshold). |
| NFR-05 | **Source material traceability** | 100% of generated scenarios link back to at least one source document | P0 | Required for IP audit and Legal review. |
| NFR-06 | **Language parameterization** | Pipeline architecture supports adding a new target language by providing new source materials, without pipeline code changes | P1 | Multi-language expansion (#24) is post-MVP but the architecture must not be English-hardcoded. |
| NFR-07 | **Ingestion robustness** | PDF/Excel parse failures flagged and isolated — one bad page/sheet does not block the rest of the ingestion run | P1 | Source materials may have inconsistent formatting across editions. |
| NFR-08 | **Data isolation** | Source materials (PDFs, transcripts) and generated content stored with access controls. Lesson transcripts containing instructor/student data are access-restricted. | P0 | Transcripts contain instructor and student speech data — privacy-sensitive. See Section 9. |

---

## 8. AI Evaluation Plan

The Curriculum Factory's generation pipeline (FR-07) is LLM-powered — the same structured input can produce different scenario outputs on each run. This section defines how we evaluate generation quality, what model capabilities are required, and how we handle failure modes.

### Evaluation methodology

**Automated checks (run on every generation batch):**

1. **Schema validation** (FR-09): Every generated scenario is validated against the scenario schema before it enters the review queue. Checks: required fields present, vocabulary within CEFR level band, grammar structures within level, valid tags. This is a hard gate — failures are blocked.

2. **Vocabulary bound check**: Automated comparison of all vocabulary in the generated scenario against the CEFR-level word list from the ingested reference material. Flags any word outside the level band + 1 level tolerance.

3. **Source grounding check**: Automated verification that the scenario's learning objectives, vocabulary, and grammar focus can be traced to at least one ingested source document. Scenarios with no source grounding are flagged as potentially hallucinated content.

**Expert review (run on every scenario at MVP):**

4. **Berlitz Method compliance spot-check**: Content expert scores each scenario against the 5-dimension rubric from the Avatar PRD Section 8 (L2 immersion, correction strategy, CEFR bounding, Q&A cycle adherence, encouragement ratio). At MVP, every scenario is reviewed. Post-MVP, review shifts to a sample as auto-approval confidence grows.

**Simulated learner validation (post-MVP, Q4 2026):**

5. **Simulation Engine integration**: Generated scenarios are run through the Simulation Engine (#34) with synthetic learner personas before human review. The simulation scores pedagogical quality and catches issues that schema validation cannot (e.g., confusing dialog flow, unreachable scenario goals). This replaces some human review load once available.

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
| Context window | >=64k tokens | Must fit: full lesson unit content (vocabulary lists, grammar rules, dialog scripts, story outlines) + CEFR level constraints + Berlitz Method rules + generation instructions + few-shot examples. A single curriculum unit's extracted content can be 10–20k tokens [~]; combined with system prompt and examples, 64k provides headroom. |
| Structured output | JSON or function-calling support | Generated scenarios must conform to a strict schema (FR-08, FR-09). Structured output avoids post-hoc parsing of free-text generation. |
| Instruction following | Reliable adherence to vocabulary bounds and format constraints | Vocabulary bound accuracy (NFR-04) depends on the model respecting explicit word-list constraints in the prompt. Models that frequently ignore constraints are not viable. |
| Multilingual fluency | Native-quality output in target language at CEFR C2 | Scenario dialog must be linguistically correct in the target language. Generation quality is the ceiling for AI Tutor output quality. |
| Cost at scale | <=$0.50 per scenario (input + output tokens) [~] | At >=50 scenarios for GA and hundreds post-GA, generation cost must be marginal relative to review time. At ~10k input tokens and ~5k output tokens per scenario, this is achievable with current model pricing [~]. |

### AI failure modes and guardrails

| Failure mode | Detection | Threshold | Action | Fallback |
|-------------|-----------|-----------|--------|----------|
| **Hallucinated vocabulary** — scenario uses words not in the CEFR level band or not present in source materials | Automated vocabulary bound check against ingested CEFR word lists | >5% of scenario vocabulary outside level band | Scenario blocked from library; returned to draft with flagged words highlighted | Content author manually replaces flagged words; if >10% of batch fails, prompt review required |
| **Fabricated teaching content** — scenario includes grammar rules, cultural claims, or factual information not grounded in source materials | Source grounding check (automated); expert review (manual) | Any scenario with 0 source document references; any factual claim flagged by reviewer | Scenario blocked; source grounding failure logged | Author verifies claims against source material or removes them; prompt updated to strengthen grounding instructions |
| **Cultural insensitivity** — scenario contains stereotypes, inappropriate role-play contexts, or culturally loaded content | Expert review (manual); post-MVP: content safety classifier | Any instance flagged by reviewer | Scenario immediately removed from library if live; escalated to content lead within 24 hours | Scenario replaced with a hand-authored alternative; generation prompt updated with negative examples |
| **Schema validation failure** — scenario missing required fields, invalid tags, or malformed structure | Automated schema validator (FR-09) | <95% pass rate per batch (GA target) | Failed scenarios returned to generation queue for retry (1 retry); if retry fails, flagged for manual authoring | Hand-authored scenario fills the gap |
| **CEFR level drift** — scenario dialog is too easy or too hard for the tagged level | Automated vocabulary/grammar complexity check; expert review | >5% of dialog turns outside level band | Scenario returned to draft; level tag adjusted or dialog regenerated | Expert manually adjusts dialog complexity |
| **Generation timeout** — LLM call exceeds time limit | Pipeline timeout monitor | >5 minutes per scenario | Retry once; if second attempt times out, log and skip | Scenario gap filled by hand-authoring or lower-priority generation |

---

## 9. Source Material Inventory

> This section documents what source materials are available. Exact counts to be confirmed during ingestion spike.

| Source Type | Format | Content | Volume | Status |
|-------------|--------|---------|--------|--------|
| Instructor guides | PDF | Lesson plans, teaching instructions, dialog scripts, grammar explanations | Extensive — multi-level [~] | Available |
| Student guides | PDF | Exercises, vocabulary, reading passages, dialog prompts | Extensive — multi-level [~] | Available |
| CEFR reference specs | PDF / structured | Vocabulary lists and grammar structures per CEFR level (A1–C2) | Complete A1–C2 [~] | Available |
| Vocabulary-to-lesson mapping | Excel (.xlsx) | Maps vocabulary items to specific lessons in the curriculum | Covers English curriculum [~] | Available |
| Lesson transcripts | Text / audio | Transcripts of live face-to-face lessons by Berlitz instructors | Unknown volume [~] — needs inventory | Available, access-restricted |

**Ingestion priority order:**
1. CEFR reference specs + vocabulary Excel (establishes level constraints — A5)
2. Instructor/student guide PDFs (populates lesson content — A1/A2)
3. Lesson transcripts (enriches teaching patterns — A4, feeds evaluation)

---

## 10. Privacy & Legal Constraints

| Constraint | Requirement | Owner | Deadline | Status |
|-----------|------------|-------|----------|--------|
| **IP ownership of generated content** | Legal must confirm that LLM-generated scenarios derived from Berlitz-owned source materials are Berlitz IP. Generation traceability (FR-17) supports this by linking output to source. | Legal | Sep 2026 (before Phase 3 / GA) | Open |
| **Lesson transcript consent** | Transcripts contain instructor and student speech. Legal must confirm: (a) consent was obtained for use in AI training/content generation, (b) if not, what anonymization or re-consent is required. | Legal | Jul 2026 (before transcript ingestion in Phase 1) | Open — blocks FR-04 |
| **Instructor data in transcripts** | Instructor names, teaching styles, and voice patterns may be identifiable in transcripts. Access controls required (NFR-08). Anonymization or pseudonymization before use in generation pipeline. | Legal + Engineering | Jul 2026 (before transcript ingestion) | Open |
| **Source material licensing** | Confirm Berlitz has unrestricted rights to use all PDF guides and CEFR materials for AI content generation (no third-party licensing restrictions). | Legal | Jul 2026 (before Phase 1 ingestion) | Open |

---

## 11. Launch Plan

### Phase 1: Ingestion Spike (Jul 2026)

**Objective:** Prove the pipeline can extract structured content from all four source types.

**Entry criteria:**
- Source material inventory completed (exact document counts, formats confirmed)
- Legal review initiated for transcript consent and IP ownership

**Activities:**
- Build PDF parsing for instructor/student guides — extract lesson goals, vocabulary, grammar, dialogs
- Build Excel parser for vocabulary-to-lesson mapping
- Parse CEFR reference material into structured level constraints
- Prototype transcript parsing (teaching pattern extraction)
- Validate extracted content against source material (spot-check accuracy)

**Exit criteria:**
- Structured content store populated for >=3 curriculum units across A1–B1
- Extraction accuracy >=90% on spot-checked entities [~]
- CEFR vocabulary and grammar constraints loaded for A1–B2

### Phase 2: Generation Pipeline (Jul–Aug 2026)

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

### Phase 3: Scenario Library & Scale (Aug–Sep 2026)

**Objective:** Build the Scenario Library and scale generation to meet avatar beta/GA requirements.

**Entry criteria:**
- Phase 2 exit criteria met
- Scenario Library storage and query API implemented (FR-12)

**Activities:**
- Populate Scenario Library with approved scenarios
- Scale generation across A1–B2 curriculum units
- Implement review interface for content experts (FR-14, lightweight)
- Integrate Scenario Library with AI Tutor session orchestrator (US-5)
- Validate runtime query latency (NFR-03)
- **Generation quality ramp:** Continue prompt tuning and few-shot example refinement to close the gap from Phase 2 exit (90%/90%/80%) to GA targets (95%/95%/85%). Run at least 3 quality-focused generation-review-tune cycles [~]. Track improvement per cycle.

**Exit criteria:**
- >=50 approved scenarios in Scenario Library across A1–B2 [~]
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

- The pipeline is offline infrastructure — it does not affect runtime if disabled
- If pipeline-generated scenarios have quality issues, fall back to hand-authored scenarios for the avatar
- Scenario Library can serve hand-authored scenarios alongside pipeline-generated ones (same schema)
- Individual scenarios can be unpublished from the library without affecting other content

---

## 12. Post-MVP Roadmap

These are scoped out of this PRD but documented as the planned evolution:

| Phase | Feature | Issue | Timing |
|-------|---------|-------|--------|
| Differentiator | Full Content QA review workflow (queue, approve/reject, reviewer roles) | #16 | Q4 2026 |
| Differentiator | Teacher idle-time review (teachers review content during no-show gaps) | — | Q4 2026 |
| Differentiator | Content Pipeline Metrics (auto-approval rate, reviewer workload, time-to-publish) | #15 | Q4 2026 |
| Differentiator | Simulated learner validation (use Simulation Engine #34 to test scenarios before human review) | #34 | Q4 2026 |
| Enhancement | Learner feedback loop (rank content by explicit feedback + learning progress data) | — | 2027 |
| Enhancement | Business Content Modules (finance, healthcare, tech, legal scenarios) | #14 | 2027 |
| Enhancement | Multi-Language Expansion (Spanish, German, Japanese) | #24 | 2027 |
| Enhancement | A/B testing of scenario variants | — | 2027 |

---

## 13. Decisions Requiring PDRs

The following cross-team, hard-to-reverse decisions are embedded in this PRD and require explicit sign-off. Once the project establishes a `decisions/` directory, each should be extracted into a standalone Product Decision Record (PDR).

| Decision | Current position in PRD | Why it needs a PDR | When |
|----------|------------------------|-------------------|------|
| **LLM-powered generation vs template-based / rule-based / hybrid** | FR-07 assumes LLM-powered generation. | This determines cost structure, quality variance, evaluation complexity, and the human review workflow. Template-based generation would produce more predictable output at the cost of variety and adaptability. A hybrid (templates for structure + LLM for dialog) may be optimal. The choice is hard to reverse once the pipeline is built and content experts are trained on the workflow. | Before Phase 2 starts (Jul 2026) |

---

## 14. Open Questions

| # | Question | Owner | Deadline | Status |
|---|----------|-------|----------|--------|
| 1 | **IP ownership:** Are LLM-generated scenarios derived from Berlitz source materials considered Berlitz IP? What documentation/traceability is required? | Legal | Sep 2026 | Open |
| 2 | **Transcript consent:** Do existing lesson transcripts have consent for use in AI content generation? If not, what re-consent or anonymization is required? | Legal | Jul 2026 | Open — blocks FR-04 |
| 3 | **Source material licensing:** Are there any third-party licensing restrictions on the PDF guides or CEFR reference materials that limit use in AI generation? | Legal | Jul 2026 | Open |
| 4 | **Auto-approval rate target:** Can we reach 80%+ auto-approval (pass schema validation + compliance check, skip human review)? Or must every scenario be human-reviewed at MVP? | PM + Content | After Phase 2 prototype | Open — answer after Phase 2 |
| 5 | **Steady-state content velocity:** How many new scenarios per month does the AI Tutor need post-GA to maintain content freshness and avoid learner repetition? | PM + Analytics | GA + 90 days | Open [~] — set from post-GA usage data |
| 6 | **Berlitz Method rules owner:** Who is the designated Berlitz Method expert to validate the structured compliance spec (A4)? Same open question as Avatar PRD OQ-8. | PM | Jul 2026 | Open |
| 7 | **Transcript volume and format:** How many lesson transcripts exist? Are they text or audio? What languages and levels do they cover? | PM + Content | Jul 2026 | Open — resolve during Phase 1 spike |
| 8 | **Instructor guide consistency:** Are PDF guides consistently formatted across editions, or will the parser need to handle multiple layouts? | Engineering | Jul 2026 | Open — resolve during Phase 1 spike |

---

## 15. Sources

### Internal
- Architecture: `engineering/design/plans/ai-tutor-architecture.md` (Layer A — Content Pipeline)
- AI Avatar PRD: `PRDs/ai-tutor/ai-avatar-prd.md` (scenario requirements, launch timeline)
- Feature matrix: `engineering/design/plans/feature-matrix.md`
- Competitive matrix: `competitive-research/competitors/competitive-matrix.md` (Section B: Content & Pedagogy)
- Strategic positioning: `competitive-research/strategic-positioning.md`
- GitHub issues: #26 (PDF Ingestion), #28 (Prompt/Scenario Gen), #33 (Scenario Library), #16 (Content QA), #15 (Pipeline Metrics), #14 (Business Content), #24 (Multi-Language)
- Teams: Chayan Roy on micro-lessons and course content flow (Jun 3 2026)

### Learning science
- Hu & Nation 2000 — 95–98% vocabulary comprehension threshold (applied as CEFR bounding heuristic)
- Lyster & Ranta 1997 — Corrective feedback types (informs Berlitz Method encoding)
- Krashen 1982/1985 — Comprehensible input (informs level-appropriate language constraints)
