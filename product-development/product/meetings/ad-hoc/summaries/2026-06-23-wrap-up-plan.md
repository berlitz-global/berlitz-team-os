# Wrap up Plan — 2026-06-23
**Attendees:** Jan Hoffmann, Michal Sobocinski, Rob Zinkov
**Date:** 2026-06-23

## TL;DR
- The team reviewed the AI services architecture diagram and discussed what remains before MVP: avatar conversations, level assessment, and audio design.
- Azure Speech Recognition outages on the current portal (concurrent-user limit breaches and silent Microsoft model changes) prompted a discussion about service watchdogs, quality benchmarks, and runtime failover.
- The Content/Curriculum Factory is **not on the critical path** for MVP; learner data will be collected but not actively used until later.
- Issue-tracker hygiene: the team will reorganise existing items under ~4 epics and use `/write-issue` to flesh out individual issues.

## Decisions
- Content/Curriculum Factory is **deprioritised** relative to getting the mobile app running; learner data will be collected but not acted on for MVP.
- Level assessment serves two distinct purposes: (1) user placement/onboarding, and (2) content-level-appropriateness checks in the content creation pipeline. Real-time level assessment *during* a conversation is considered overkill/latency risk.
- Avatar conversations will be supported in MVP; the team wants to blur the line between drills and open conversation ("one big conversation").
- Audio design (ambient background sounds, recognisable sound effects like Duolingo) is a frontend concern currently absent; flagged as something to add.
- Existing epics in the issue tracker will be reorganised into ~4 new epics: **Evaluators**, **Learner Progress**, **LLMs/ASR/TTS/Avatar**, **Content/Curriculum Factory**. Jan will lead that cleanup.
- The team will run through `/write-issue` together for the first few items to align before splitting the work.
- ADR 0007 (auxiliary learner data service alongside LMS) is approved — Daniel signed off.

## Action items
| Owner | Action | Status |
|-------|--------|--------|
| Jan Hoffmann | Review and reorganise existing GitHub epics into ~4 epics | pending |
| Jan Hoffmann | Add individual items from the whiteboard session as issues under the correct epics | pending |
| Rob Zinkov | Pair with Jan to run through `/write-issue` together for the first few issues | pending |
| Rob Zinkov | Download and trial the **Busuu** app (Michal's recommendation as a UX reference) | pending |
| Michal Sobocinski | Notify Sergey of pre-approved vacation days and add dates to the shared calendar | pending |
| Team | Add monitoring / watchdogs and a weekly quality-and-latency benchmark for all external AI services (ASR, TTS, LLMs) | pending |
| Team | Investigate runtime failover between ASR/LLM providers when a service is degraded | pending |

## Open questions
- Should level assessment during an active conversation be included? Concern: latency. Deferred — put it in but iterate if it becomes a problem.
- What is the exact name/grouping for the "LLMs / ASR / TTS / Avatar" epic? Tentatively "AI Interaction Layer."
- Do we want custom avatars (requires a fixed monthly fee to HeyGen / 11 Labs)? Currently Berlitz uses stock avatars with custom voices. No decision taken.
- When exactly is Ali (new hire) joining — July 1 or later?

## Discussion

### Azure Speech Recognition outage (current portal)
Jan opened with a war story from the existing Berlitz portal: Azure Speech Recognition stopped working for a cohort of students in South America because the contracted concurrent-user ceiling was breached — Azure silently returned nothing rather than erroring. A separate incident occurred when Microsoft updated the ASR model without notifying customers, causing regional degradation. The team agreed both failure modes need to be guarded against via (a) real-time health watchdogs, (b) a weekly benchmark pipeline that runs a fixed test set through each external service and tracks quality and latency over time, and (c) runtime failover/load-balancing across providers.

### Architecture diagram review
Rob and Michal reviewed the AI services architecture diagram. They noted the diagram has a "virtuous loop" where evaluation data feeds back into the content factory, which adjusts lessons. Jan proposed two additions: (1) an **audio design** component (ambient sounds, sound effects) to be placed in the frontend box, and (2) a **level assessment** component, which prompted the clarification discussion below.

### Level assessment — two meanings clarified
The team had been using "level assessment" to mean two different things. Jan's concern is *user placement*: placing a first-time user at exactly the right difficulty from the start. Rob had been thinking of level assessment as a *content quality gate*: a quick automated check verifying content is level-appropriate before showing it to a learner. Both uses are now agreed on. Real-time level adjustment *during* a conversation was discussed but deferred due to latency concerns.

### MVP scope: avatar and conversations
Rob wants MVP to include talking to an avatar in (a) open-ended conversation and (b) scenario-based conversation. Jan wants to blur the boundary between drills and conversation so it feels like one fluid experience. Rob noted the Berlitz method at lower levels is "presentation-practice-performance" and at higher levels is "task-supported learning" (scenarios with a concrete task). Busuu was raised as a better UX reference than Duolingo; Michal highlighted its use of video, diverse accents, and ambient audio (coffee-shop sounds).

### Issue tracker hygiene
The proposed new structure is ~4 epics: **Evaluators**, **Learner Progress**, **LLMs/ASR/TTS/Avatar** (name TBD), and **Content/Curriculum Factory**. Individual whiteboard items are granular enough to feed directly into `/write-issue`. Jan will lead the cleanup; Rob and Jan will pair on the first few `/write-issue` runs before splitting the work. Michal confirmed GitHub supports assigning epics to milestones via the issue sidebar.

## Misc
- Michal reminded everyone that Thursday (June 24) is a public holiday in Spain — he will be off.
- Rob does not keep Teams on his personal phone (intentional boundary). The team needs a lightweight out-of-band channel for urgent pings.
- Jan acknowledges he rarely checks email; Teams messages are more reliable.
- Jeff the avatar was identified as "the freaky old guy." Divya (the Indian woman avatar) is in the upper-right of the conversation partner selection screen in Practice Hub.
