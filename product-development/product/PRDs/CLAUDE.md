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
| `ai-tutor/ai-avatar-prd.md` | AI Avatar |
| `ai-tutor/curriculum-factory-prd.md` | Curriculum Factory |

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
