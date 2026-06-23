# Tutor AI: Agent Memory, MVP Scope, and Repo Migration — 2026-06-12

**Attendees:** Rob Zinkov, Michal Sobocinski
**Date:** 2026-06-12

## TL;DR

- Michal has been exploring the codebase and prototyped a "memory mode" that injects dynamic context (past errors, vocab items) into the system prompt across sessions.
- Rob walked Michal through the broader MVP feature scope: pronunciation/vocab/grammar drills, comprehension, guided and freeform avatar conversation, lesson import, progress tracking, and teacher handoffs.
- The team agreed on a one-to-one replacement of existing Talkio AI functionality as the initial milestone, with feature development following after.
- The current experimental repo will migrate to the decided `berlitz-apps` / `berlitz-services` monorepo structure, likely the following week.

## Decisions

- One-to-one Talkio replacement first, then feature additions.
- Single source of truth for lesson/student data with ingest from existing Berlitz systems.
- Migrate to `berlitz-apps` / `berlitz-services` monorepos next week (pending CI/CD clarity).
- Python or Go for now; migrate to Rust if performance bottlenecks emerge.
- Merge Michal's memory-mode PR.
- Prefer `gh` CLI over GitHub MCP server.

## Action items

| Owner | Action | Status |
| ----- | ------ | ------ |
| Rob Zinkov | Send Michal Talkio access credentials | New |
| Rob Zinkov | Share internal lesson content API access with Michal | New |
| Rob Zinkov | Follow up with Dayon re: SSO/company login access | New |
| Rob Zinkov | Migrate experimental repo to monorepos (target: Monday) | New |
| Michal Sobocinski | Open PR for memory-mode implementation | New |
| Rob Zinkov | Merge Michal's memory-mode PR | New |

## Open questions

- Which features are MVP vs. post-MVP? (To be resolved with Jan in roadmap meeting.)
- Where will session assessment data be stored? (Rob working with Kanu.)
- Who owns CI/CD setup for the new monorepos, and on what timeline?
- What is the exact structure of the internal Berlitz lesson content API?

## Discussion

### Agent memory prototype

Michal prototyped a "memory mode" that injects dynamic context (past errors, vocabulary items) into the system prompt across sessions. Rob and Michal discussed the implementation approach and agreed to merge Michal's PR.

### MVP feature scope

Rob walked Michal through the broader MVP scope: pronunciation/vocab/grammar drills, comprehension exercises, guided and freeform avatar conversation, lesson import, progress tracking, and teacher handoffs. They agreed on a one-to-one replacement of existing Talkio AI functionality as the first milestone before adding new features.

### Data architecture and session assessment

Rob is working with Kanu on where session assessment data will be stored. The goal is a single source of truth for lesson/student data with ingest from existing Berlitz systems.

### Live Avatar architecture and provider flexibility

They discussed Live Avatar architecture and the need to keep provider choices (Tavus, LiveKit, etc.) swappable. Rob is exploring LiveKit for on-device audio/video handling.

### Monorepo migration

The current experimental repo will migrate to `berlitz-apps` / `berlitz-services` monorepos, targeting the following Monday, pending CI/CD clarity with Dayon.

### Backend language and tooling

They settled on Python or Go for now, with a plan to migrate to Rust if performance bottlenecks emerge. Rob prefers the `gh` CLI over the GitHub MCP server for issue management.
