# Berlitz Method & Evaluation Rubric

> **Status:** Living reference
> **Last Updated:** 2026-06-21
> **Source:** Architecture doc (Layer A, Section 5), AI Conversation Experience PRD Section 8
> **Used by:** AI Conversation Experience PRD, Curriculum Factory PRD

This is the single source of truth for the Berlitz Method definition and the evaluation rubric used to measure AI compliance. Both the conversation engine (runtime) and the content pipeline (generation) are evaluated against this rubric.

---

## Berlitz Method - Core Principles

The Berlitz Method is the teaching methodology that distinguishes Berlitz AI sessions from generic chatbots. These principles are encoded as system prompts injected into every AI session:

- **Immersive L2 use** - maximize target language, minimize L1. The AI speaks the target language; L1 is used only when strictly necessary for comprehension
- **Question-answer cycles** - teacher asks, student answers, teacher corrects/expands. Every turn should advance the learner's production
- **Graduated difficulty** - scaffold up, don't jump levels. Content complexity matches and gently stretches the learner's CEFR level
- **Error correction by salient prompts** - gentle, contextual corrections that elicit self-repair (e.g., "Can you try saying that differently?") rather than implicit recasts. Grounded in Lyster & Ranta 1997: prompts > recasts for acquisition
- **Encouragement patterns** - praise effort, celebrate progress. Positive reinforcement at least once per 5 turns [~]

Source: architecture doc Layer A4; Lyster & Ranta 1997; spec research 2.3

---

## 5-Dimension Evaluation Rubric

The Berlitz Teaching Rubric is derived from annotated real teacher-learner recordings (architecture doc section 5). It is used by:
- The **AI Conversation Experience** to evaluate runtime session quality (automated eval suite + human audit)
- The **Curriculum Factory** to evaluate whether generated scenarios produce compliant teaching interactions

| Dimension | What it measures | Target |
|-----------|-----------------|--------|
| **L2 immersion** | % of AI utterances in the target language | >=98% |
| **Correction accuracy** | % of grammar corrections that are linguistically correct | >=95% |
| **Correction strategy** | % using salient prompts vs implicit recasts | >=80% prompts |
| **CEFR bounding** | % of AI vocabulary within the learner's level band | >=95% |
| **Q&A cycle adherence** | % of turns following question-answer-feedback pattern | >=70% |

**Composite Berlitz Method compliance score** = weighted average of the five dimensions. Weights TBD with designated Berlitz Method expert (see AI Conversation Experience OQ-6).

---

## Eval Thresholds

| Level | Compliance score | When |
|-------|-----------------|------|
| **Launch gate** | >=85% | Phase 2 beta entry |
| **Target** | >=90% | GA (Oct 2026) |
| **Aspirational** | >=95% | GA + 6 months |

If compliance drops below 85% on any eval run, the prompt/model change is blocked.

---

## Evaluation Methodology

### Automated eval suite (run on every model or prompt change)

- **Scenario corpus:** >=30 scripted synthetic-learner sessions [~] spanning A1-B2, covering guided conversation and role-play, with annotated expected teaching behaviors
- **LLM-as-judge scoring** against the 5-dimension rubric above
- **Human audit sample:** 10% of beta sessions [~] reviewed by a Berlitz Method expert. Inter-rater reliability tracked; if kappa <0.6, recalibrate the judge

### Reviewer calibration (for Curriculum Factory content review)

Before the first formal review round, all reviewers independently score a calibration set of 5 scenarios. Inter-rater agreement must reach >=70% (simple agreement on pass/fail per dimension). If below threshold, refine rubric and recalibrate.

---

## CEFR Vocabulary Constraints

AI output is constrained to the learner's CEFR level (Hu & Nation 2000: 95-98% known vocabulary threshold):

| CEFR | Grammar | Vocabulary | Sentence complexity |
|------|---------|-----------|-------------------|
| A1 | Simple present, basic | ~500 words | Short sentences |
| A2 | Past tense introduced | ~1,000 words | Compound sentences |
| B1 | All common tenses | ~2,500 words | Expressing opinions |
| B2 | Complex grammar | ~5,000 words | Nuanced discussion |
| C1/C2 | Near-native complexity | Full range | Full range |

Source: architecture doc A5; Hu & Nation 2000

---

## Sources

- Architecture doc: `engineering/design/plans/ai-tutor-architecture.md` (Layers A4, A5, Section 5)
- Lyster & Ranta 1997 - Corrective feedback (prompts > recasts)
- Hu & Nation 2000 - 95-98% vocabulary comprehension threshold
- VanLehn 2011 - ITS effectiveness (d ~= 0.76)
- Krashen 1982/1985 - Affective filter, comprehensible input
- Swain & Lapkin 1995 - Output hypothesis
