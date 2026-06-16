# AI Avatar / Tutor — Specification Research

| Field | Value |
|-------|-------|
| **Author** | Jan Hoffmann, PM |
| **Status** | Research draft (input to PRD) |
| **Last Updated** | 2026-06-16 |
| **Purpose** | Compile internal context + external state-of-the-art + market signals to ground the AI Avatar/Tutor PRD |
| **Related** | `engineering/design/plans/ai-tutor-architecture.md`, `engineering/design/plans/feature-matrix.md`, `product/PRDs/mobile-app-feature-overview.md`, `product/strategy/vision/berlitz-platform-vision.md`, `product/competitive-research/competitors/competitive-matrix.md` |

> This is a **research compilation**, not the PRD. It assembles the evidence base — what we're building internally, what the learning science says actually works, where avatar/voice tech stands, and what the market is hyping — so the PRD can cite grounded sources. Claims are attributed inline. Low-certainty items are marked `[~]`; contested findings are flagged explicitly.

---

## Sourcing & confidence conventions

- **`[~]`** — estimate or unverified figure.
- **`[contested]`** — the claim is real but disputed in the literature or weakly evidenced.
- **`[vendor-claim]`** — self-reported by a company; activity/marketing metric, not independent evidence.
- Academic claims carry author, year, and DOI/URL. Effect sizes are reported as published; a few were sourced from canonical citations rather than re-fetched full text — verify exact digits before quoting externally.
- Funding/market facts marked **[verified]** were fetched from the primary source during this research.

---

## Executive Summary

Berlitz is building an **AI Tutor with two interaction modes — Audio-Only (drills) and Avatar (conversation)** — as the strategic core of a new Learner App (web Sep 2026, mobile Oct 2026). The internal architecture is well-developed: a content pipeline that turns Berlitz's pedagogical IP into AI scenarios, a real-time AI engine (ASR/TTS/LLM + pronunciation + CEFR assessment), a human-teacher bridge, and an evaluation framework benchmarked against real teacher recordings. A parallel strategic question is **build-vs-buy** for the avatar/voice stack, prompted by the current ~€26k [~] spend and a brief on replacing the third-party vendor (Talkio) with an in-house tutor.

The external evidence points to four things the PRD should internalize:

1. **The avatar's value is mostly motivational, not instructional.** Meta-analyses show on-screen pedagogical agents produce only a small learning-outcome gain (g ≈ 0.19; Schroeder et al. 2013). The outcome lift comes from *behavior* — human voice, conversational tone, gesture/gaze — **not** from the presence of a face (Mayer's "image principle" is often null). This argues for investing in voice, responsiveness, and feedback quality before photorealism.

2. **The instructional moat is feedback + speaking practice + spacing, not the character.** The strongest, most robust evidence supports distributed practice/spaced repetition for vocabulary (Cepeda et al. 2006; Bahrick et al. 1993), salient corrective feedback that elicits self-repair over implicit recasts (Lyster & Ranta 1997; Li 2010), and high-volume low-anxiety speaking practice (Swain's output hypothesis + Krashen's affective filter). An AI tutor's genuine edge is giving learners far more low-stakes speaking reps with immediate, salient feedback than a classroom can.

3. **Real-time avatar conversation is technically viable, and at Berlitz's volume the unit cost is low.** Natural turn-taking needs ~200–500 ms response gaps (Stivers et al. 2009). Vendor *list/PAYG* prices for real-time avatar APIs span a wide range ($0.01 up to ~$5.90/min at the premium end), but these are the wrong anchor for an enterprise deal negotiated at volume. Berlitz's own cost model (v0.2.8) assumes **$0.01/min (Simli) to $0.10/min (HeyGen LiveAvatar Lite)** for the avatar render, with an on-device path at ~$0.005/min — putting an all-in enterprise avatar-conversation minute (avatar + voice + LLM + pronunciation) at roughly **$0.10–$0.15/min [~]**, dominated by the avatar render. Native speech-to-speech (OpenAI Realtime) is fastest but **does not expose phoneme-level pronunciation scores**, which Berlitz needs — pointing toward a hybrid pipeline.

4. **The market hype is real and well-funded, but efficacy evidence is thin.** Speak ($1B valuation, OpenAI-backed) and Praktika (AI-avatar, $35.5M Series A) are the poster children; Duolingo's "AI-first" push and video avatar "Lily" and Khan's "2-sigma tutor for everyone" thesis dominate the narrative. The loudest efficacy numbers are vendor marketing from tiny studies; the few credible independent signals (a 2026 PNAS Khan Academy study; a contested World Bank Nigeria GPT-4 tutoring RCT) are not about talking avatars specifically.

