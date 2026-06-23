# Rob x Michal — Issues Alignment — 2026-06-19
**Attendees:** Rob Zinkov, Michal Sobocinski
**Date:** 2026-06-19

## TL;DR
- Michal raised that he feels behind on context and wants to start writing code rather than attending more planning meetings.
- The team aligned on trimming the grammar exercises issue to a narrower scope (audio grammar evaluation endpoint only) and renaming it accordingly.
- Rob and Michal walked through the ADR workflow: write ADR first, open a PR for review, get a thumbs-up, then start implementation.
- Rob pointed the team to the Berlitz knowledge base (GitHub) as the glossary and auto-updated reference for all repos.

## Decisions
- Narrow the grammar exercises issue to an **audio grammar evaluation endpoint** only (backend, no mobile-side concerns).
- Rename the issue accordingly; Michal to update the body and share with Rob and Jan for review.
- ADR-first workflow confirmed: write ADR → PR → thumbs-up → implement.
- Rob will handle ADR collision risk via a lint test; no need to manually reserve number ranges.

## Action items
| Owner | Action | Status |
|-------|--------|--------|
| Michal Sobocinski | Update issue title and body (audio grammar evaluation endpoint), share link with Rob and Jan | pending |
| Michal Sobocinski | Write ADR for the audio grammar evaluation endpoint, open a PR for review | pending |
| Rob Zinkov | Clarify issue scope with Jan in the AI data group chat | pending |
| Rob Zinkov | Tag Michal on ADR PRs for a quick review | pending |
| Rob Zinkov | Merge Team OS and Knowledge Ray repos (planned for following week) | pending |

## Open questions
- Will audio transcription and grammar evaluation live in the same service or separate ones? (To be resolved in the ADR.)
- What LLM/service handles grammar evaluation — ElevenLabs for transcription was mentioned, but the evaluator isn't confirmed.
- Does Jan sign off on the narrowed issue scope, or does he have further concerns?

## Discussion

### Issue Scope and Title
Michal had been working on a GitHub issue for grammar exercises but it was too broad — it covered voice input (mobile-side concern), transcription, and grammar evaluation all in one. Jan's concern was that it read like an epic spanning multiple teams. Rob suggested narrowing it to just the backend work: an audio-only grammar evaluation endpoint. The new framing: accept audio + exercise context (target grammar pattern, CEFR level), transcribe via ElevenLabs, evaluate, return a score. Rob proposed renaming the issue from "grammar exercises" to "audio grammar evaluation endpoint."

### Issue Approval Process
Rob explained his proposal: Michal creates or refines the issue, puts it in a PR/comment, and Rob gives a quick thumbs-up before Michal starts work — not a heavyweight gate, just a "yes, this is the problem we want to solve." Rob noted Jan may have concerns about too much overlap in the original issue. Michal agreed to update the issue body with his own description (replacing the current content), change the title, and share the link with Jan and Rob.

### ADR Workflow
Michal asked about ADR numbering — he saw reserved slots and wasn't sure whether to pick 007 or skip ahead. Rob confirmed ADRs 7 and 8 are in open PRs (just pushed), and if there's a collision it can be resolved at review time. He suggested adding a lint check for duplicate numbers. Michal's plan: write the ADR, open a PR, get review, then start coding. ADRs are immutable — changes to the same topic in the future require a new ADR, not an edit.

### Service Architecture Question
Rob flagged that the acceptance criteria implied audio → text → grammar eval, suggesting two separate concerns: (1) an endpoint that evaluates grammar given text, (2) an endpoint that transcribes audio to text. Both could live in the same service, exposed as two different endpoints. Michal agreed the ADR would clarify the right structure before coding begins.

### Knowledge Base & Glossary
Michal asked about acronyms he kept encountering. Rob pointed him to the `berlitz-knowledge-base` GitHub repo, which is auto-updated and aggregates every Berlitz repo as a submodule. Cloning it lets Claude answer questions across all services. Rob noted Team OS should already be in there and plans to merge Team OS and Knowledge Ray into one repo the following week.

## Misc
- Rob mentioned the avatar service code is written but is waiting on ADR merges (ADRs 7 & 8) before moving forward.
- Meeting ended with Michal planning to start coding by the following Friday once the issue and ADR are settled.
