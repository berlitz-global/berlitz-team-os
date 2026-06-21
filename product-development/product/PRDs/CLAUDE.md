# PRDs

## Purpose

Product Requirement Documents for AI Tutor features.

---

## Template

Start from [`_prd-template.md`](_prd-template.md) — the house-style PRD template (metadata block, problem statement, business opportunity, why now, customer requests, goals & success metrics, user stories, requirements, launch plan, open questions). Copy it to the right area folder and fill it in.

## Naming Convention

```
[feature-name]-prd.md
```

---

## Current PRDs

PRDs are organized by product area:

| PRD | Feature |
|-----|---------|
| `curriculum-factory/curriculum-factory-prd.md` | Curriculum Factory (content pipeline) |
| `ai-conversation/ai-conversation-prd.md` | AI Conversation Experience (guided conversation + role-play, audio & avatar modes) |
| `practice-drills/practice-drills-prd.md` | Practice Drills (pronunciation, vocabulary, grammar drills + Wordbook) |
| `ai-avatar/ai-avatar-prd.md` | AI Avatar Experience (visual delivery mode for conversation) |

---

## Shared References

PRDs reference these shared docs rather than restating common content inline. Each is the single source of truth for its topic:

| Reference | Path | Used by |
|-----------|------|---------|
| Personas & Tiers | `product-context/personas-and-tiers.md` | All PRDs |
| Berlitz Method & Eval Rubric | `product-context/berlitz-method-and-eval-rubric.md` | Conversation, Curriculum Factory |
| Cost Model Summary | `product-context/cost-model-summary.md` | Conversation, Avatar, Drills |
| Privacy & Data Requirements | `product-context/privacy-and-data-requirements.md` | Conversation, Drills, Avatar |
| Instrumentation Schema | `product-context/instrumentation-schema.md` | Conversation, Drills, Avatar |
| Content Taxonomy | `product-context/content-taxonomy.md` | All PRDs |

---

## Creating New PRDs

Use the `/prd` command to create new PRDs. The command will:
1. Research existing context (customers, competitive data, analytics)
2. Guide you through required sections
3. Format to Berlitz standards

---

## PRD Template Sections

See [`_prd-template.md`](_prd-template.md) for the full template with inline guidance. Structure:

1. **Metadata block** — author, status, last updated, related RFC/plan
2. **Overview** (optional) — one-paragraph what/who/why
3. **Problem Statement** — numbered, compounding problems from the user's perspective
4. **Business Opportunity** — churn/conversion/revenue impact + lever table (flywheel if applicable)
5. **Why Now** — urgency: competitive, request volume, pipeline, readiness
6. **Customer Requests** — verbatim quotes with real sources
7. **Goals & Success Metrics** — goals, metrics (baseline/target/timeframe), guardrails, non-goals
8. **User Stories** — As a / I want / so that + testable acceptance criteria
9. **Requirements** — Functional (P0/P1/P2) and Non-Functional (concrete targets)
10. **Launch Plan** — Dogfood → Beta → GA, success criteria, rollback, feature flags
11. **Open Questions** — table with owner + status

Conventions: ground every number in a source; mark estimates `[~]`; make each requirement independently testable.
