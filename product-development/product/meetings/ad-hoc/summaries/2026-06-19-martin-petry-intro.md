# Introductory Meeting: Martin Petry, Jan, Rob & Michal — 2026-06-19

**Attendees:** Martin Petry (Global Head of QA & Operations), Jan Hoffmann, Rob Zinkov, Michal Sobocinski
**Date:** 2026-06-19

## TL;DR

- Martin Petry (Global Operations / QA) walked the team through how Berlitz stores instructor quality data in Salesforce and the current state of "Max" — an AI agent under testing that evaluates lesson transcripts against the Berlitz lesson observation rubric.
- Max is not yet live; it has been through two testing rounds with Martin as sole evaluator, and has recently expanded to a small QA team. Scores are within 0.25 of human evaluators in most cases.
- The team discussed how lesson observation forms link to individual lessons via CH/PD identifiers in Salesforce, and how instructor guides are intentionally flexible frameworks rather than rigid scripts.
- Martin offered to run a dedicated session on the Berlitz method and lesson observation form to help the AI Tutor team better understand pedagogy.

## Discussion

### Max — AI lesson evaluator (testing status)

Martin demonstrated how instructor quality data is stored in Salesforce under each instructor's profile: customer satisfaction scores, lesson observation records, and the PDF monitoring forms completed by QA supervisors. Max is an AI agent built to evaluate lesson transcripts against the same rubric human QA specialists use. Testing shows Max is generally within 0.25 of the human score; divergences occur partly because human supervisors factor in prior feedback and instructor history that Max lacks. Martin has been the sole evaluator through the first two rounds; a small QA sub-team now has access. A key open testing gap: the same transcript has not yet been run through Max multiple times to measure score variance across runs — Michal raised this and Martin acknowledged it as a good idea not yet actioned.

Martin noted Max had a tendency to over-assign "exceeds expectations" scores; this has been tuned down via prompt/configuration changes.

### Complaint handling and the value of transcripts

When a dissatisfied student response comes in, QA specialists currently watch the full lesson recording to fact-find. Martin explained that transcripts (and by extension Max) can help pinpoint where in the lesson the issue arose, reducing the time burden on specialists. Dissatisfaction volumes are low — roughly 9 dissatisfied responses vs. 1,900 very-satisfied in a given month globally.

### Lesson data model and Salesforce identifiers

Jan asked how to reliably link a lesson observation form to the specific lesson it evaluated. Martin clarified that the CH number and PD number in Salesforce together uniquely identify a lesson — they encode time, program, and curriculum unit. Customer satisfaction feedback is intentionally *not* automatically associated with individual lessons (a deliberate design choice, to avoid instructors gaming metrics or conflating student enjoyment with Berlitz-standard teaching quality).

### Instructor guides and pedagogical flexibility

A significant portion of the meeting covered the relationship between instructor guides (IGs) and what actually happens in class. Martin stressed that IGs are frameworks, not scripts — experienced instructors routinely deviate from them to personalise lessons to the student's context. The first criterion on the lesson observation form asks whether the instructor adapted the lesson goal to the student's interests and study needs; generic goal-setting is a negative mark. This has implications for the AI Tutor team's curriculum work: direct comparison between a transcript and an IG will often show divergence by design.

### Mobile app / Felix / blended learning context

Jan described the mobile AI Tutor as likely following a similar online-plus-live-activation structure to Felix (Berlitz's existing blended product). Martin noted that in Felix, customer satisfaction is consistently highest for the live human activation session, not the online practice component. He also confirmed the Speaking Tutor is already fully AI-avatar-based. Felix's earlier iterations received feedback that content was too long and repetitive; subsequent versions addressed some of this but usage remains modest.

### Instructor-facing tooling (backlog)

Martin flagged a long-standing gap: instructors cannot currently see their own customer satisfaction scores in real time. In Japan this was available via iPad; globally it is still done manually. This development has been on the list for ~10 years but has never been prioritised over billing and scheduling work. Jan mentioned that John and Javier are now working on the instructor/teacher side of the product; Martin has been asked by Henning to collaborate with them, with a kick-off planned for the following Tuesday.

### Access to Salesforce data

Rob asked who manages the Salesforce systems in order to get data access. Martin was uncertain of the current owner following recent organisational changes and a ~3-month development freeze; he suggested Javier or Dynas (the engineer who built Max) as contact points.

## Decisions

- Martin will share the lesson observation form guides (for standard and Flex/blended lessons) with the team via Jan; Jan already has copies.
- A follow-up session on the Berlitz method and lesson observation form will be arranged (Martin, Jan, Rob, Michal).

## Action items

| Owner | Action | Status |
| ----- | ------ | ------ |
| Jan Hoffmann | Share lesson observation form guides (standard + Flex) with Rob and Michal | New |
| Jan Hoffmann / Rob Zinkov | Schedule follow-up session with Martin on Berlitz method and lesson observation rubric | New |
| Martin Petry | Run same transcript through Max multiple times to measure score variance | New |
| Rob Zinkov | Identify Salesforce data owner (likely Javier or Dynas) to arrange data access | New |

## Open questions

- Who is currently the owner/maintainer of the Salesforce system after the recent reorganisation and development freeze?
- How much score variance does Max produce when the same transcript is evaluated multiple times?
- To what extent do instructors actually diverge from IGs in practice, and is that divergence measurable at scale from transcripts?
- Should the mobile AI Tutor curriculum be "on rails" (like the online Felix component) or allow flexibility comparable to live human sessions?
