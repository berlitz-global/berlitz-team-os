# AI Issue Triage and Sprint Planning — 2026-06-17

**Attendees:** Rob Zinkov, Michal Sobocinski
**Date:** 2026-06-17

## TL;DR

- Rob and Michal walked through the full backlog of AI tutor issues, assigning each to a milestone (MVP, current iteration, or a future iteration).
- The current iteration landed at roughly 7 items; several were deferred or flagged as low priority or not clearly AI features.
- A key clarification: the Berlitz Method Compliance deliverable is a markdown file reviewed by language-teaching staff and stored in the repo — not an API.
- The team agreed to review the triage output with Jan before formally assigning tasks.

## Decisions

- Berlitz Method Compliance = a markdown file in the repo, not an API; effort estimate revised accordingly.
- Grammar and pronunciation drills placed in the same iteration.
- Audio clips issues removed from the AI board (not an AI feature).
- All vague issues must be rewritten to meet the clarity standard before anyone picks them up.
- Triage output to be reviewed with Jan before task assignment.

## Action items

| Owner | Action | Status |
| ----- | ------ | ------ |
| Rob Zinkov | Confirm Postman collection status at 11 AM meeting | New |
| Rob Zinkov | Remove audio clips issues from the AI board | New |
| Rob Zinkov | Scaffold open conversation / avatar issues in the repo with clear parent-child structure | New |
| Michal Sobocinski | Start on Berlitz Method Compliance markdown | New |
| Michal Sobocinski | Start on grammar exercise implementation | New |
| Michal Sobocinski | Rewrite vague backlog issues using Claude | New |
| Michal Sobocinski | Meet with mentor about LMS content access | New |

## Open questions

- Should the placement test be API-only or include a full in-app UX? (Needs Jan's input.)
- Who is the intended audience for the drill session summary feature?
- Which API key / provider should be used for the grammar exercise implementation?

## Discussion

### Avatar and open conversation overlap

The team discussed the relationship between the AI avatar feature and the open conversation feature, noting significant overlap. These were flagged for consolidation or clearer boundary definition in the issue tracker.

### AI-Assisted Lesson Prep

AI-Assisted Lesson Prep was identified as a potential dual-use feature (useful for both instructors and the curriculum factory pipeline). The team discussed scoping it carefully to avoid ambiguity.

### Video and session recording sizing

The team sized the video/session recording feature and discussed what scope belongs in MVP vs. later iterations given data storage and GDPR implications.

### Grammar and pronunciation evaluation API

The team discussed combining grammar and pronunciation evaluation into a single API endpoint. This was placed in the current iteration alongside other drills.

### Placement test scope

The placement test feature prompted a discussion about whether it should be API-only or include a full in-app UX. This was left as an open question for Jan to weigh in on.

### Berlitz Method Compliance clarification

Rob clarified that Berlitz Method Compliance is not an API — it is a markdown document that codifies the teaching methodology, reviewed and signed off by Berlitz language-teaching staff, and stored in the repo. This changes the effort estimate significantly.

### Issue clarity standard and vague issues

Rob reinforced the standard: every issue must be clear enough for a newcomer or an LLM to act on without additional context. Several backlog issues were flagged as too vague and must be rewritten (using Claude) before anyone picks them up.

### Postman collection and sprint timing

Rob flagged a pending Postman collection question to confirm at an 11 AM meeting. The team discussed sprint start timing relative to Jan's availability.
