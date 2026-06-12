# Competitive Analysis Plan - Berlitz AI Tutor

**Created:** 2026-06-04
**Status:** Complete

## Context

Berlitz is building an AI-powered avatar for language learning as a confirmed product feature. The competitive research structure in the repo exists but is empty, and the feature matrix uses dev-tool dimensions (UI component quality, CI/CD, Git integrations) that must be replaced entirely with language-learning dimensions. This analysis serves both feature prioritization for the Sep 2026 MVP and strategic positioning for internal alignment.

---

## Competitors (12)

Research for each competitor must capture: estimated active users, revenue/ARR (or funding if private), market segments (B2B/B2C/B2G), strongest regions, and explicit end-user pricing.

| # | Competitor | Type | Market | Why included |
|---|-----------|------|--------|-------------|
| 1 | Duolingo | Incumbent | B2C, B2B | Market leader; best gamification; free benchmark |
| 2 | Babbel | Incumbent | B2C, B2B | Strong in Europe; subscription model |
| 3 | Italki | Marketplace | B2C | Largest human-tutor marketplace; no AI |
| 4 | Preply | Marketplace | B2C, B2B | Growing AI; Preply Business; closest hybrid |
| 5 | Rosetta Stone | Legacy | B2B, B2C, B2G | Enterprise/government contracts; displacement opportunity |
| 6 | Busuu | Incumbent | B2C, B2B | McGraw-Hill backed; CEFR certification |
| 7 | Speak | AI-native | B2C | OpenAI-backed; dominant in Korea; strong speech tech |
| 8 | ELSA | AI-native | B2C, B2B | Best-in-class pronunciation AI; ELSA for Organizations |
| 9 | Praktika | AI-native | B2C | AI avatar conversations - most direct avatar competitor |
| 10 | TalkPal | AI-native | B2C | GPT-powered conversation; multi-modal; fast-growing |
| 11 | Lingoda | Hybrid | B2C | Live group + 1:1 at scale; Sprint model; CEFR cert |
| 12 | EF English Live | Enterprise hybrid | B2B, B2C, B2G | Direct enterprise competitor; live teachers + self-study |

---

## Feature Taxonomy (10 categories, 73 features)

### 0. Company Overview (per competitor, not scored)
Est. Active Users (MAU), Est. Revenue/ARR, Funding/Market Cap, Founded, HQ, Employees, Market Segments (B2C/B2B/B2G), Strongest Regions, Languages Offered (count)

### A. AI Capabilities (11)
Conversational AI, AI Avatar/Visual Agent, Speech Recognition (ASR), Pronunciation Feedback, Accent Training, Grammar Correction, Adaptive Learning/Personalization, AI Role-Play/Simulation, Writing Assistance, Real-Time Translation, LLM Foundation

### B. Content & Pedagogy (8)
CEFR Alignment, Structured Curriculum, Languages Offered, Business Content, Cultural Content, Skills Beyond Language, Content Freshness, Lesson Variety

### C. Speech & Pronunciation Technology (5)
Real-Time Voice Interaction, TTS Quality, Phoneme-Level Scoring, Shadowing/Repeat-After-Me, Conversation Recording & Playback

### D. Assessment & Progress (5)
Placement Test, Progress Dashboard, Pre/Post Assessment, Certification, Learning Analytics

### E. Engagement & Gamification (6)
Streaks/Daily Goals, Leaderboards, Rewards/Points, Achievements/Badges, Social Features, Push Notifications/Reminders

### F. Platform & Delivery (6)
iOS App, Android App, Web App, Offline Mode, Wearable/Smart Speaker, Multi-Device Sync

### G. Human Teacher Integration (6)
1:1 Live Tutoring, Group Classes, Teacher Marketplace, AI-Human Handoff, Teacher Quality Assurance, Teacher-Learner Continuity

### H. Enterprise/B2B Features (14)
Admin Dashboard, Team Progress Reports, ROI Measurement, SSO/SAML, SCIM Provisioning, HRIS Integration, LMS/LTI Integration, Custom Content/Branding, Compliance Training, Seat/License Management, Data Residency/Privacy, Dedicated Account Management, API Access, SLA Guarantees

### I. Monetization Model (6)
Free Tier, Consumer Pricing, Enterprise Pricing, Credit/Token System, Family/Team Plan, Money-Back Guarantee

---

## Execution Plan

### Phase 1: Foundation (update index files + replace matrix)

**Replace entirely:**
- `competitors/competitive-matrix.md` - new 9-category matrix with 13 columns (Berlitz + 12 competitors), empty cells

**Update in place:**
- `competitors/CLAUDE.md` - replace Audit Dimensions table with 9 language-learning categories; fill Competitor Index with all 12
- `competitive-research/CLAUDE.md` - fill Competitors table with all 12 entries

### Phase 2: Per-Competitor Research (web search + write profiles)

For each competitor, create `{slug}/CLAUDE.md`, `{slug}/tldr.md`, `{slug}/pricing.md`.

