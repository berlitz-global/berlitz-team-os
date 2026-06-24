# More Planning — 2026-06-23
**Attendees:** Jan Hoffmann, Michal Sobocinski, Rob Zinkov
**Date:** 2026-06-23

## TL;DR
- The team spent ~2.5 hours whiteboarding the architecture for the Berlitz AI Tutor app, working through the drill/conversation/evaluator stack and how front-end content delivery maps to back-end services.
- Key tension: keeping the free tier cheap enough to run TTS/ASR at scale while not sacrificing the immersive, audio-first experience.
- The conversation module (guided role-play scenarios vs. free conversation) was defined and separated from classic drills; both need distinct evaluator paths (async for drills, real-time for live conversation).
- Data ownership of learner progress is unresolved — whether the AI team builds and owns the learner-progress service or ingests it from the mobile-app team needs a decision this week.

## Decisions
- Drill evaluation for dogfood will be **rigid/exact match**; for MVP it will add an **LLM-based flexible evaluator** that accepts semantically correct but literally different answers.
- For TTS of static lesson content, audio will be **pre-rendered and cached** (e.g. on S3) rather than generated on every request.
- ASR strategy will have **three tiers**: a good cloud model, a cheaper cloud model (e.g. Open Router), and built-in on-device speech recognition as a free fallback.
- The **level-appropriateness evaluator** will be scoped per-lesson (known vocab + grammar at that lesson), not global CEFR level. Gemma 4 (free/local model) was validated as capable enough for this task.
- Pronunciation assessment is **not currently enabled** in the Berlitz app and is out of scope for dogfood and likely MVP.
- The app's navigation will follow **three tabs**: Learn, Practice, Tutor — consistent with Srikant's design; free conversation lives under Tutor.
- "Conversation scenarios" is the preferred term (over "conversational drills") for guided role-play; a **scenario library** will be the content artifact.
- For the conversation module, **segment transitions** (e.g. order coffee → directions to theater) are natural break points where async grammar/pronunciation feedback can be surfaced without disrupting immersion.

## Action items
| Owner | Action | Status |
|-------|--------|--------|
| Rob Zinkov | Draft document describing the shape of learner data (vocab, grammar, progress) for dogfood/MVP | pending |
| Jan Hoffmann | Discuss data governance / learner-data ownership with the broader team this week | pending |
| Jan Hoffmann / Rob Zinkov | Ask Nicolas and John (Talki/Tokyo contacts) where BPO modules appear in the learner path | pending |
| Team | Add Berlitz demo-account credentials to a password manager (AWS Secrets or 1Password) rather than the repo | pending |
| Rob Zinkov | Share Berlitz Learning Hub login with Michal | pending |

## Open questions
- Who owns the **learner-progress service**? Option A: AI team builds and owns it. Option B: mobile-app team owns it and AI team ingests from it.
- How does **teacher feedback from in-person live classes** flow back to the system?
- Where exactly do **BPO modules** appear in the learner path? Rob noted they appear in English level 5 but the curriculum wiring is unclear.
- Should the level-appropriateness check be done **per-lesson** (explicit vocab/grammar list) or via a higher-level CEFR prompt?
- Should a grammar or pronunciation error **interrupt** a live conversation scenario, or only surface at segment transitions?
- How are Tokyo/Talki conversation scenarios integrated into the overall learner path?

## Discussion

### Reviewing existing myBerlitz portal
Jan and Michal spent time before the meeting walking through the current myBerlitz portal. Key observations: the current implementation has no audio output for drills (the "teacher" does not read the question aloud), and the evaluator does not match on transcribed student speech — it pattern-matches on a canonical answer and rejects anything syntactically different, even if semantically correct. Jan showed a live example where saying "doesn't" instead of "does not" was marked wrong.

### Speech / TTS cost and fallback strategy
The team agreed the free tier must be as cheap as possible because TTS/ASR calls at 1M users become substantial money. Rob proposed a three-tier ASR strategy: best cloud model → cheaper cloud model (Open Router — Michal noted the free tier has ~50% failure rates, so paid access needed) → built-in on-device speech recognition. For TTS of static content, pre-rendering and caching audio files (S3) avoids repeated API calls. Rob flagged that Azure Speech may not be necessary; small, self-hosted ASR models are cheap and straightforward.

### Drill evaluator design
Three evaluator types were identified: grammar evaluator, vocabulary/level-appropriateness evaluator, and pronunciation evaluator. For dogfood, evaluation will be exact/rigid. For MVP and beyond, an LLM layer will be added so semantically correct but literally different answers are accepted. Rob argued this is cheap (small token count), can use a very old/cheap model (even cheaper than Haiku), and is exactly the task LLMs were built for — potentially runnable on CPU.

### Level-appropriateness evaluator
Jan wants an evaluator that, given a lesson number (e.g. "English 3, lesson 5"), knows the vocabulary and grammar a student should know and can flag whether a student's answer is level-appropriate. Michal validated this with Gemma 4: giving it the student's answer, the target context, and a CEFR level produces useful level feedback without explicitly listing every word. Rob corroborated this with his own experiment generating B1 German text using Goethe Institute word limits via Gemma 4. The preferred approach is per-lesson vocab list passed in context, not just a global CEFR label.

### Conversation module: guided vs. free
Jan and Rob debated the distinction between guided conversation scenarios (on-rails role-play, e.g. order a pizza over the phone, book a doctor's appointment) and free conversation (unbounded). They aligned on: guided scenarios belong in the Practice tab, are structured lessons with steps and per-step evaluation, and share an API shape similar to a lesson. Free conversation belongs in the Tutor tab. The term "scenario" (linked to a "scenario library" already in the issue tracker) was preferred.

### Reviewing Talki/Tokyo content library
Rob shared the Talki admin console. Key findings: conversation prompts for English 1 are structured (ask nationality, country, city; ensure student asks five questions). Role-play exercises with target vocabulary appear in English level 5+. Audio outperforms video by a factor of 10 in usage. Progress tracking in Talki is at lesson granularity. Rob confirmed all English content has already been exported to Excel documents previously shared with Michal.

### Architecture whiteboard / data ownership
The final section focused on the system diagram. Jan drew the architecture: frontend → evaluators + user input → conversation module → learner progress / path-and-progress controller → LMS. The unresolved question is who owns the learner-progress service. Rob outlined two options: (1) AI team builds and owns it, (2) mobile-app team owns it and AI team ingests from it. Jan noted three distinct data streams to manage: learner data (vocab, grammar, progress), generic product telemetry, and curriculum-optimization data (raw evaluation outputs for improving content). Jan flagged data governance needs to be discussed with the broader team this week.

## Misc
- Michal is currently on the free tier of Open Router; Rob agreed to get him paid access quickly.
- The team should not commit credentials to GitHub; Rob proposed adopting AWS Secrets Manager or 1Password.
- Miro was mentioned favorably for whiteboarding.
- The three participants were co-located; lunch was coordinated for 1:30 PM with a 3:00 PM reconvene.
