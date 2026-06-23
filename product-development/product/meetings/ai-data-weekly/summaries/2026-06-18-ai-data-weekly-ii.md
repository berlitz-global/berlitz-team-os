# AI + Data Weekly II: MVP Scope, Roadmap Review, and Architecture Diagram — 2026-06-18

**Attendees:** Jan Hoffmann, Rob Zinkov, Michal Sobocinski
**Date:** 2026-06-18

## TL;DR

- The team reviewed the GitHub project board and current roadmap priorities, which appear broadly reasonable.
- Jan raised a concern that without a component-level architecture diagram, the MVP issue list cannot be verified as complete.
- MVP was defined as: download app, sign up, onboard, and complete 1–2 lessons — with the avatar grounded in actual lesson content, not free-form conversation.
- Rob committed to producing a Mermaid architecture diagram (stored in Team OS repo) as his top priority.

## Decisions

- MVP scope: download → sign up → onboard → complete 1–2 lessons (avatar grounded in lesson content).
- Tablet and web are post-MVP.
- New purpose-built content API, not Moodle.
- Architecture diagram to be produced before further roadmap validation.

## Action items

| Owner | Action | Status |
| ----- | ------ | ------ |
| Rob Zinkov | Create Mermaid architecture block diagram (Team OS repo) | New |
| Jan Hoffmann | Commit PRDs to repo | New |
| Jan Hoffmann | Schedule Srikant alignment session | New |
| Jan Hoffmann | Review and agree on ticket structure with Michal, then share with Rob | New |
| Michal Sobocinski | Review and agree on ticket structure with Jan, then share with Rob | New |
| Rob Zinkov | Identify Moodle stakeholders for new LMS requirements conversation | New |

## Open questions

- Are there MVP components missing from the issue list that the architecture diagram will reveal?
- What is the migration path and timeline for sunsetting myBerlitz?

## Discussion

### Roadmap review

The team walked through the GitHub project board and current roadmap priorities. The overall structure appeared reasonable, but Jan noted that without a component-level architecture diagram it's hard to confirm the issue list is complete — unknown unknowns may be missing.

### MVP definition

MVP was scoped narrowly: a user can download the app, sign up, onboard, and complete 1–2 lessons. The avatar experience should be grounded in actual lesson content rather than free-form conversation. Tablet and web support are explicitly post-MVP.

### Content pipeline and LMS architecture

The team debated the content/LMS architecture. The decision is to build a new purpose-built content API rather than use Moodle. The new system is not Moodle-based; human-authored content will be used for the first four MVP lessons. myBerlitz is to be sunset over time.

### Project tracking structure

The team discussed using multiple GitHub milestones to track work across the MVP and beyond. Jan and Michal to align on ticket structure before sharing with Rob.

### Architecture diagram

Rob committed to creating a Mermaid architecture block diagram (to live in the Team OS repo) as his top priority, to unblock Jan's ability to verify MVP issue completeness.