**Net implication for the PRD:** lead with feedback quality, speaking volume, and CEFR-appropriate adaptivity; treat the avatar as an engagement layer to be earned through behavior, not photorealism; design the speech stack as a hybrid (conversational S2S + a pronunciation-scoring pass); and set efficacy expectations against credible effect sizes (VanLehn's ITS ≈ human-tutor d ≈ 0.76; field-RCT ITS g ≈ 0.3–0.5) rather than the inflated "2-sigma" trope.

---

## Part 1 — Internal context: what Berlitz is building

Synthesized from the repo (`ai-tutor-architecture.md`, `feature-matrix.md`, `mobile-app-feature-overview.md`, `berlitz-platform-vision.md`), Teams discussions, and SharePoint.

### 1.1 Product shape

The AI Tutor is the **strategic core** of the Learner App. It has two interaction modes sharing one AI engine:

- **Audio-Only Mode (drills, 1–5 min):** listen → repeat → feedback. Pronunciation, vocabulary, and grammar drills with phoneme-level visual feedback. No visual character; faster to load; accuracy over fluency.
- **Avatar Mode (conversation, 5–20 min):** multi-turn dialogue and role-play with an animated 3D character (lip-sync, expressions, gestures), scene rendering, real-time transcript, inline correction.

A third layer surfaced in Teams (Chayan Roy, Jun 3 2026): **microlearning lessons** (Babbel/Duolingo-style 10–20 tap exercises, 2–5 min) that feed into the AI practice. The open question raised internally: *does the MVP include those tap-based micro-lessons, and how does existing course content flow into the AI avatar/voice practice?*

### 1.2 Architecture (four layers + evaluation)

- **Layer A — Content Pipeline (offline):** ingests Berlitz instructor/student-guide PDFs → structures by CEFR level/skill/topic → LLM generates conversation scenarios, pronunciation drills, role-play scripts, with Berlitz Method encoding and CEFR-bounded language constraints → human QA → versioned scenario library. *This is positioned as the defensible moat — 140+ years of structured pedagogical IP no competitor has.*
- **Layer B — AI Engine (real-time):** session orchestrator, conversational AI core, ASR, TTS, pronunciation analysis, grammar/vocabulary feedback, adaptive difficulty, CEFR assessment.
- **Layer C — Presentation:** Audio-Only + Avatar modes, shared session UI, post-session review.
- **Layer D — Learning Intelligence:** persistent learner profile, event pipeline, teacher-context bridge, adaptive curriculum engine.
- **Evaluation & Simulation Framework:** synthetic learner profiles, automated session runner, and a **ground-truth benchmark built from real teacher-learner recordings** scored against a "Berlitz Teaching Rubric." Flagged as essential infrastructure ("without it, we cannot measure whether the AI Tutor is teaching or just chatting").

### 1.3 MVP scope (Sep 2026)

The feature matrix tags 38 MVP features (of 75 total). AI-relevant MVP items include: pronunciation/vocabulary/grammar drills + drill summary (Audio-Only); avatar character, guided conversation, role-play, real-time grammar correction, Berlitz Method compliance, level-appropriate language (Avatar); PDF ingestion, scenario generation, content QA, scenario library (Content Factory); CEFR assessment, adaptive difficulty, learner profile (AI Engine); simulation engine + ground-truth benchmark (Evaluation). Human-teaching integration and enterprise admin are explicitly **post-MVP**.

> **[~] Flagged assumption (from the architecture doc):** "Both audio-only and avatar modes ship at MVP. This depends on avatar technology feasibility — revisit after avatar tech evaluation." Fallback if avatar slips: audio-only + text-based conversation.

### 1.4 The build-vs-buy trigger

- Internal SharePoint brief: *"Replacing Talkio — Building an In-House AI Speaking Tutor for Berlitz: Build vs. Buy Analysis & Roadmap"* (R. Zinkov, Jun 2026). Companion `features.md` lays out P0 (LMS integration, learner profile sync — "must be done before Talkio can be switched off"), P1 (Talkio feature parity: real-time voice, pronunciation assessment, tutor voices/accents, in-session vocab tools, post-session assessment), and P2 "in-house unlocks" (custom Berlitz avatar, lesson authoring, **self-hosted TTS to eliminate ElevenLabs billing**, instructor voice cloning, **self-hosted talking-head renderer to eliminate LiveAvatar billing**).
- Jan Hoffmann (Teams, May 18 2026) asked what Berlitz pays for "the AI tutor agent… is that the avatar we pay 26k for?" — i.e., current avatar spend ~€26k [~] is a live cost concern.
- The cost model (`berlitz_cost_model_v0.2.8.xlsx`) tracks per-session AI costs (LLM, STT, TTS, pronunciation, avatar) and a `no_avatar` scenario is explicitly contemplated in the Berlitz Simulator plan. A changelog example notes "Avatar cost updated from $0.45/min to $0.03/min — Simli volume pricing quote received" [~].

### 1.5 Strategic framing

The platform vision casts Berlitz as an "**AI-native workforce communication platform**," operating on the principle **"AI Suggests. Humans Decide."** (human-in-the-loop guardrails). The durable advantage is framed as the data/operational moat connecting learning behavior to outcomes — not the avatar feature itself. This matters: it aligns with the external evidence that the character is not where the learning lives.

---

## Part 2 — Learning science: what makes an AI tutor *teach* (not just chat)

The central design question. Evidence below is the strongest available grounding for the PRD's pedagogical requirements.

### 2.1 Intelligent tutoring systems work — but "2-sigma" is a trap

- **Well-designed computer tutors approach human-tutor effectiveness.** Kurt VanLehn's meta-review found human tutoring vs no-tutoring at d ≈ 0.79 (not the mythical 2.0), and step-based/substep intelligent tutoring systems at d ≈ 0.76 — essentially matching human tutors; older answer-based CAI was weaker (~0.3). *Granularity of interaction (step-level feedback) matters more than "human-ness."* — VanLehn (2011), *Educational Psychologist* 46(4):197–221, https://doi.org/10.1080/00461520.2011.611369
- **The "2-sigma" claim is contested.** Bloom (1984) reported 1:1 mastery tutoring ~2 SD above conventional classes — but this rests on two small, short dissertations and **has not replicated at that magnitude**. VanLehn's numbers directly undercut it. Treat "2 sigma" as an aspirational ceiling / marketing trope, not a defensible target. — Bloom (1984), *Educational Researcher* 13(6):4–16, https://doi.org/10.3102/0013189X013006004 `[contested]`
- **Field-RCT reality check.** Real-classroom ITS effects typically land at g ≈ 0.3–0.5 — meaningful but well short of lab claims. — Kulik & Fletcher (2016), *Review of Educational Research* 86(1):42–78, https://doi.org/10.3102/0034654315581420
- **Mastery learning** (require ~90% before advancing; attribute failure to instruction, not ability) has solid but more modest support than 2-sigma. — Winget & Persky (2022), *Am. J. Pharm. Educ.* 86(10):8906, PMC10159400.

### 2.2 The mechanisms an AI tutor can exploit better than a classroom

- **Comprehensible input + i+1 (Krashen).** Acquisition is driven by input slightly above current level; basis for CEFR-graded adaptive difficulty. Widely influential but **criticized as untestable** — use as a design heuristic, not proof. — Krashen (1985), *The Input Hypothesis*, https://www.sdkrashen.com/content/books/principles_and_practice.pdf `[contested]`
- **Affective filter (Krashen).** Anxiety/low self-esteem block input processing. Speaking is consistently learners' most anxiety-inducing activity (MacIntyre & Gardner; Young 1990). **A private, judgment-free AI partner is a near-textbook intervention for lowering speaking anxiety** — arguably the strongest theory-fit selling point for AI speaking practice. Frame as "reduces measurable speaking anxiety," not as proof of the filter construct. — Krashen (1982), https://en.wikipedia.org/wiki/Affective_filter
- **Output hypothesis (Swain).** Producing language ("pushed output") forces syntactic processing via noticing gaps, hypothesis-testing, and reflection — input alone is insufficient (French-immersion learners stayed non-native-like despite years of rich input). — Swain & Lapkin (1995), *Applied Linguistics* 16:371–391, https://en.wikipedia.org/wiki/Comprehensible_output
- **Interaction hypothesis (Long).** Negotiated, two-way interaction (clarification requests, comprehension checks) drives acquisition more than static input — the theoretical backbone for dialogue practice. — Long (1996); meta-analytic support Mackey & Goo (2007).
- **Productive tension to resolve in product:** Swain says *push* speaking; Krashen warns pushing speaking *raises* anxiety. An AI tutor uniquely resolves this — high-volume, low-stakes speaking reps mitigate both objections at once.

### 2.3 Corrective feedback — it works, but *how* matters

- **Corrective feedback has a moderate, durable effect** (overall ≈ d/g 0.61, effects grow on delayed post-tests; explicit tends to outlast implicit). — Li (2010), *Language Learning* 60(2):309–365, https://doi.org/10.1111/j.1467-9922.2010.00561.x
- **Oral feedback in classrooms is effective; prompts that push self-repair ≥ recasts.** — Lyster & Saito (2010), *SSLA* 32(2):265–302, https://doi.org/10.1017/S0272263109990520
- **Recasts are the most common but lowest-uptake feedback type.** Foundational descriptive finding: recasts were ~55% of teacher feedback yet produced the least learner self-correction; "negotiation of form" (prompts, elicitation) generated far more. — Lyster & Ranta (1997), *SSLA* 19(1):37–66, https://doi.org/10.1017/S0272263197001034
- **Recast effectiveness is conditional** on developmental readiness and on the learner *noticing* the correction. — Ellis & Sheen (2006), *SSLA* 28(4):575–600, https://doi.org/10.1017/S027226310606027X
- **Product implication:** make corrections **salient** (explicit or prompt-style "can you try that again?") rather than relying on implicit recasts, delivered with **focus-on-form inside meaningful tasks** (Long 1991) and timed to avoid disrupting fluency/raising anxiety.

### 2.4 Spaced repetition — the most robust lever

- **Spacing effect** is one of learning science's most robust findings: distributed practice beat massed practice in 259 of 271 comparisons. — Cepeda, Pashler, Vul, Wixted & Rohrer (2006), *Psychological Bulletin* 132(3):354–380, https://doi.org/10.1037/0033-2909.132.3.354
- **Spacing works specifically for L2 vocabulary, and wider gaps win:** 56-day spacing beat 28/14-day; 13 sessions at 56-day spacing matched 26 sessions at 14-day. — Bahrick et al. (1993), *Psychological Science* 4(5):316–321, https://doi.org/10.1111/j.1467-9280.1993.tb00571.x
- **Pair with retrieval practice** (test-enhanced learning compounds the gains). — Roediger & Karpicke (2006), *Psychological Science* 17(3):249–255, https://doi.org/10.1111/j.1467-9280.2006.01693.x
- **Product implication:** the vocabulary engine should be SRS-based (Anki/SuperMemo lineage) with expanding intervals — this is the highest-confidence pedagogical requirement in this doc.

### 2.5 Comprehension threshold for "appropriate difficulty"

- Reading comprehension drops sharply below ~95–98% known vocabulary — empirical basis for CEFR-graded "just-above-level" content selection. — Hu & Nation (2000), *Reading in a Foreign Language* 13(1):403–430.
- **CEFR (A1–C2)** is the operational scaffolding scale, but it describes *can-do* competencies, not a difficulty algorithm; mapping content difficulty to CEFR introduces measurement assumptions. — Council of Europe (2001; Companion Volume 2020), https://www.coe.int/en/web/common-european-framework-reference-languages `[~]`

---

## Part 3 — The avatar: do on-screen characters actually help?

Directly relevant to the build-vs-buy and "how much to invest in photorealism" decisions.

### 3.1 Pedagogical-agent / embodiment evidence

- **The "persona effect": agents boost perceived experience/engagement, not necessarily outcomes.** — Lester et al. (1997), *CHI '97*, https://doi.org/10.1145/258549.258797
- **Meta-analysis: adding an agent yields only a small learning gain (g ≈ 0.19).** Larger for some moderators (on-screen with younger learners); near-zero in others. — Schroeder, Adesope & Gilbert (2013), *J. Educational Computing Research* 49(1):1–39, https://doi.org/10.2190/EC.49.1.a
- **The outcome lift comes from agent *behavior*, not its presence.** Human-like gesture/gaze improved transfer (d ≈ 0.4–0.8); gesturing specifically helps (g ≈ 0.36 retention). — Mayer & DaPra (2012), https://doi.org/10.1037/a0028616; Davis (2018), *Educational Research Review* 24:193–209, https://doi.org/10.1016/j.edurev.2018.05.002
- **Agents do not reliably increase cognitive load** (a common fear) — mixed-to-null. — Schroeder & Adesope (2014), https://doi.org/10.1080/15391523.2014.888265

### 3.2 Mayer's multimedia principles for a talking avatar

All from Mayer (2014), *Cambridge Handbook of Multimedia Learning* (2nd ed.), https://doi.org/10.1017/CBO9781139547369.017:

- **Voice principle** — use a human (not machine-sounding) voice. Median d ≈ 0.74. *Strong support for high-quality TTS / voice cloning.*
- **Personalization principle** — conversational, first/second-person language beats formal. Median d ≈ 1.1 (one of the largest multimedia effects). *Strong support for a conversational Berlitz-Method tone.*
- **Image principle** — adding a static on-screen image/face of the speaker does **NOT** reliably help (often null, median d ≈ 0.20 and inconsistent). **This is the key caution: a face alone is not the lever.** `[contested]`
- **Redundancy principle** — don't add on-screen text duplicating speech (harms, d ≈ 0.86) — **but this can reverse for L2 learners**, where verbatim captions help. *A/B captions by proficiency.* — Mayer & Fiorella (2014), https://doi.org/10.1017/CBO9781139547369.015

### 3.3 Uncanny valley — a real risk for photoreal talking heads

- Mori's uncanny valley: affinity rises then sharply drops near (not at) full realism, and **motion amplifies the dip** — realistic-but-imperfect talking heads sit in the riskiest zone. — Mori (1970/2012), https://doi.org/10.1109/MRA.2012.2192811
- Empirically confirmed for faces; eeriness is driven by **mismatched/atypical features** and **inconsistent realism** (e.g., realistic face + imperfect lip-sync/eyes). — Mathur & Reichling (2016), *Cognition* 146:22–32, https://doi.org/10.1016/j.cognition.2015.09.008; MacDorman & Chattopadhyay (2016), *Cognition* 146:190–205, https://doi.org/10.1016/j.cognition.2015.09.019
- **Product implication:** a **stylized, clearly-non-photoreal avatar is the safer choice** than a near-photoreal talking head. If pursuing realism, prioritize *consistency* across face, motion, gaze, and lip-sync over raw fidelity.

### 3.4 Synthesis for the avatar decision

The evidence converges: **invest in voice quality, conversational tone, responsiveness, gesture/gaze, and feedback — not in photorealism.** A face adds motivation (which aids retention/engagement, a real business lever) but little direct learning, and a near-real face carries uncanny-valley downside. This supports a measured avatar investment and validates the architecture doc's open question about whether avatar must be MVP-essential.

---

## Part 4 — Avatar & voice technology landscape (2025–2026)

### 4.1 Latency: the bar for "natural"

- Human turn-taking gaps are ~200 ms on average across 10 languages; all language means fall within ~500 ms. **Sub-500 ms (ideally ~200–300 ms) end-to-end is the "feels natural" bar; ~500 ms–1 s is noticeable; >1 s feels laggy.** — Stivers et al. (2009), *PNAS* 106:10587–10592, https://www.pnas.org/doi/10.1073/pnas.0903616106
- The "sub-500 ms voice-to-voice" engineering target is a vendor convention (LiveKit, Deepgram, Cartesia, OpenAI), not a formal spec. `[~]`

### 4.2 Real-time talking-head avatar vendors

| Vendor | Real-time? | Transport | Latency | Published price | Notes |
|--------|-----------|-----------|---------|-----------------|-------|
| **Tavus** (Phoenix/Raven/Sparrow, CVI) | Yes (full pipeline) | WebRTC (Daily) | "lowest latency" claim; ~600 ms figure circulates but **unverified** `[~]` | **$0.32–$0.37/min** conversational video [verified, tavus.io/pricing] | Dedicated turn-taking model (Sparrow); 100+ replicas, 42+ langs; custom replica from ~2-min video |
| **HeyGen** Interactive Avatar → **"LiveAvatar"** | Yes (streaming line) | WebRTC (LiveKit) | low-latency two-way | **~$1/min** (legacy Avatar III) to **$3–4/min** (premium IV/V) [verified, developers.heygen.com] | Flagship Avatar IV/V is async; streaming is the real-time product. G2 #1 Fastest Growing Product 2025 |
| **D-ID** Agents | Yes | real-time streaming API | "under 2 seconds" `[vendor-claim]` — slower than the natural bar | **1 credit/min** confirmed; $/credit on JS page unverified `[~]` | LLM+RAG visual agents; "V4 Expressive" (2026) |
| **Simli** | Yes (purpose-built) | WebRTC (P2P/LiveKit) | low (speech→video) | **not published** in docs; third-party reports ~$0.03–0.18/min `[~]` | "Add a face to your AI agent"; bring-your-own LLM/TTS; cheapest where confirmable |
| **Synthesia** | **Mostly async** | n/a (script→video) | n/a | n/a | Not a real-time conversational API — likely out of scope for live turn-taking |

*The prices above are vendor list/PAYG rates and are the wrong anchor for Berlitz.* At enterprise volume the rates are negotiated and far lower: **Berlitz's cost model v0.2.8 assumes $0.01/min (Simli Trinity-1) for Free–Career tiers and $0.10/min (HeyGen LiveAvatar Lite) for Premium/Enterprise**, with an on-device/in-house render at ~$0.005/min. The avatar render is still the single largest line in the real-time stack, so vendor choice/negotiation there moves margin the most — which is why the `no_avatar` and on-device scenarios matter and why the ~€26k current spend [~] is worth pressure-testing against these per-minute economics.

### 4.3 Speech stack (STT / TTS / real-time)

- **STT/ASR:** Deepgram Nova-3 — streaming WER ~6.84% (vendor benchmark), from **$0.0077/min**, strong multilingual/non-native handling (vendor preference study) — https://deepgram.com/learn/introducing-nova-3-speech-to-text-api. OpenAI `gpt-4o-transcribe` ~$0.006/min (Whisper family is **not natively streaming** — a latency disadvantage). Azure STT ~$1/audio-hour `[~ verify]`.
- **TTS / voice cloning:** ElevenLabs Flash v2.5 advertises ~75 ms latency *(model inference only; excludes app/network — real TTFB is higher)* — https://elevenlabs.io/docs/overview/models; pro voice cloning from the $11/mo tier; effective ~$0.05–0.36/min by tier. Cartesia Sonic offers **word- and phoneme-level timestamps + custom pronunciation dictionaries** (directly useful for pronunciation feedback). Azure Neural TTS ~$15/1M chars, 400+ voices, Custom Neural Voice for instructor cloning (consent-gated).
- **Real-time conversational:** OpenAI Realtime API / `gpt-realtime` (GA Aug 28 2025) is native speech-to-speech — lowest latency, can switch languages/accents mid-sentence; ~$32/1M audio-in, ~$64/1M audio-out tokens (~$0.06–0.24/min `[~]`) — https://openai.com/index/introducing-gpt-realtime/. Google Gemini Live is a comparable native-audio option.
- **Pronunciation assessment:** **Azure Pronunciation Assessment** is the strongest documented fit — phoneme/syllable/word/full-text scores, FluencyScore, ProsodyScore (en-US), miscue detection, scripted + unscripted modes, priced same as standard STT — https://learn.microsoft.com/azure/ai-services/speech-service/how-to-pronunciation-assessment. **Speechace** and **ELSA API** are purpose-built for non-native learners but are contact-sales priced.

### 4.4 The critical architecture tradeoff for a tutor

Native speech-to-speech (OpenAI Realtime, Gemini Live) gives the best conversational feel **but does not expose a clean transcript or phoneme/word-level pronunciation scores** — a real limitation for a tutor that must give pronunciation feedback. A **pipeline (STT → LLM → TTS)** is higher-latency but yields transcripts, confidence scores, and a hook for a separate pronunciation-scoring pass. **Recommended pattern: a hybrid** — native S2S for fluid conversation in Avatar mode, plus a parallel Azure/Speechace/ELSA scoring pass (and/or pipeline mode for Audio-Only drills where accuracy beats latency).

### 4.5 Build-vs-buy: self-hostable talking-head models

- **MuseTalk** (Tencent, v1.5 2025) — real-time lip-sync ~30 fps+ on a single V100; strongest OSS candidate, but dubs an existing face rather than driving from a still, and trails commercial photorealism. https://github.com/TMElyralab/MuseTalk
- **LivePortrait** (Kuaishou 2024) — ~12.8 ms/frame on RTX 4090; expression/pose transfer, not a full audio-driven stack. https://github.com/KwaiVGI/LivePortrait
- **SadTalker** — batch/offline, modest quality, good for pre-rendered clips, **not** live conversation.
- Newer real-time OSS (Ditto, FasterLivePortrait/TensorRT) shows the frontier moving toward real-time conversational avatars — all require self-hosted GPUs.
- **Tradeoff:** OSS gives near-zero per-minute software cost + full data control, but you run/scale your own GPU fleet and **must stitch your own STT+LLM+TTS+turn-taking+WebRTC loop** — the integrated low-latency turn-taking is exactly what commercial APIs (e.g., Tavus's Sparrow) sell. For MVP speed, buy; for the P2 "in-house unlocks" and margin, the self-hosted renderer/TTS path is the strategic build (matches the internal `features.md` roadmap).

---

## Part 5 — Market & competitor signals: what's being hyped

### 5.1 The funded poster children

- **Speak** [verified, speak.com/blog/series-c]: **$78M Series C at a $1B valuation** (Dec 10 2024), Accel-led, with **OpenAI Startup Fund**, Khosla, Y Combinator; **$162M raised to date**; valuation doubled in six months. Speaking-first, **no live human tutors**; "1 billion+ sentences spoken" in 2024 `[vendor-claim]`; Speak for Business cites 200+ customers, 85% adoption `[vendor-claim]`.
- **Praktika** [verified, TechCrunch 2024-05-22]: **$35.5M Series A led by Blossom Capital (May 2024)**, after a $2.5M seed; AI-**avatar** tutors with tone-of-voice/emotion and multiple accents; **1.2M MAU and ~$20M revenue** at the time of the round; participation from Carles Reina (ElevenLabs) and Patrice Evra. Current site claims "20M+ learners" `[vendor-claim, ~]`; "Praktika 4.0" (Feb 2026) touts new generative-AI animation + multi-agent infrastructure. OpenAI published a Praktika case study.
  - *Praktika's efficacy stats ("250% confidence," "23% fluency," "12× more practice") trace to an ~n=30, 8-week, self-published study conflated across apps* `[vendor-claim — treat as hype]`.

### 5.2 The incumbents' AI narrative

- **Duolingo**: **Duolingo Max** (Mar 2023, GPT-4) with **Video Call (avatar "Lily")** and Roleplay. CEO Luis von Ahn's **"AI-first" memo (Apr 2025)** triggered public backlash (users canceling subscriptions/streaks; the company pulled its social videos). 10.9M paying subscribers (Jun 2025); plans for ~150 GenAI-built courses. **Efficacy is mixed**: company-funded studies claim university-equivalent gains, but a 2017 study found no significant difference vs classroom for elementary Spanish, and a **2023 Duolingo-funded study found learners "did not significantly learn much grammar."** — https://en.wikipedia.org/wiki/Duolingo `[contested]`
- **Khan Academy / Sal Khan**: **Khanmigo** (Mar 2023, GPT-4), pilot ~65,000 students; Khan's TED talk + book *Brave New Words* frame AI as delivering Bloom's "2-sigma" tutor "for every student." **But** WSJ (Feb 2024) found Khanmigo "made basic calculation errors," and Khan concedes the AI "can't just sit there and wait." Google **LearnLM/Gemini** partnership deepened (2026), pitched as supporting (not automating) instruction.
- **ELSA Speak** (pronunciation AI), **Babbel** (more conservative AI conversation positioning, "human linguists + AI"), and **Google LearnLM** round out the field. `[~ — ELSA/Babbel specifics not independently verified this pass]`

### 5.3 Efficacy vs hype — the honest read

- **Credible independent positive signals are rare and not avatar-specific:** a **2026 PNAS Khan Academy study** (Eames et al., doi:10.1073/pnas.2507708123) associating platform use with improved math learning; and a **World Bank Nigeria GPT-4 tutoring RCT** (2024–25) reporting large gains (~1.5–2 years of schooling-equivalent over ~6 weeks) — **widely cited but contested** (short, supervised, possible novelty effects, not peer-reviewed at release). `[contested]`
- **The skeptic case is consistent:** most vendor "efficacy" numbers are activity metrics or tiny uncontrolled studies; chatbots make factual errors; engagement/confidence ≠ measured proficiency; AI-generated content risks losing socio-cultural nuance (the Hechinger "Proof Points" / EdSurge / Audrey-Watters tradition). 
- **Implication for Berlitz:** the market rewards the *narrative* (avatars, "AI tutor for everyone") but the *defensible* differentiation is exactly what Berlitz already has — structured curriculum, CEFR alignment, a teaching method, real teacher recordings for evaluation, and the human bridge. Lead with rigor (the evaluation framework) as a credibility wedge competitors can't easily match.

### 5.4 Where Berlitz sits competitively (internal matrix, mid-2026)

From `competitive-matrix.md`: Berlitz targets best-in-class on Content & Pedagogy (CEFR alignment 5/5, structured curriculum 5/5, business content 5/5), Assessment, Human-teacher integration, and Enterprise — and **must catch up** on gamification (Duolingo 5/5), mobile maturity, free-tier depth, language breadth, and speech-AI quality (Speak/ELSA set the bar). On **AI Avatar/Visual Agent**, Praktika is the only 5/5; Berlitz targets 4/5. Unique advantage: the **AI + human hybrid with credit-based monetization** — no competitor does both well.

---

## Part 6 — Implications & open questions for the PRD

### What the evidence says to prioritize

1. **Feedback quality > avatar fidelity.** Salient, self-repair-eliciting corrective feedback (not implicit recasts), focus-on-form in meaningful tasks. (Lyster & Ranta; Li 2010)
2. **Speaking volume at low anxiety is the unique edge.** Maximize low-stakes speaking reps; this resolves the Swain/Krashen tension classrooms can't. (Swain; Krashen)
3. **SRS vocabulary engine** with expanding intervals — highest-confidence requirement. (Cepeda; Bahrick)
4. **CEFR-bounded adaptive difficulty** at ~95–98% comprehension threshold. (Hu & Nation; CEFR)
5. **Voice + conversational tone are evidence-backed; a static face is not.** Invest TTS/voice-clone quality and conversational personalization first. (Mayer voice d≈0.74, personalization d≈1.1, image ≈ null)
6. **Stylized avatar over photoreal** to dodge the uncanny valley; earn the avatar's value through gesture/gaze/voice. (Mori; Mathur & Reichling)
7. **Hybrid speech architecture** — conversational S2S + dedicated pronunciation scoring (Azure/Speechace/ELSA). Don't rely on pure S2S for a tutor that must score pronunciation.
8. **Set efficacy expectations honestly** — cite VanLehn (ITS ≈ human tutor, d≈0.76) and field RCTs (g≈0.3–0.5), avoid "2-sigma."

### Open questions to resolve in the PRD

| # | Question | Source of tension |
|---|----------|-------------------|
| 1 | Is the **avatar MVP-essential**, or does audio-only + text ship first if avatar tech slips? | Architecture doc flagged assumption; evidence says avatar is engagement, not learning |
| 2 | **Build vs buy** the avatar renderer and TTS — MVP buy (Tavus/HeyGen/Simli) vs strategic self-host (MuseTalk/LivePortrait + self-hosted TTS) | Internal `features.md` P2; ~€26k spend; cost model `no_avatar` scenario |
| 3 | Do MVP **microlearning tap-lessons** ship, and how does existing course content flow into AI practice? | Chayan Roy Teams thread (Jun 3 2026) |
| 4 | Which **ASR best handles your learners' actual accents** — Deepgram vs gpt-4o-transcribe? Needs an A/B on real learner audio. | Vendor benchmarks are self-run |
| 5 | What **latency budget** can the chosen stack actually hit end-to-end, and is it within the ~500 ms–1 s natural band? | Stivers threshold vs pipeline reality |
| 6 | How is **avatar realism styled** to avoid the uncanny valley while staying on-brand? | Uncanny-valley evidence |
| 7 | What is the **efficacy measurement plan** (ground-truth benchmark + pre/post CEFR) that lets Berlitz claim outcomes credibly? | Evaluation framework; market's evidence gap |

---

## Sources

### Internal (Berlitz)

- Repo: [`ai-tutor-architecture.md`](../../../engineering/design/plans/ai-tutor-architecture.md), [`feature-matrix.md`](../../../engineering/design/plans/feature-matrix.md), [`mobile-app-feature-overview.md`](../mobile-app-feature-overview.md), [`berlitz-platform-vision.md`](../../strategy/vision/berlitz-platform-vision.md), [`competitive-matrix.md`](../../competitive-research/competitors/competitive-matrix.md), [`berlitz-simulator.md`](../../strategy/plans/berlitz-simulator.md)
- SharePoint: "Replacing Talkio — Building an In-House AI Speaking Tutor (Build vs Buy)" and `features.md` (R. Zinkov, Jun 2026); `berlitz_cost_model_v0.2.8.xlsx`
- Teams: [Chayan Roy on MVP scope / micro-lessons + AI avatar (Jun 3 2026)](https://teams.microsoft.com/l/message/19%3Af71cdc778be34691bd49246961bbe270%40thread.v2/1780489797958?context=%7B%22contextType%22%3A%22chat%22%7D); [Chayan Roy on lessons flowing into AI practice (Jun 4 2026)](https://teams.microsoft.com/l/message/19%3A3d18f9512f164dd0a1fc5950b43f1088%40thread.v2/1780501119568?context=%7B%22contextType%22%3A%22chat%22%7D); [Jan Hoffmann on avatar cost / "26k" (May 18 2026)](https://teams.microsoft.com/l/message/19%3A447b3fe6-0ec1-4829-a217-3239d61f58f9_af3e2b0f-ddcb-4653-8dad-a5f543fdb637%40unq.gbl.spaces/1779112123525?context=%7B%22contextType%22%3A%22chat%22%7D)

### Learning science
VanLehn 2011 (https://doi.org/10.1080/00461520.2011.611369) · Bloom 1984 (https://doi.org/10.3102/0013189X013006004) · Kulik & Fletcher 2016 (https://doi.org/10.3102/0034654315581420) · Krashen 1982/1985 (https://www.sdkrashen.com/content/books/principles_and_practice.pdf) · Swain & Lapkin 1995 (https://en.wikipedia.org/wiki/Comprehensible_output) · Li 2010 (https://doi.org/10.1111/j.1467-9922.2010.00561.x) · Lyster & Saito 2010 (https://doi.org/10.1017/S0272263109990520) · Lyster & Ranta 1997 (https://doi.org/10.1017/S0272263197001034) · Ellis & Sheen 2006 (https://doi.org/10.1017/S027226310606027X) · Cepeda et al. 2006 (https://doi.org/10.1037/0033-2909.132.3.354) · Bahrick et al. 1993 (https://doi.org/10.1111/j.1467-9280.1993.tb00571.x) · Roediger & Karpicke 2006 (https://doi.org/10.1111/j.1467-9280.2006.01693.x) · Hu & Nation 2000 (https://nflrc.hawaii.edu/rfl/) · CEFR (https://www.coe.int/en/web/common-european-framework-reference-languages)

### Pedagogical agents, multimedia, uncanny valley
Lester et al. 1997 (https://doi.org/10.1145/258549.258797) · Schroeder, Adesope & Gilbert 2013 (https://doi.org/10.2190/EC.49.1.a) · Mayer & DaPra 2012 (https://doi.org/10.1037/a0028616) · Davis 2018 (https://doi.org/10.1016/j.edurev.2018.05.002) · Mayer 2014 (https://doi.org/10.1017/CBO9781139547369.017) · Mayer & Fiorella 2014 (https://doi.org/10.1017/CBO9781139547369.015) · Mori 1970/2012 (https://doi.org/10.1109/MRA.2012.2192811) · Mathur & Reichling 2016 (https://doi.org/10.1016/j.cognition.2015.09.008) · MacDorman & Chattopadhyay 2016 (https://doi.org/10.1016/j.cognition.2015.09.019)

### CAPT / pronunciation
Mahdi & Al Khateeb 2019 (https://doi.org/10.1002/rev3.3165) · O'Brien et al. 2018 (https://doi.org/10.1075/jslp.17001.obr) · Rogerson-Revell 2021 (https://doi.org/10.1177/0033688220977406)

### Avatar / voice / speech tech
Stivers et al. 2009, PNAS (https://www.pnas.org/doi/10.1073/pnas.0903616106) · Tavus docs/pricing (https://docs.tavus.io / https://www.tavus.io/pricing) · HeyGen (https://developers.heygen.com/docs/pricing) · D-ID (https://www.d-id.com/ai-agents/) · Simli (https://docs.simli.com) · Deepgram Nova-3 (https://deepgram.com/learn/introducing-nova-3-speech-to-text-api) · OpenAI gpt-realtime (https://openai.com/index/introducing-gpt-realtime/) · OpenAI audio models (https://openai.com/index/introducing-our-next-generation-audio-models/) · ElevenLabs (https://elevenlabs.io/docs/overview/models) · Cartesia (https://docs.cartesia.ai/api-reference/tts/tts) · Azure Pronunciation Assessment (https://learn.microsoft.com/azure/ai-services/speech-service/how-to-pronunciation-assessment) · MuseTalk (https://github.com/TMElyralab/MuseTalk) · LivePortrait (https://github.com/KwaiVGI/LivePortrait)

### Market / competitors
Speak Series C (https://www.speak.com/blog/series-c) · Praktika Series A, TechCrunch 2024-05-22 (https://techcrunch.com/2024/05/22/praktika-raises-35-5m-to-use-ai-avatars-to-make-learning-languages-feel-more-natural/) · Praktika (https://praktika.ai/) · Duolingo Max (https://blog.duolingo.com/duolingo-max/) · Duolingo overview/efficacy (https://en.wikipedia.org/wiki/Duolingo) · Khan Academy (https://en.wikipedia.org/wiki/Khan_Academy) · Sal Khan (https://en.wikipedia.org/wiki/Sal_Khan) · Khan Academy PNAS 2026 (https://www.pnas.org/doi/10.1073/pnas.2507708123) · World Bank Nigeria GPT-4 tutoring study (https://documents.worldbank.org/en/publication/documents-reports/documentdetail/099548505302533326)
