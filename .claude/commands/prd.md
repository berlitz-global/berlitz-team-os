# PRD Writing Command

You are an expert product manager at Berlitz writing a Product Requirements Document (PRD) to the highest internal standards.

**Every claim must be grounded in evidence.** If a claim is unverified, estimated, or assumed, mark it with `[~]` inline. If an entire paragraph rests on an assumption, open it with `> **[~] Assumption:**`. Low-certainty content is acceptable - unacknowledged uncertainty is not.

---

## Phase 1: Intake

Ask the user for:

1. **Feature name** - what should this PRD be called?
2. **Product area** - which area does this fall under? (billing, deployment, prototyping, home-page, starter-templates, collaboration, enterprise, or other)
3. **One-sentence pitch** - what problem does this solve and for whom?
4. **What they already have** - do they have notes, a ticket, research, customer quotes, or a rough draft to work from? Ask them to share anything relevant before you proceed.

---

## Phase 2: Research

Before writing anything, gather evidence from the codebase. Run these lookups in parallel:

### 2a. Feature index
Read `product-development/feature-index.yaml` and search for the feature by name or area. Note any related PRDs, RFCs, plans, experiments, or tickets that already exist.

### 2b. Customer evidence
- Read `product-development/product/customers/CLAUDE.md` to understand the customer routing structure
- Search `product-development/product/customers/` for any calls or feature requests that mention the feature area
- Extract verbatim quotes with their source (customer name, call date or ticket number)

### 2c. Competitive context
- Read `product-development/product/competitive-research/CLAUDE.md`
- Check `product-development/product/competitive-research/competitors/competitive-matrix.md` for relevant feature rows
- Note which competitors have the feature, at what quality, and whether this has appeared in competitive deal feedback

### 2d. Analytics & metrics
- Read `product-development/analytics/CLAUDE.md`
- Look for any existing metrics, investigations, or experiments that establish a current-state baseline for the problem area
- Note data sources and whether figures are confirmed or estimated

### 2e. Strategy alignment
- Read `product-development/product/strategy/CLAUDE.md` and any linked roadmap
- Check whether this feature appears in current-quarter priorities or OKRs

### 2f. Existing engineering context
- Read `product-development/engineering/CLAUDE.md`
- Check for any RFCs or plans related to the feature that would inform technical considerations

After research, summarize what you found and what gaps remain. If critical evidence (customer verbatims, baseline metrics, competitive data) is missing, flag it before proceeding - do not fabricate it.

---

## Phase 3: Clarification

Based on what you found, ask the user targeted questions to fill gaps. Do not ask for information you already found in Phase 2. Focus on:

- **Business case gaps**: Is there a revenue impact estimate? A customer deal tied to this? Current metric baselines?
- **Scope boundaries**: What is explicitly out of scope for v1?
- **Open decisions**: Are there known unresolved questions (pricing, tier gating, technical constraints)?
- **Launch context**: Is there a target quarter, a specific beta customer, or a dependency on another feature?
- **Team**: Who is the engineering owner? Design owner?

Keep the question list tight - ask only what you genuinely need to write a high-quality PRD. If a piece of information is nice-to-have but you can mark it `[~]`, say so and proceed.

---

## Phase 4: Write the PRD

Write the complete PRD. Follow the structure below exactly. Use the existing PRDs as style references:
- `product-development/product/PRDs/deployment/custom-domains-prd.md` - strong business case, customer request format
- `product-development/product/PRDs/prototyping/version-history-prd.md` - strong problem statement, open questions
- `product-development/product/PRDs/home-page/project-search-prd.md` - strong success metrics with guardrails
- `product-development/product/PRDs/billing/credit-usage-dashboard-prd.md` - strong non-goals, P0/P1/P2 requirements
- `product-development/product/PRDs/starter-templates/community-marketplace-prd.md` - strong flywheel narrative

---

### PRD Structure

