# Lesson Transcript Analysis & QA Agent Deep-Dive — 2026-06-17

**Attendees:** Jan Hoffmann, Rob Zinkov, Michal Sobocinski, Dainis Tkacovs
**Date:** 2026-06-17

## TL;DR

- Dainis demoed a Microsoft Copilot Studio agent ("Max") that evaluates instructor lesson quality from Zoom transcripts, achieving ~97–98% agreement with manual QA scoring.
- Lesson recordings and transcripts live on Zoom Cloud for 15 days, then move to AWS, and are fully deleted at 90 days per GDPR policy — creating a narrow window to extract data for further use.
- The team identified a need to map transcripts to instructor guides and lesson content, and to eventually build a pipeline that automatically pulls transcripts from Zoom into a durable store (e.g., Dataverse or S3) for AI analysis.
- The immediate next step is for the team to set up Zoom accounts, get access to recordings, and schedule a call with Martin (QA team lead) to understand the end-to-end evaluation workflow.

## Decisions

- The team will set up Zoom accounts (Dainis sent invitations before the meeting) and notify Dainis so he can assign roles for transcript access.
- Dainis will share the knowledge-base document used by Max and also the custom prompt (as a TXT file) with the team.
- Jan will invite Dainis to Nicole's workshop the following Wednesday.

## Action items

| Owner | Action | Status |
| ----- | ------ | ------ |
| Rob Zinkov | Create and activate Zoom account; ping Dainis on Teams when done | New |
| Michal Sobocinski | Create and activate Zoom account; ping Dainis on Teams when done | New |
| Jan Hoffmann | Create and activate Zoom account; ping Dainis on Teams when done | New |
| Dainis Tkacovs | Share Max agent knowledge-base document and custom prompt (as TXT) with the team | New |
| Dainis Tkacovs | Find a previously analyzed lesson transcript along with the associated instructor guide for the team to experiment with | New |
| Jan Hoffmann | Invite Dainis to Nicole's workshop next Wednesday | New |
| Jan Hoffmann | Review AI-generated PRD draft and follow up with the team | New |
| Jan Hoffmann | Schedule follow-up to review roadmap/iterations (target: same day or next morning) | New |

## Open questions

- Where exactly are Martin's team's manual QA evaluation documents stored (SharePoint folder, specific Teams channel)?
- Can the Zoom API be used to extract transcripts automatically before the 15-day window closes, and would there be GDPR or contractual constraints on storing them in a separate database?
- Why is Nicole/Product Ops leading the session data analysis workshop, and what is the scope of that effort?
- Is video analysis of lessons (for facial expressions, gestures, pronunciation) feasible in the near future, and at what cost?

## Discussion

### QA Lesson Evaluation Agent (Max)

Dainis described an agent he built several months ago in Microsoft Copilot Studio, available as a Microsoft Teams channel bot called "Max." The agent is used by Martin's QA team to evaluate instructor lesson quality. The current workflow is:

1. A QA team member downloads a Zoom transcript (in VTT format) from the Zoom backend.
2. They manually convert it to TXT (splitting files >10 KB into chunks to stay within Teams upload limits).
3. They upload up to ~10 TXT files per message to Max and ask it to evaluate.
4. Max applies a scoring rubric stored in a compressed knowledge-base document to produce a structured report: summary of strengths and risks, a breakdown by lesson phase (opening, goal, presentation, practice), scores per section with evidence, student performance notes, and AI-generated improvement recommendations.
5. The full evaluation takes ~30–45 seconds.

The agent went through six or seven iteration rounds with Martin's team. Latest results showed ~97–98% agreement between the agent's scores and manual human scores. Dainis attributed this to the scoring rubric being highly standardized, leaving little room for subjective disagreement.

The agent license (MS Copilot Studio) costs ~$5,000/year and is funded by Global Live Operations (Henning's team). It includes 10,000 messages/month across all agents, and current usage is well below that cap. Dainis noted this environment would not scale to serving 700+ instructors or students directly — a different solution would be needed at that point.

### Transcript Data Storage and Access

Lesson recordings and transcripts are created via Zoom (primary platform) or Microsoft Teams (secondary). The data lifecycle is:

- Days 0–15: Recordings and transcripts live on Zoom Cloud/backend.
- After 15 days: Copied to Berlitz's own AWS servers; accessible via student portal or Salesforce by support teams.
- After 90 days total: All recordings and transcripts are deleted per GDPR requirements.

There is currently no automated mapping between a transcript and the lesson content (instructor guide, unit, level) that was supposed to be delivered. The Zoom UI shows instructor email and lesson naming conventions (e.g., "German Level 1 Unit 3"), but no programmatic link to the expected lesson materials. Martin's team manually cross-references Salesforce to know what an instructor was supposed to teach.

Dainis mentioned that in theory, Max could be connected to "Don AI" (another internal agent with access to Berlitz's curriculum materials) so that before evaluating a transcript, it could fetch the expected lesson content and evaluate against it — but this is not implemented.

### Ideal Future Pipeline

Dainis described the ideal end state: an automated background process that pulls transcripts from Zoom via API, stores them in a durable database (Dataverse, AWS, or similar), and allows agents to be triggered simply by specifying an instructor and lesson date — no manual download or conversion needed.

Jan emphasized that the team's primary interest is understanding where the data lives and what infrastructure is needed to build features like the Curriculum Factory or automated micro-learning content generation. Jan noted that the AI Tutor team needs to be able to analyze data from live sessions (with instructors) and eventually mirror that capability in the mobile app.

Jan raised a separate parallel effort: Nicole has scheduled a workshop for the following Wednesday with Henning's team on what data should be extracted from sessions for future analysis.

### AI Spend Visibility

Rob raised the question of tracking AI spend as a team responsibility. Dainis confirmed the MS Copilot Studio license (~$5K/year) is paid by Henning's Global Live Operations team. Rob noted it was important to map where LLM costs are being incurred across the organization, particularly as Microsoft frequently changes pricing.

### PRD and Roadmap (brief)

After Dainis left the call, the remaining three briefly touched on follow-up items. Jan mentioned he had generated a PRD using the PRD skill with a large data dump, and the output was long but mixed in quality — he was still reviewing it. Rob had set up iterations in GitHub (building on Jan's starting point) and added priorities to all issues. Jan planned to review the PRD and the iteration setup, with a goal of getting the roadmap kicked off that day or the next morning.

## Misc

- Dainis is based in Bangkok (UTC+7). He noted flexibility for early-morning or evening meetings to accommodate European and US colleagues.
- Martin Petry (QA team lead) is based in Tokyo; he was unavailable for this meeting due to the time difference.