**Research priority order:**
1. Praktika (most direct avatar competitor)
2. Speak (best-funded AI-native)
3. Preply (closest hybrid - identified in business-info.md)
4. Duolingo (market leader, free-tier benchmark)
5. ELSA (speech tech leader)
6. EF English Live (enterprise competitor)
7. TalkPal (fast-growing AI wrapper)
8. Babbel, Busuu, Lingoda, Rosetta Stone, Italki

### Phase 3: Matrix Population

Fill all cells in `competitive-matrix.md` from the per-competitor research. Score the Summary Scorecard (1-5 per category). Write Key Competitive Gaps section.

### Phase 4: Strategic Positioning

Create `strategic-positioning.md` with landscape map, differentiation analysis, persona-based threats, and MVP prioritization.

### Phase 5: Finalize Indexes

Update all CLAUDE.md files with positioning dimensions and key takeaways.

### Phase 6: Source Attribution & Verification (added 2026-06-04)

Re-research all competitor profiles to comply with AGENTS.md Research Standards:

1. Every factual claim cites its source inline with URL or document reference.
2. Every research doc includes a Sources section (URLs + access dates), Confidence Summary table, and Methodology note.
3. Key findings verified by 2+ independent sources where possible (High confidence). Single-source findings tagged Medium. Estimates and unverified claims tagged Low.
4. Web searches use 3+ varied queries per competitor to avoid single-source bias.
5. Conflicting data points are reported rather than silently resolved.
6. `competitive-matrix.md` Company Overview updated with sourced data; Berlitz column renamed to "Berlitz (Target)".

**Priority order (AI-native first):**
1. ~~Speak~~ DONE (2026-06-05) - tldr.md, pricing.md rewritten with sources
2. ~~Praktika~~ DONE (2026-06-05) - tldr.md, pricing.md rewritten with sources
3. ~~ELSA~~ DONE (2026-06-05) - tldr.md, pricing.md rewritten with sources
4. ~~TalkPal~~ DONE (2026-06-05) - tldr.md, pricing.md rewritten with sources; HQ corrected (Israel -> Wilmington, DE), languages updated (57 -> 84+)
5. ~~Jumpspeak~~ DONE (2026-06-05) - tldr.md, pricing.md rewritten with sources
6. ~~competitive-matrix.md~~ DONE (2026-06-05) - Berlitz column renamed to "Berlitz (Target)", Company Overview data updated
7. ~~Remaining competitors~~ DONE (2026-06-05):
   - ~~Duolingo~~ DONE - tldr.md, pricing.md rewritten with sources
   - ~~Babbel~~ DONE - tldr.md, pricing.md rewritten with sources
   - ~~Preply~~ DONE - tldr.md, pricing.md rewritten with sources
   - ~~Italki~~ DONE - tldr.md, pricing.md rewritten with sources
   - ~~Rosetta Stone~~ DONE - tldr.md, pricing.md rewritten with sources
   - ~~Busuu~~ DONE - tldr.md, pricing.md rewritten with sources
   - ~~Lingoda~~ DONE - tldr.md, pricing.md rewritten with sources
   - ~~EF English Live~~ DONE - tldr.md, pricing.md rewritten with sources
8. ~~All pricing.md comparison tables~~ DONE (2026-06-05) - "Berlitz" renamed to "Berlitz (Target)" in all 13 pricing.md files
9. ~~competitive-matrix.md Sources section~~ DONE (2026-06-05) - per-competitor sources table added
10. ~~strategic-positioning.md Sources section~~ DONE (2026-06-05) - sources and methodology added

---

## Files to Create/Modify

| Action | Count | Files |
|--------|-------|-------|
| Replace | 1 | `competitors/competitive-matrix.md` |
| Update | 2 | `competitive-research/CLAUDE.md`, `competitors/CLAUDE.md` |
| Create | 37 | 12 competitors x 3 files each + `strategic-positioning.md` |

All paths under `product-development/product/competitive-research/`.

---

## Key Source Files

- `product-development/product/strategy/business-context/berlitz-business-info.md` - existing competitor notes, pricing, delivery model
- `product-development/product/strategy/business-context/berlitz-jtbd-and-users.md` - personas for "threats by persona" section
- `product-development/product/strategy/vision/berlitz-platform-vision.md` - AI strategy layers for Berlitz column
- `product-development/product/strategy/roadmaps/berlitz-2026-2027-roadmap.md` - MVP timeline for prioritization

---

## Verification

- Every competitor folder has `CLAUDE.md`, `tldr.md`, `pricing.md`
- Every `tldr.md` has company profile (users, revenue, funding, regions, market segments)
- Every `pricing.md` has explicit end-user costs with worked examples
- `competitive-matrix.md` Company Overview table populated for all 13 competitors
- `competitive-matrix.md` scored features have no empty cells (67 scored features x 14 columns)
- Summary Scorecard fully scored (9 categories, excludes Company Overview)
- `strategic-positioning.md` references all 5 personas and links features to MVP timeline
- All file paths in CLAUDE.md indexes resolve to real files
- No em dashes in any file
- Every `tldr.md` and `pricing.md` has inline source citations, a Sources section, a Confidence Summary, and a Methodology note (per AGENTS.md Research Standards)
