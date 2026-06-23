# AI Tutor Mobile App Design — Engineering/Design Sync — 2026-06-12

**Attendees:** Rob Zinkov, Chayan Roy
**Date:** 2026-06-12

## TL;DR

- Rob and Chayan aligned on the AI tutor screen designs in Figma and clarified what API/data shape the mobile app will need from the backend.
- Chayan walked Rob through the current wireframes covering Learn, Practice, and AI Tutor avatar screens — still at baseline/wireframe stage; sign-up/sign-in flow is the first delivery.
- Usage data shows current AI avatar sessions average 2–3 minutes and users prefer audio/text over video at a 10-to-1 ratio, informing the discussion on whether to use video avatar at all for MVP.
- The team discussed on-device vs. cloud inference for TTS/STT and the cost/quality trade-offs of avatar providers (Tavus vs. Live Avatar).

## Decisions

- Use Live Avatar (current provider) for MVP; architecture to remain provider-agnostic for future swaps.
- HUD overlay is the designated surface for all real-time text during avatar sessions (transcription, corrections, vocab tracking, historical references).
- Backend will deliver content via WebSockets; no web views.
- Defer on-device LLM inference; evaluate on-device TTS/STT selectively by device tier as a cost-reduction measure.
- Prioritize shipping with third-party APIs in the near term rather than in-housing AI infrastructure.

## Action items

| Owner | Action | Status |
| ----- | ------ | ------ |
| Chayan Roy | Complete sign-up/sign-in flow delivery to Daniel, then return to Learn tab and AI tutor flows | New |
| Chayan Roy | Share Figma access with Rob Zinkov | New |
| Chayan Roy | Arrange Duolingo brownbag session and invite Rob | New |
| Rob Zinkov | Pull sample AI tutor session transcripts and share with Chayan for design reference | New |
| Rob Zinkov | Explore LiveKit integration to improve avatar turn-detection and responsiveness | New |
| Rob Zinkov | Investigate device-tier routing strategy for on-device vs. cloud TTS/STT | New |

## Open questions

- What lesson content types will be built for the Learn tab, and how will that determine HUD/overlay requirements?
- Can Jan Hoffmann's proposed AI pipeline handle LX content reformatting for mobile microlearning at scale?
- What is Berlitz's total annual revenue (needed for cost/margin modeling)?
- At what point does Tavus become cost-competitive enough to revisit as the avatar provider?

## Discussion

### Figma Walkthrough and Design Status

Chayan shared the Figma file covering the main app screens: Learn tab, Practice tab, Tutor/Progress, and the AI avatar conversation screen. The designs are baseline wireframes/mockups rather than finalized UI. Chayan is currently prioritizing the sign-up/sign-in flows as a first delivery to Daniel, with deeper flows (Learn tab, AI tutor) to be refined in subsequent sprints. Rob noted that several screens had a strong Duolingo visual resemblance, which Chayan acknowledged — the intent is to modernize the existing Berlitz design system (described as old-school corporate blue) without abandoning brand identity.

### API and Data Handoff for the AI Tutor Screen

Rob clarified that the backend will expose WebSocket endpoints rather than web views; the mobile client will receive content and render it natively. Exact endpoint contracts will be coordinated with Daniel once the design flows are more locked. Chayan confirmed endpoints are not needed yet — they are needed at the prototype/Tavus stage, not for current Figma work.

### Heads-Up Display (HUD) Concept

Chayan described a heads-up display overlay as the primary surface for all real-time text during AI avatar conversations: live transcription, grammar/pronunciation corrections, references to past sessions, and vocabulary word tracking. The HUD is designed to be dismissible by the user. Rob noted the existing Berlitz desktop avatar has a side-panel word-tracking UI where words light up as the learner says them; Chayan confirmed a similar concept could work in the HUD layer on mobile.

### Learner Memory and Adaptive Practice

Rob raised using agent memory (cross-session conversation history and error tracking) to adaptively surface exercises and have the avatar reference prior mistakes. Chayan confirmed this is desirable and noted the HUD could surface these historical references without requiring a separate screen. Both agreed the avatar should naturally say things like "last time you had trouble with X" rather than presenting it through a distinct UI element.

### Session Length and Engagement Variety

Rob shared API usage data: median AI tutor session is 2–3 minutes, and audio/text usage outpaces video usage by roughly 10-to-1, even since video was introduced 2–3 months ago. Both agreed that staring at a video avatar for extended periods is unappealing and that variety (avatar conversation, quiz, reading exercise, back to avatar) is likely key to engagement. Duolingo lessons, per Chayan's contact, run 2–5 minutes and are trending shorter.

### Avatar Provider Trade-offs: Tavus vs. Live Avatar

Chayan has prior experience with Tavus (perception-analysis-driven avatar that adapts based on user emotional state via camera), but Rob noted Tavus is approximately 3x the cost of the current Live Avatar provider. The team has ~270,000 credits with Live Avatar and agreed to use them while evaluating. Rob proposed potential improvements to the Live Avatar setup via LiveKit for better turn-detection and mood signaling, plus custom avatars to reduce the "stiff/canned" feel. Both agreed the architecture should remain provider-agnostic to allow future swaps.

### On-Device vs. Cloud Inference for TTS/STT

Chayan is prototyping with Qwen 3 (3.6B and 4B parameter models) and platform TTS/STT on an iPhone 16 Pro Max. Rob expressed cautious optimism: models like Parakeet and Qwen can run well on 2–3 year-old devices, and on-device TTS/STT could meaningfully reduce cloud spend given the 10-to-1 audio preference. However, Rob warned that built-in platform TTS quality varies significantly across device age. Chayan noted that even on an iPhone 16 Pro Max, Qwen caused significant heat and battery drain after ~15 minutes. Rob suggested a device-tier approach: route newer flagship devices to on-device inference and fall back to cloud for older hardware. The main LLM was agreed to remain cloud-side for now given model size.

### Duolingo Competitive Insights

Chayan has a contact on Duolingo's subscription/conversion team and is arranging an informal brownbag session. Stats shared: 60M daily active users, ~10% conversion, ~$1.2B revenue, near-zero human instructor cost. Rob noted that AI cost control (Berlitz's projected $173M annual AI spend at scale) is a relevant question to raise. Both agreed shipping a functional product with API providers first is pragmatic given the 1–2 month delivery pressure, with in-housing deferred.

### LX Content Portability to Mobile

Chayan flagged that existing LMS content does not map 1-to-1 to the mobile app; microlearning-format content will need to be created or transformed. Jan Hoffmann has proposed an AI pipeline to reformat LX content. This was noted as an open coordination item.

## Misc

- Rob lives in Berlin and occasionally works from a co-working space in Wedding; Chayan is near Friedrichshain/Lichtenberg. Both are open to meeting in person once AI features begin appearing in the mobile app.
