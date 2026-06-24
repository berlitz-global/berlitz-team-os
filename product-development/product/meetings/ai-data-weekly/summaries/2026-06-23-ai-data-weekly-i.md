# AI + Data Weekly I: Architecture Review and Grammar Evaluator Demo — 2026-06-23

**Attendees:** Jan Hoffmann, Rob Zinkov, Michal Sobocinski
**Date:** 2026-06-23

## TL;DR

- Jan walked the team through an architecture diagram on Microsoft Whiteboard, covering the full learner-path stack from LMS through front end. Key MVP scoping decisions were made for learner path (static), level assessment (looks like a lesson), and TTS (always-on).
- LMS ownership is unresolved: no one has made the buy-vs.-build decision or assigned it to a team. Rob to raise in standup.
- Michal demoed a working grammar evaluator (STT output + target pattern + CEFR level → correction + score + level feedback) using OpenRouter/Gemma 4; Jan was impressed by out-of-the-box quality.
- Two spikes proposed: (1) investigate current lesson audio-input evaluation behavior; (2) front-end speech caching for static content.

## Decisions

- MVP learner path: static fixed sequence; progress is a bookmark (no SRS/branching for MVP).
- Level assessment should be designed to feel like a fun first lesson, not a formal test; treat it architecturally as the first lesson a learner takes.
- TTS is always-on: every piece of text shown to a learner should also be spoken (Berlitz method core); mobile app team implements the UI, AI Data team provides the TTS API endpoint.
- Static lesson audio should be pre-generated at content publish time rather than called live per-session (reduce LLM cost); spike needed to evaluate caching approach.
- Grammar evaluator prototype uses OpenRouter (Gemma 4) for CEFR-aware evaluation; direction is sound, but Berlitz-specific vocabulary/grammar guidelines should be added to system prompts.
- Front end is primarily Mobile app team's responsibility; AI Data team's boundary is the TTS endpoint.

## Action items

| Owner | Action | Status |
| ----- | ------ | ------ |
| Rob Zinkov | Raise LMS ownership question in standup — who is building the next LMS and is it buy or build? | New |
| Rob Zinkov | Send Michal the API key needed for grammar evaluator testing | New |
| Rob Zinkov | Complete protocol/sequence diagram (owed to Jan, Srikant, and Knut) | New |
| Jan Hoffmann | Send Michal a calendar invite for the follow-up session at 11:00 (was missed) | New |
| Jan Hoffmann | Paste LMS architecture diagram into group chat (it disappeared from the repo) | New |
| Michal Sobocinski | Create Jira spike: investigate current lesson audio-input evaluation behavior (wrong-answer acceptance bug, latency) | New |
| Jan / Michal | Create spike for front-end speech caching: evaluate pre-generation at publish vs. LLM prompt caching | New |

## Open questions

- Who owns the LMS build, and has the buy-vs.-build decision been made? Does Learner App team (Knut's group) think the Curriculum Factory replaces the LMS, or are they expecting a separate system?
- What is the right audio caching strategy: pre-generate all static audio at publish time, or rely on LLM token-level caching?
- How should pronunciation correction be scoped: always-on background monitoring vs. explicit pronunciation drills only? At what CEFR levels should active correction kick in?
- Can the existing OPT (Online Placement Test, levels 1–8) be extended with a speaking component affordably, or should the AI Tutor's level assessment replace it entirely?
- Should Berlitz's CEFR-level vocabulary and grammar guidelines (Nicolas's Excel content) be added as context to the grammar evaluator prompt?

## Discussion

### Architecture diagram walkthrough

Jan shared a Microsoft Whiteboard diagram covering the main layers of the AI Tutor stack. The diagram uses yellow to flag components the team must own. Key components reviewed: curriculum factory (content source), LMS (TBD), learner path and progress ("lesson taking loop"), level assessment, front end/presentation layer, and the evaluation/feedback services. Rob suggested renaming "main loop" to "Lesson Taking Loop" to be more descriptive.

### LMS ownership: unresolved buy-vs.-build

The team has no clarity on who is building the next LMS or whether the decision has been made to build at all. Michal noted that Knut asked whether the Curriculum Factory would split out the authoring and progress-tracking functions that currently sit inside the LMS as one system. Rob's working assumption had been that the team would eventually build a minimal LMS as part of the AI Tutor platform. Rob committed to raising this in his standup to get a clearer answer.

### MVP learner path and level assessment

For MVP, the learner path is a fixed static sequence; progress is stored as a bookmark. No dynamic branching or SRS for MVP. Level assessment has historically been a 20–40 minute session with a human tutor, which doesn't scale. Jan's view: it should feel like a fun onboarding game (Duolingo-style), not a test, and as a byproduct the system learns the learner's level. Rob proposed treating it architecturally as the first lesson. The existing OPT covers levels 1–8 for reading/listening but lacks speaking; Japan attempted to add a paid speaking component but never deployed it due to per-test cost.

### TTS, audio caching, and front-end boundary

The Berlitz method requires everything to be spoken: all text shown to a learner should also be read aloud; learners always respond by speaking, never typing. The AI Data team's responsibility in the front-end layer is to provide a TTS API endpoint; the Mobile app team owns the UI. Michal raised that calling a TTS API live on every lesson load is expensive. Proposed solution: pre-generate audio for all static content during the curriculum factory publish pipeline and serve cached files. A spike is needed to compare pre-generation vs. LLM prompt caching.

### Grammar evaluator demo (Michal)

Michal demoed a working grammar evaluator. Inputs: STT-transcribed user response, target pattern from the lesson content, user's CEFR level. Output (JSON): correct/not, score, correction, explanation, level-appropriateness feedback. Implemented with OpenRouter using Gemma 4 (free tier). The LLM already understands CEFR levels out of the box. Jan's reaction: "Holy crap, that is already crazy good." Next steps: add Berlitz-specific vocabulary and grammar expectations to the system prompt (Nicolas's Excel content is a candidate source), and integrate the speech-to-text layer once Rob provides an API key. Rob emphasized pronunciation evaluation must operate on raw audio, not on STT output.

### Current lesson demo and audio-input evaluation bug

Jan demoed the current production lesson in the portal. Observed issues: no TTS on exercise text (learner must read silently), a recording latency at the start of each utterance, and a multiple-choice evaluation bug where the system accepted a clearly incorrect answer by mapping the STT transcript to the nearest option regardless of correctness. Michal will create a Jira spike to investigate how the current audio evaluation works and why it behaves this way.

### New team member

A new engineer joins July 1st. Rob and Srikant have both worked with them previously; Jan has not met them.
