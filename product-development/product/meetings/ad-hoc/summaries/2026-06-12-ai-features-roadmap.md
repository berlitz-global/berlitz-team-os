# AI Features Roadmap and Avatar Tutor Planning — 2026-06-12

**Attendees:** Jan Hoffmann, Rob Zinkov, Michal Sobocinski
**Date:** 2026-06-12

## TL;DR

- The team reviewed the AI avatar/tutor feature scope, distinguishing MVP (minimum working learning experience in the mobile app) from a full competitive launch feature set.
- Priority is clear: get the AI tutor plugged into the mobile app first; replacing myBerlitz is secondary and may not happen at all.
- Rob will create GitHub issues tagged by milestone by end of day or start of next week; first sprint plan targeted for early the following week.
- Michal will connect with Andres Mora about the LMS and reach out to Nicolas Potel (LX team lead) to obtain lesson content and Talkio avatar configuration exports.

## Decisions

- Primary milestone: AI tutor plugged into the mobile app; myBerlitz replacement is secondary and non-blocking.
- Use the bring-your-own (non-fully-managed) Talkio avatar tier to preserve dialect and persona control.
- Twice-weekly team syncs going forward.
- First sprint plan to be ready early the following week.

## Action items

| Owner | Action | Status |
| ----- | ------ | ------ |
| Rob Zinkov | Share prompts spreadsheet with Michal | New |
| Rob Zinkov | Create GitHub issues tagged by milestone | New |
| Rob Zinkov | Produce cost estimates for Jan | New |
| Michal Sobocinski | Meet with Andres Mora about LMS content access | New |
| Michal Sobocinski | Reach out to Nicolas Potel (LX team lead) for lesson content and Talkio avatar config exports | New |
| Jan Hoffmann | Arrange twice-weekly sync cadence | New |

## Open questions

- What is the long-term fate of myBerlitz — sunset, parallel operation, or handoff?
- How will student profile data be surfaced in the mobile app?
- What Talkio metadata (persona configs, dialect settings) is exportable and in what format?
- Should microservices be written in Python, Go, or Rust? (Deferred pending performance data.)

## Discussion

### Cost model concerns

Jan raised a concern that the cost figures in the board presentation appear unreliable. The team agreed not to anchor planning on those numbers without verification.

### Platform strategy: AI services as API endpoints

Rob articulated the platform strategy: build AI capabilities as standalone API endpoints rather than deep LMS integrations. Content will be extracted from the LMS (read-only pull), not tightly coupled to it. The AI tutor will be embedded in the self-serve learning path for now.

### Primary milestone vs. myBerlitz replacement

The primary milestone is an AI tutor experience that plugs into the mobile app. Replacing myBerlitz is a secondary concern and may not happen at all — the team agreed not to let it distract from the core AI tutor work.

### Talkio feature parity walkthrough

The team walked through Talkio's current feature set as a baseline for parity: TTS/STT, speech rate control, AI responses, vocabulary exercises, session tracking, and pronunciation assessment. Pronunciation assessment was identified as a net-new capability Berlitz would need to build. The team decided to use the bring-your-own (non-fully-managed) Talkio avatar tier to preserve dialect and persona control.

### Longer-term features

After MVP, the team discussed a roadmap of longer-term features: voice cloning, lesson authoring tools, teacher and lesson evaluation, personalization, and cross-session memory.

### GitHub project setup and sprint planning

Rob committed to creating GitHub issues tagged by milestone by end of day or start of the following week. The first sprint plan was targeted for early the following week. Jan proposed twice-weekly syncs going forward.
