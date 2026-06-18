# PDR-001: Content Generation Approach  - LLM vs Template vs Hybrid

| Field | Value |
|-------|-------|
| **Status** | Open |
| **Author** | Jan Hoffmann, PM |
| **Created** | 2026-06-16 |
| **Decision deadline** | Jul 2026 (before Curriculum Factory Phase 2) |
| **Stakeholders** | PM, Engineering, Content Authors |
| **Related PRD** | `PRDs/curriculum-factory/curriculum-factory-prd.md` (FR-07, Section 13) |

---

## Context

The Curriculum Factory (Layer A in the AI Tutor architecture) needs a generation engine that transforms structured lesson content into runtime-ready scenarios. The PRD currently assumes LLM-powered generation (FR-07). This decision determines the cost structure, quality variance, evaluation complexity, and human review workflow for the entire content pipeline.

## Options

### Option A: LLM-powered generation

The LLM receives structured content (lesson goals, vocabulary, grammar, dialog scripts) and generates complete scenarios  - dialog flow, character roles, success criteria, correction opportunities.

| Dimension | Assessment |
|-----------|-----------|
| **Variety** | High  - LLM produces diverse dialog flows and phrasings per generation |
| **Predictability** | Low  - same input produces different output; requires evaluation framework |
| **Adaptability** | High  - new scenario types or formats require prompt changes, not code changes |
| **Cost per scenario** | ~$0.50–2.00 LLM inference [~] + review time |
| **Review burden** | High at MVP (every scenario reviewed); decreasing as auto-approval confidence grows |
| **Evaluation complexity** | High  - requires schema validation, vocabulary bounds checking, compliance scoring |
| **Time to first output** | Fast  - prompt engineering, not software engineering |

### Option B: Template-based generation

Pre-defined scenario templates with slots (vocabulary, grammar focus, topic, character names) filled from the structured content store. No LLM involved.

| Dimension | Assessment |
|-----------|-----------|
| **Variety** | Low  - output follows template patterns; learners may notice repetition |
| **Predictability** | High  - deterministic output; same input always produces same scenario |
| **Adaptability** | Low  - new scenario types require new templates (engineering work) |
| **Cost per scenario** | Near zero (compute) + template authoring time |
| **Review burden** | Low  - templates reviewed once; generated instances are predictable |
| **Evaluation complexity** | Low  - template guarantees structure; only slot-fill accuracy needs checking |
| **Time to first output** | Slow  - requires template design and authoring for each scenario type |

### Option C: Hybrid (templates for structure + LLM for dialog)

Templates define scenario structure (objectives, phases, correction opportunities). LLM generates the natural-language dialog within those structural constraints.

| Dimension | Assessment |
|-----------|-----------|
| **Variety** | Medium-high  - structural consistency with dialog variety |
| **Predictability** | Medium  - structure is deterministic; dialog varies |
| **Adaptability** | Medium  - new structures need templates; dialog adapts via prompts |
| **Cost per scenario** | ~$0.25–1.00 LLM inference [~] (smaller generation scope) + template + review |
| **Review burden** | Medium  - structure is trusted; dialog needs review |
| **Evaluation complexity** | Medium  - template enforces structure; LLM dialog still needs quality checks |
| **Time to first output** | Medium  - needs both templates and prompts |

## Evaluation criteria

| Criterion | Weight | Notes |
|-----------|--------|-------|
| Content velocity at GA (>=50 scenarios) | High | Can the approach produce enough content by Oct 2026? |
| Quality consistency | High | Does the approach meet >=85% Berlitz Method compliance reliably? |
| Review burden at scale | Medium | What's the steady-state human review cost? |
| Adaptability to new languages/skill types | Medium | How much rework for multi-language expansion? |
| Cost at scale (hundreds of scenarios) | Low | LLM costs are marginal vs. review time at current volumes |

## Recommendation

TBD  - to be decided after Phase 1 ingestion spike provides concrete data on structured content quality and volume. A short generation spike (2–3 days) comparing Options A and C on the same 5 curriculum units would provide the evidence needed.

## Decision

*Pending  - deadline Jul 2026.*
