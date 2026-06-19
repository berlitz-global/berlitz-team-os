# AI + Data Weekly Kickoff: Backlog Grooming and MVP Scoping — 2026-06-16

**Attendees:** Jan Hoffmann, Rob Zinkov, Michal Sobocinski
**Date:** 2026-06-16

## TL;DR

- First AI + Data weekly meeting; focused on orienting Jan and Michal to the GitHub Projects board (AI Services project) and walking through the backlog structure.
- The team agreed to scope the MVP around end of July and created an "AI MVP" milestone in GitHub Projects to tag relevant issues.
- Jan proposed two parallel work tracks for MVP: (1) AI avatar component (with ASR/TTS/video avatar integrated) and (2) content/curriculum factory; these are likely large enough to each warrant their own PRD.
- The meeting closed with Jan committing to flag MVP issues and write PRDs; Michal and Rob to then assign and begin work.

## Discussion

### GitHub Projects board orientation

Rob walked Jan and Michal through the AI Services GitHub project. He showed how to navigate the backlog, filter by iteration, view issue details, and use labels. Jan asked about swim lanes (grouping by epic); Rob confirmed this is achievable via "Group by" and discussed using parent/sub-issue relationships. Rob demonstrated creating a parent issue for AI Avatar. The team noted there is no automated sync between issues and PRDs — periodic manual manicuring is expected, potentially aided by an agent.

### Issue quality bar and the LLM-as-reader standard

Rob articulated his preferred bar for issue quality: issues should be specific enough that a newcomer or an LLM could understand what needs to be done without additional context. He noted the AI engineering kit includes a skill for writing/revising issues and plans to use it after priorities are agreed.

### MVP milestone and deadline

The team agreed to end of July as the AI MVP milestone target. Rob created the "AI MVP" milestone in GitHub Projects. Vacation periods noted: Michal out July 15–17; Jan out two weeks in August; Rob out approximately one week end of August/beginning of September.

### MVP scope: AI avatar track

Jan outlined the AI avatar as a self-contained component (ASR + TTS + video avatar) that can be given different personas and dialects. For MVP: single personality. The "AI Avatar" GitHub issue should be restructured as a high-level parent shell with narrower child issues carrying acceptance criteria.

### MVP scope: content / curriculum factory track

For MVP, the team would take ~5 lessons, combine instructor guide content, HyperWave source material, and CEFR definitions, handcraft the pipeline manually as a proof of concept, and validate level-appropriateness. Long-term vision: fully automated pipeline (learning goals + existing content as input → LLM-generated lesson scripts and exercises as output). Minimum viable content for launch: English levels 1–4 at minimum. Chayan is working on adapting existing MyBerlitz on-demand content to mobile.

### PRD granularity and issue-to-PRD linkage

Rob and Jan agreed both the AI avatar and the curriculum factory merit their own PRDs. PRDs are authoritative; GitHub issues are downstream and should link to the relevant PRD (modeled on the ADR-linking pattern in the Berlitz Services repo).

### Lesson content structure and the present–practice–perform model

After Rob left, Jan and Michal discussed Berlitz's three-phase lesson structure. Michal raised a concern: the "present" phase in the existing LMS is mainly videos with no transcriptions. Jan hoped instructor guide content mirrors the video content but acknowledged this needs validation. Michal noted he contacted Nicolas Potel to clarify.

### Analytics and dashboards scope boundary

Internal engineering-facing quality dashboards will be built by this team; broader business analytics will go into a BI tool (Snowflake or similar), out of MVP scope. Longer-term vision includes a teacher cockpit showing student history and session-level learning goal completion.

### Terminology: curriculum vs. certification

"Curriculum" maps to a full course path (e.g., English 1–8), not an individual lesson. Skipped quizzes should not be ignored — the AI Tutor should track unmet learning goals and resurface them in subsequent sessions.

## Decisions

- MVP milestone target: end of July 2026.
- "AI MVP" milestone created in GitHub Projects; issues to be tagged accordingly.
- Parent issue "AI Avatar" created in GitHub Projects; sub-issues to be nested below it.
- Issues must be clear enough for a newcomer or LLM to act on without additional context.
- AI Avatar and Curriculum Factory each warrant separate PRDs.
- PRDs are authoritative; GitHub issues should link to the relevant PRD.
- Internal quality/engineering dashboards are in scope; business BI dashboards are out of scope for MVP.

## Action items

| Owner | Action | Status |
| ----- | ------ | ------ |
| Jan Hoffmann | Review all GitHub Projects issues and flag MVP vs. non-MVP using the AI MVP milestone | New |
| Jan Hoffmann | Write PRDs for AI Avatar and Curriculum Factory | New |
| Jan Hoffmann | Propose swim-lane/parent-issue groupings via group chat | New |
| Rob Zinkov | Manicure issue groupings/parent-child relationships after Jan proposes them | New |
| Rob Zinkov | Polish issues using the AI engineering kit's write-issue skill once priorities are agreed | New |
| Michal Sobocinski | Sync with Rob Zinkov on AI avatar implementation to clarify what can start now | New |
| Michal Sobocinski | Follow up with Nicolas Potel on whether instructor guide content mirrors lesson videos | New |

## Open questions

- Does the existing instructor guide content for English cover the same material as the lesson videos, or are the two independent?
- What structured data is available from the mobile app team (Daniel, Jon) for non-audio, non-avatar lesson interactions?
- Should the content pipeline for MVP be fully manual/handcrafted (spike), or is there a faster path to a partially automated first version?
- Where does Snowflake end and other systems begin for business analytics?
