# Berlitz Team OS - Agent Instructions

Instructions for any AI agent working in this repository.

## Purpose

This repo is the operating system for the Berlitz AI Tutor product team. It contains product documentation, PRDs, engineering plans, analytics artifacts, design docs, customer insights, and team onboarding guides. There is no application code here.

## Finding artifacts

**Always check `product-development/feature-index.yaml` first** when looking for artifacts related to a specific feature. It maps every feature to its PRDs, design docs, plans, schemas, experiments, and tickets.

For broader orientation, see the doc index in `CLAUDE.md`.

## Writing style

Apply to every file you add or edit:

- No em dashes. Use a hyphen, a comma, or a new sentence.
- No filler. Lead with the instruction. Cut hedging, throat-clearing, and decorative adjectives.
- Imperative voice. "Run X.", not "You may want to run X."
- Concrete and verifiable. Name real files and paths.
- Scannable structure. Prefer bullets and tables over paragraphs.
- Match the voice of the surrounding file.

## Planning

- When you produce a plan, also save it to the plans/ folder of the respective folder as a dated markdown file.

## Research Standards

Apply to every research task (competitive analysis, market research, customer insights, technology evaluation).

### Source Attribution

- Every factual claim must cite its source inline: `[Source Name](URL)` or `(Source: document name, date)`.
- No uncited claims. If a source cannot be identified, mark the claim `(Unverified - needs source)`.
- Prefer primary sources (company websites, SEC filings, press releases, official docs) over secondary (blog posts, news aggregators).

### Multi-Source Verification (Triangulation)

- Verify key findings with multiple independent sources where possible.
- Tag each finding with a confidence level:
  - **High confidence** = 2+ independent sources agree, or confirmed from a primary source (company website, SEC filing, press release)
  - **Medium confidence** = 1 credible source (reputable publication, industry report)
  - **Low confidence** = unverified, estimated, or single non-authoritative source (flag for review, do not use for decisions without verification)
- Independent means different organizations or authors. Three articles citing the same press release count as 1 source.
- When confidence is Medium or Low, state this explicitly so the reader knows.

### Research Output Format

Every research document must include:

1. **Sources section** at the bottom listing all sources used, with URLs and access dates.
2. **Confidence summary** table showing which findings are high/medium/low confidence.
3. **Methodology note** (1-2 sentences) describing how the research was conducted.

### When Using Web Search

- Run at least 3 separate searches with varied queries to avoid single-source bias.
- Cross-check claims across results before including them.
- Include the source URL for every fact pulled from search results.
- If search results conflict, report the conflict rather than picking one silently.

## Before you commit

- Every file or path referenced in changed files resolves.
- No em dashes, and the writing style above is followed.