```
# [Feature Name] PRD

| Field | Value |
|-------|-------|
| **Author** | [Name], [Role] |
| **Status** | Draft |
| **Last Updated** | [YYYY-MM-DD] |
| **Related RFC** | [path or TBD] |
| **Related Plan** | [path or TBD] |

---

## Problem Statement

[2-4 paragraphs. Describe the problem from the user's perspective. Be specific about who is affected and how. Quantify the pain where data exists. Mark estimates with [~].]

[Structure as numbered compounding problems if there are multiple dimensions, as in version-history-prd.md.]

## Business Opportunity

[Connect the problem to business outcomes. Cover: churn impact, conversion impact, competitive positioning, and/or revenue at risk. Every figure needs a source in parentheses - e.g., "(see investigation: analytics/investigations/...)" or "(based on competitive benchmarking with X)" or "[~] estimated".]

| Business lever | Impact |
|---------------|--------|
| [lever] | [impact with source or [~]] |

## Why Now

[3-5 bullet points or numbered reasons explaining the urgency. Reference: competitive launches, customer escalation trends, infrastructure readiness, pipeline deals at risk, request volume.]

## Customer Requests

[Table of verbatim evidence. Every row must have a real source - named customer, ticket ID, call date, NPS batch, support ticket number, or Slack community post. Do not paraphrase into generic statements.]

| Source | Customer / Segment | Date | Verbatim |
|--------|-------------------|------|----------|
| [ticket / call / NPS / etc.] | [name or segment] | [date] | "[exact quote]" |

## Goals & Success Metrics

### Goals

[2-4 numbered goal statements.]

### Success Metrics

[Table. Include the current baseline where it exists. Mark estimates with [~]. Include the measurement timeframe.]

| Metric | Definition | Baseline | Target | Timeframe |
|--------|-----------|----------|--------|-----------|

### Guardrail Metrics

[Optional - include when this feature could regress a neighboring metric.]

| Metric | Definition | Threshold |
|--------|-----------|-----------|

### Non-Goals

[Optional but encouraged - list what this PRD explicitly does not cover. Reference ticket numbers for deferred scope.]

## User Stories

[One story per distinct user type / job-to-be-done. Use the "As a / I want to / So that" format. Each story must have acceptance criteria - concrete, testable, written in present tense.]

### [User Type]

**As a** [user type with context], **I want to** [action], **so that** [outcome].

**Acceptance criteria:**
- [criterion 1]
- [criterion 2]

## Requirements

### Functional Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-1 | [requirement] | P0 |

Priority guide:
- **P0** - must ship for launch; feature is broken or unusable without it
- **P1** - important but the feature ships without it
- **P2** - nice to have; consider for a follow-on

### Non-Functional Requirements

| ID | Requirement | Target | Priority |
|----|-------------|--------|----------|
| NFR-1 | [requirement] | [measurable target] | P0 |

[Cover: latency/performance, reliability, security/data isolation, accessibility, rate limiting, scale targets.]

## Launch Plan

[Three phases minimum: Internal Dogfood → Beta → GA. Each phase must have: audience, duration or timing, entry criteria / success gate.]

### Phase 1: Internal Dogfood

### Phase 2: Beta

### Phase 3: General Availability

### Success Criteria for GA

### Rollback Plan

[How to disable without a deploy. What happens to existing user data if the feature is turned off.]

## Open Questions

[Track unresolved decisions that would affect requirements or design. Every row must have an owner and a status.]

| # | Question | Owner | Status |
|---|----------|-------|--------|
| 1 | [question] | [name] | Open / Investigating / Decided: [decision] |
```

---

## Writing standards

**Evidence and sourcing:**
- Every quantitative claim needs a source: investigation file path, ticket ID, customer name + call date, or a competitive reference
- If you cannot source a figure, mark it `[~]` and note what data would confirm it
- Customer verbatims must be exact quotes, not paraphrases - if you only have a paraphrase, say so
- Ticket references use the format your team uses (e.g., `PROJ-XXXX`)

**Low-certainty markers:**
- `[~]` inline after a specific figure or statement: `"estimated 2-week reduction in sales cycle [~]"`
- Block assumption for a whole paragraph: `> **[~] Assumption:** This analysis assumes churn behavior mirrors Vercel/Netlify patterns, which has not been validated for AI Tutor's user base.`
- Open questions for unresolved decisions (not uncertain facts - use the Open Questions table for those)

**Tone and style:**
- Write for an audience of engineers, designers, and executives who were not in the room when the feature was conceived
- Lead with the user and business problem - do not open with a feature description
- Prefer concrete examples over abstract descriptions
- Avoid hedging language like "may", "could", "might" unless you also mark `[~]` - hedged claims without markers erode trust in the whole document
- Use the same terminology as defined in `product-development/product/CLAUDE.md`
- **No em dashes.** Use a regular hyphen surrounded by spaces ( - ) where a dash is needed
- **Bullets over prose.** Default to bullet points. Use prose only when narrative flow is essential (e.g., a problem statement that builds a causal chain). If a paragraph can be a list, make it a list
- **Be concise.** As short as possible, as long as necessary. Cut filler, qualifiers, and throat-clearing. Every sentence should earn its place
- **No redundancy (MECE).** Each piece of information appears exactly once in the PRD. Cost, pricing, and unit economics live in one section and are referenced elsewhere. Content blocks should be mutually exclusive and collectively exhaustive where possible

**Diff-friendly edits:**
- When fixing review findings, be diff-friendly. If a change is tiny and does not change meaning, skip it
- Insert new content cleanly and leave adjacent lines untouched so git diff shows only the real change
- Only rewrite surrounding text when the meaning has changed

**Requirements quality:**
- Each FR and NFR must be independently testable - if you cannot write a passing/failing test for it, rewrite it
- FR IDs are sequential within the PRD (FR-1, FR-2…), same for NFR
- Performance targets must be concrete: "< 200ms p95", not "fast"
- Security requirements must specify the threat they mitigate, not just the control

---

## Phase 5: Save

Once the PRD draft is written and the user has reviewed it:

1. **Determine the save path.** Use the product area to pick the right subfolder:
  - `product-development/product/PRDs/billing/`
  - `product-development/product/PRDs/deployment/`
  - `product-development/product/PRDs/prototyping/`
  - `product-development/product/PRDs/home-page/`
  - `product-development/product/PRDs/starter-templates/`
  - `product-development/product/PRDs/collaboration/` (create if needed)
  - `product-development/product/PRDs/enterprise/` (create if needed)

2. **Name the file.** Use kebab-case: `[feature-name]-prd.md`

3. **Save the file.** Write the PRD to the determined path.

4. **Update the PRDs index.** Add a row to the table in `product-development/product/PRDs/CLAUDE.md`:
   ```
   | `[area]/[feature-name]-prd.md` | [Feature Name] |
   ```

5. **Update the feature index.** Read `product-development/feature-index.yaml` and add or update the entry for this feature with the PRD path.

6. **Confirm to the user.** Output the saved file path and a one-line summary of the PRD's core hypothesis (problem → solution → expected outcome).
