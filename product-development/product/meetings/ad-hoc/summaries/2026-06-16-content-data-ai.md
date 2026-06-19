# Content Authoring & Data Access for AI Tutor — 2026-06-16

**Attendees:** Jan Hoffmann, Nicolas Potel, Rob Zinkov, Michal Sobocinski, Andres Mora
**Date:** 2026-06-16

## TL;DR

- The team toured HyperWave (the content authoring system) and mapped the full content supply chain from scope-and-sequence through instructor guide, student guide, and online practice.
- Key question is whether AI can access HyperWave content via API; contact is Vladimir at Arcadia (aka Software Country).
- Lesson recordings and transcripts are valuable training data for the AI Tutor but are stored only briefly (~30 days); Martin Petry governs access.
- English flex video scripts are largely missing; the team agreed to explore AI-generated captioning via CloudFlare, which already hosts the videos.

## Discussion

### HyperWave Content Architecture

Nicolas walked the team through HyperWave, Berlitz's content authoring platform. The main entry points are:

- **Courses** — current, HTML-based material organized by language. Each course contains: Instructor Guide (IG), Student Guide (SG), and Online Practice.
- **Legacy** — PDF-only materials, some still in use.

Content was originally imported from XML manuscripts into HyperWave before 2018; since then it has been authored natively on the platform. The old XML/docx source files are still visible in authoring mode but should not be treated as source of truth — they are rough first drafts that were refined directly on the platform.

The IG and SG are published to a CDN via a separate tool called the Cobra loader (built and maintained by Arcadia/Software Country) and are then surfaced on the LMS.

### Instructor-Led Lesson Flow

Jan described the current live-lesson flow: instructor references the IG (digital or occasionally print), shares a student-facing view on screen, and the session is recorded via Teams or Zoom. Recordings are accessible to students for approximately 30 days in the "My Media" section of My Berlitz. Martin Petry (on the Gold/operations side) manages recordings and uses them for lesson observation.

The IG contains speaking prompts, sample sentences, and visual asset references. There is also a separate media library (GoldSpot) where instructors can request and fetch supplementary images. Nicolas noted this solution is old and a replacement is being considered.

The student-facing content is deliberately non-evaluative: it has interactive fields (checkboxes, radio buttons, text input) but sends no data back to the LMS. Feedback is given orally by the instructor.

### Flex vs. Standard Instructor-Led

Standard ILT sessions are 45 minutes and cover a full unit. Flex live coaching sessions are 25 minutes and cover only the performance phase — the present and practice phases happen asynchronously on My Berlitz. Because unlock timing varies per student, Flex sessions require the student to book a slot from the calendar rather than having a pre-set schedule. Flex instructor guides live on HyperWave; Flex self-study activities were authored natively on the LMS. This split authoring is acknowledged as non-ideal.

### HyperWave API Access

Rob asked whether there is an API for programmatic access to HyperWave content. Nicolas was not certain one exists but noted that Arcadia (Vladimir and Alexander) has API documentation from the original vendor. Jan noted that Srikant has paused new work with Arcadia on legacy items but that this request — supporting the new AI Tutor build — should be in scope. The team agreed to contact Vladimir to ask about API availability and to obtain the documentation.

### Scope-and-Sequence Index

Jan asked about the pre-authoring artifacts. Nicolas confirmed a scope-and-sequence spreadsheet (vocabulary index) exists for both legacy and new content. Each unit has a speaking goal (the communicative skill a student should be able to perform after the unit) plus grammar points (shown in blue) and vocabulary categories (green). This document is finalized when the course is finished but is updated alongside writing during development.

### Lesson Recordings and Transcripts as Training Data

Michal raised using live-session transcripts as AI training data. Jan confirmed he has a sample recording with a corresponding IG and a human quality observation/rating — a potential labeled dataset. Nicolas offered to share additional onboarding samples. The recordings are held for ~30 days; it is unclear whether transcripts are retained longer. Martin Petry is the decision-maker on retention policy. The team sees this data as valuable for modeling both instructor behavior and student responses, and noted it is stratified by level. Jan flagged privacy considerations around repurposing customer recordings.

### Video Transcripts / Captions

Michal noted that many LMS lesson videos lack transcripts, which affects both accessibility and AI ingestion. Nicolas clarified:

- German, French, and Spanish video scripts exist.
- English Flex videos: the original batch was filmed with live instructors in Princeton. Scripts are fragmentary because content was later reorganized. No reliable English source currently exists.
- New synthetic videos have scripts and captions can be generated cleanly.
- Videos are hosted on CloudFlare, which has an AI-generated captioning feature. Nicolas is willing to pay for a service to caption the older English videos.

Andres Mora confirmed the new SCORM packages include video plus transcription below the video.

### Student Progress Data

Michal asked whether structured student progress notes exist (level, quiz results, instructor notes for the next session). Nicolas explained the post-lesson survey instructors fill out captures: (1) whether the student met the speaking goal, and (2) a 5-skill rating (speaking, pronunciation, listening, reading, grammar). Free-text notes are possible but rarely used. Berlitz policy is that instructors are paid only for teaching time, not admin, so cross-lesson communication is minimal and usually oral.

Nicolas relayed that the Gold operations team raised the same gap that morning: they want a feedback loop so the next instructor knows what was covered and what to focus on. Jan and Nicolas agreed that transcript-derived analysis could automate this — detecting errors, summarizing progress, and presenting a pre-lesson brief to the instructor (a "cockpit") so they can confirm or adjust before the session begins. A concierge that prompts homework check-in before the lesson was also discussed.

## Decisions

- The team will reach out to Vladimir at Arcadia to ask about HyperWave API access and to obtain existing API documentation.
- Nicolas will share CloudFlare credentials with Rob and Michal so they can explore AI-generated captioning for English Flex videos.
- The primary near-term use of transcript/recording data is content generation (creating more lesson content), not student modeling.

## Action items

| Owner | Action | Status |
| ----- | ------ | ------ |
| Nicolas Potel | Send Vladimir's and Alexander's contact details to Rob and Michal | New |
| Rob Zinkov | Contact Vladimir (Arcadia/Software Country) to ask about HyperWave API availability and request documentation | New |
| Michal Sobocinski | Contact Vladimir (Arcadia/Software Country) to ask about HyperWave API availability and request documentation | New |
| Jan Hoffmann | Forward sample lesson recording (with corresponding IG and quality observation) to Rob and Michal | New |
| Nicolas Potel | Share additional sample lesson recordings with the team | New |
| Nicolas Potel | Add CloudFlare credentials to shared access (for Rob and Michal) | New |
| Rob Zinkov | Explore AI-generated captioning service for older English Flex videos hosted on CloudFlare | New |
| Rob Zinkov | Reach out to Martin Petry to discuss access to lesson recordings and transcripts, and clarify retention policy | New |
| Michal Sobocinski | Reach out to Martin Petry to discuss access to lesson recordings and transcripts, and clarify retention policy | New |

## Open questions

- Does HyperWave expose an API, and if so, is Berlitz licensed to use it?
- Are lesson transcripts retained beyond the ~30-day recording window, and under what terms can they be used for AI training?
- What do current customer agreements say about using session recordings for AI/benchmarking purposes?
- Can CloudFlare's built-in AI captioning handle the existing English Flex video library, or is a third-party batch transcription service needed?
