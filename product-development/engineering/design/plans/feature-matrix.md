# Berlitz Learner App - Feature Matrix

**Created:** 2026-06-07
**Purpose:** Feature-level breakdown across 4 viewpoints with MVP scope and evolution path

## Viewpoint Key

| Tag | Viewpoint | Core Question |
|-----|-----------|---------------|
| **BIZ** | Berlitz (business) | Can we monetize, operate, and scale? |
| **STU** | Student (learner) | Is the learning real, engaging, and worth paying for? |
| **ENT** | Enterprise (B2B buyer) | Can I manage teams, prove ROI, and integrate with my systems? |
| **TCH** | Teacher (instructor) | Can I teach effectively without wasting time on admin? |

## MVP Definition

"MVP Required" = must ship to charge money and deliver a credible learning product. Without it, either we can't bill, the learner gets nothing useful, or the product is not differentiated from free alternatives.

---

## A. Onboarding & Identity

| # | Feature | MVP? | V1.0 Scope | Improvements & Extensions | Viewpoints |
|---|---------|------|-----------|---------------------------|------------|
| A1 | Sign-up / Login | Yes | Email + password; social login (Google, Apple) | Add SSO/SAML for enterprise; MFA; biometric login on mobile | BIZ, STU, ENT |
| A2 | Placement Test | Yes | 10-15 min CEFR placement (listening + reading + speaking sample); assigns A1-B2 level | Add writing assessment; granular sub-skill placement (grammar vs vocabulary vs pronunciation); adaptive test length | STU, TCH |
| A3 | L1/L2 Selection | Yes | Select native language and target language (English at launch) | Multi-language support (Spanish, German, Japanese); simultaneous study of multiple languages | STU, BIZ |
| A4 | Learning Goal Setting | Yes | Choose goal: general fluency, business English, travel, exam prep | Custom goals; goal-linked curriculum paths; enterprise-defined goals (e.g., "all team members to B1 in 6 months") | STU, ENT |
| A5 | Enterprise Enrollment | No | -- | Invite-link or SSO-based enrollment; admin assigns tier and credit pool; bulk onboarding CSV import; SCIM provisioning | ENT, BIZ |

---

## B. AI Tutor - Audio-Only Mode (Drills)

| # | Feature | MVP? | V1.0 Scope | Improvements & Extensions | Viewpoints |
|---|---------|------|-----------|---------------------------|------------|
| B1 | Pronunciation Drills | Yes | Listen to native audio, repeat word/phrase, get pass/fail pronunciation score with visual feedback | Phoneme-level scoring with per-sound heatmap; accent comparison; targeted drill generation for weak sounds; IPA display | STU |
| B2 | Vocabulary Drills | Yes | Flashcard-style drill with speech input: see word, say it, get feedback; spaced repetition scheduling | Image association; contextual sentences; vocabulary mastery tracking per word; export to Anki | STU |
| B3 | Grammar Exercises | Yes | Fill-in-the-blank and sentence construction with voice input; instant correction with explanation | Adaptive grammar review targeting error patterns; grammar rule reference cards; contrastive grammar (L1 vs L2) | STU |
| B4 | Listen & Comprehend | No | -- | Audio clips with comprehension questions; dictation exercises; speed adjustment; natural speech (not textbook pace) | STU |
| B5 | Drill Session Summary | Yes | Post-drill summary: words practiced, accuracy rate, pronunciation scores, time spent | Trend charts over time; weak-area recommendations; share summary with teacher | STU, TCH |

---

## C. AI Tutor - Avatar Mode (Conversation)

| # | Feature | MVP? | V1.0 Scope | Improvements & Extensions | Viewpoints |
|---|---------|------|-----------|---------------------------|------------|
| C1 | AI Avatar Character | Yes | Single animated 3D avatar with lip-sync, expressions, and voice; personality consistent with Berlitz brand | Multiple avatar personas (different accents, personalities, cultural backgrounds); avatar customization; scene variety | STU |
| C2 | Guided Conversation | Yes | Scenario-based dialogue following Berlitz curriculum: avatar guides learner through a structured conversation with specific learning objectives (e.g., "order food at a restaurant using polite forms") | Branching scenarios based on learner choices; multi-character scenes; increasing open-endedness as level rises | STU |
| C3 | Open Conversation | No | -- | Free-form conversation on any topic within level constraints; avatar adapts to learner's interests; no fixed scenario script | STU |
| C4 | Role-Play | Yes | Pre-defined role-play scenarios from Berlitz curriculum (job interview, client meeting, hotel check-in); avatar plays one character, learner plays the other | Custom role-play creation; multi-role scenarios; role reversal (learner plays both parts); business-specific role-plays per industry | STU, ENT |
| C5 | Real-Time Grammar Correction | Yes | Avatar gently corrects grammar errors inline during conversation (Berlitz Method: correct without breaking flow) | Post-session grammar report with pattern analysis; link corrections to grammar rules; difficulty-adjusted correction frequency | STU, TCH |
| C6 | Conversation Recording & Playback | No | -- | Record full conversation; replay with avatar animation; highlight corrections; share with teacher for review | STU, TCH |
| C7 | Berlitz Method Compliance | Yes | System prompts enforce: immersive L2 use, question-answer cycles, graduated difficulty, gentle error correction, encouragement patterns | Method compliance scoring per session (internal QA); A/B test method variations; method adaptation per culture/L1 | BIZ, STU |
| C8 | Level-Appropriate Language | Yes | AI tutor output constrained to learner's CEFR level: vocabulary, grammar structures, sentence complexity, speaking speed | Dynamic adjustment within session if learner is struggling or excelling; cross-session level drift detection | STU, TCH |

---

## D. Content Pipeline & Curriculum

| # | Feature | MVP? | V1.0 Scope | Improvements & Extensions | Viewpoints |
|---|---------|------|-----------|---------------------------|------------|
| D1 | PDF Content Ingestion | Yes | Extract structured content from Berlitz instructor + student guide PDFs: lesson goals, vocabulary, grammar, dialog scripts, story outlines | Support for additional content formats (Word, structured JSON); automated re-ingestion on new editions; diff detection for updated content | BIZ |
| D2 | Prompt/Scenario Generation | Yes | LLM transforms structured lesson content into conversation scenarios, pronunciation drills, role-play scripts with vocabulary bounds, grammar focus, and success criteria | Automated quality scoring of generated content; batch generation for new curricula; teacher-contributed scenario seeds | BIZ, STU |
| D3 | Content QA Review | Yes | Human reviewer (pedagogy expert) approves/edits generated scenarios before they go live; reject/revise workflow | Approval rate dashboard; auto-approve for high-confidence content; reviewer workload management; versioned edit history | BIZ |
| D4 | Scenario Library | Yes | Versioned, tagged library of ready-to-use scenarios; filterable by CEFR level, skill type, topic, lesson unit | A/B testing of scenario variants; usage analytics per scenario (completion rate, learner satisfaction); deprecation workflow | BIZ, STU |
| D5 | Business Content Modules | No | -- | Industry-specific scenarios (finance, healthcare, tech, legal); professional skills (presentations, negotiations, email writing); compliance content (EU AI Act, etc.) | STU, ENT |
| D6 | Multi-Language Expansion | No | -- | Extend content pipeline to Spanish, German, Japanese; per-language adaptation of Berlitz Method prompts; L1-specific error pattern libraries | BIZ, STU |

---

## E. Progress & Assessment

| # | Feature | MVP? | V1.0 Scope | Improvements & Extensions | Viewpoints |
|---|---------|------|-----------|---------------------------|------------|
| E1 | Progress Dashboard | Yes | Current CEFR level, lessons completed, vocabulary mastered, streak count, credit balance, time practiced this week | Skills radar (grammar, vocabulary, pronunciation, conversation, listening); trend charts; comparison to peers (anonymized); weekly email summary | STU |
| E2 | Session History | Yes | List of past AI sessions with date, type (drill/conversation), scenario, duration, score summary | Filterable by skill type; re-do a past session; compare scores across attempts; export to PDF | STU, TCH |
| E3 | CEFR Level Tracking | Yes | Display current estimated CEFR level (overall); level-up notification when threshold met | Per-skill CEFR breakdown (grammar: A2, pronunciation: B1, etc.); level progression timeline; level confidence indicator | STU, ENT, TCH |
| E4 | Pre/Post Assessment | No | -- | Formal CEFR test at enrollment and at milestones; measures improvement delta; feeds enterprise ROI dashboards | STU, ENT |
| E5 | CEFR Certificate | No | -- | Downloadable certificate upon completing a CEFR level; Berlitz-branded; human-verified assessment for B1+; verifiable via URL | STU, ENT |
| E6 | Learning Analytics (Learner) | Yes | Basic stats: total sessions, hours practiced, words learned, accuracy trends | Predictive time-to-level-up; recommended focus areas; comparison to learning goals | STU |

---

## F. Human Teaching Integration

| # | Feature | MVP? | V1.0 Scope | Improvements & Extensions | Viewpoints |
|---|---------|------|-----------|---------------------------|------------|
| F1 | Teacher Cockpit | No | -- | Dashboard for teachers: upcoming sessions, learner profiles with AI practice summary, error patterns, readiness signals, suggested focus areas. "The learner practiced ordering food 5 times this week, struggles with subjunctive -- focus your session on that." | TCH |
| F2 | Learner Context Feed | No | -- | Before each human session, teacher sees: recent AI sessions, topics covered, grammar errors, pronunciation weak spots, vocabulary gaps, CEFR level estimate, learner goals | TCH, STU |
| F3 | Session Booking | No | -- | Browse available teachers (filtered by language, specialty, timezone); book using credits; calendar integration; reschedule/cancel | STU, BIZ |
| F4 | AI-Human Handoff | No | -- | AI Tutor suggests "Want to practice this with a real teacher?" when learner hits limits; packages context for teacher; seamless transition | STU, TCH |
| F5 | Teacher Observations | No | -- | After human session, teacher logs observations (level assessment, notes, recommended focus); these feed back into AI Tutor personalization | TCH, STU |
| F6 | AI-Assisted Lesson Prep | No | -- | Before session, teacher gets AI-generated lesson plan based on learner's recent activity, weak areas, and curriculum position. Reduces 10-15 min prep to 2 min. | TCH |
| F7 | Session Continuity | No | -- | Human teacher picks up exactly where AI left off: same vocabulary, same grammar focus, aware of what was practiced. No "first 5 minutes wasted on warm-up." | TCH, STU |
| F8 | Teacher Scheduling Management | No | -- | Teachers manage availability, view upcoming sessions, see utilization %, handle cancellations. Target: 60-65% utilization (vs 45.7% current). | TCH, BIZ |

---

## G. Credits, Billing & Monetization

| # | Feature | MVP? | V1.0 Scope | Improvements & Extensions | Viewpoints |
|---|---------|------|-----------|---------------------------|------------|
| G1 | Subscription Tiers | Yes | Display Free/Plus/Pro/Career/Premium tiers; purchase flow; upgrade/downgrade | Annual billing option; promotional pricing; referral discounts; student/educator discounts | BIZ, STU |
| G2 | Credit Balance & Usage | Yes | Show remaining credits; credit consumption log (which sessions used how many credits); low-balance alert | Usage prediction ("at your pace, credits run out on June 20"); credit top-up option; rollover visibility for mid-market | BIZ, STU |
| G3 | Payment Processing | Yes | Stripe integration: credit card, Apple Pay, Google Pay; subscription billing; receipts | Multi-currency support per launch market; invoice generation for B2B; VAT handling for EU; payment retry logic | BIZ |
| G4 | Free Tier Experience | Yes | Unlimited AI practice (audio-only + avatar); 1 demo AI tutor session; 1 demo human class; credit balance shows "0 remaining" after demos with upgrade prompt | Free tier engagement tracking; conversion funnel analytics; optimized upgrade prompts based on usage patterns | BIZ, STU |
| G5 | Usage Metering | Yes | Metronome integration: track AI session starts, duration, credit consumption in real-time; feed billing system | Cost-per-session analytics for internal margin tracking; usage alerts for enterprise admins; budget forecasting | BIZ, ENT |
| G6 | Enterprise Credit Pools | No | -- | Admin allocates credits per user/team from shared pool; real-time usage visibility; budget controls; overage alerts; monthly usage reports | ENT, BIZ |

---

## H. Engagement & Retention

| # | Feature | MVP? | V1.0 Scope | Improvements & Extensions | Viewpoints |
|---|---------|------|-----------|---------------------------|------------|
| H1 | Daily Streak | Yes | Track consecutive days of practice; display streak count; streak-freeze option (skip 1 day without breaking) | Streak milestones with rewards; streak recovery purchase; social sharing | STU |
| H2 | Push Notifications | No | -- | Daily practice reminder; streak-at-risk warning; session reminder; "Your teacher is available"; weekly progress summary | STU, BIZ |
| H3 | Daily Goal | Yes | Set daily practice goal (5/10/15/20 min); progress ring on home screen | Adaptive goal suggestion based on pace and level; weekly goals; enterprise-set goals | STU, ENT |
| H4 | XP / Points | No | -- | Earn XP for sessions, drills, streaks; XP leaderboard (opt-in); level-up animations | STU |
| H5 | Achievements / Badges | No | -- | Milestone badges (first conversation, 7-day streak, 100 words mastered, first human session); displayable on profile | STU |
| H6 | Social Features | No | -- | Friend connections; practice partner matching; community challenges; share progress | STU |

---

## I. Enterprise Admin & B2B

| # | Feature | MVP? | V1.0 Scope | Improvements & Extensions | Viewpoints |
|---|---------|------|-----------|---------------------------|------------|
| I1 | Admin Dashboard | No | -- | Overview: total enrolled, active learners, credit usage, average CEFR progress, top learners, at-risk learners (low engagement) | ENT |
| I2 | Team Management | No | -- | Create teams/departments; assign learners; set per-team goals; view team-level progress | ENT |
| I3 | Credit Pool Administration | No | -- | Allocate credits from company pool to teams/individuals; real-time usage; budget caps; overage alerts; monthly reports | ENT, BIZ |
| I4 | ROI Dashboard | No | -- | Pre/post CEFR assessment results; time-to-level-up metrics; engagement rates; cost per CEFR level gained; exportable for CFO reporting | ENT |
| I5 | Progress Reports | No | -- | Per-learner and team-level reports: sessions completed, CEFR progress, hours practiced, human sessions used, credit consumption | ENT, TCH |
| I6 | SSO/SAML Integration | No | -- | SAML 2.0 SSO for enterprise identity; IdP-initiated and SP-initiated; auto-provisioning on first login | ENT |
| I7 | SCIM Provisioning | No | -- | Automated user provisioning/deprovisioning synced with enterprise directory (Azure AD, Okta, etc.) | ENT |
| I8 | HRIS Integration (Kombo) | No | -- | Sync employee data from HRIS (Workday, BambooHR, etc.) via Kombo; auto-assign learners to teams based on department/role | ENT |
| I9 | LMS/LTI Integration | No | -- | Export learning data via xAPI/SCORM; LTI launch from enterprise LMS (Cornerstone, Degreed, etc.); completion reporting | ENT |
| I10 | Data Residency & Privacy | No | -- | EU data residency option; GDPR compliance tooling; data export/deletion on request; DPA for enterprise contracts | ENT, BIZ |
| I11 | Compliance Training Content | No | -- | Pre-built compliance modules (EU AI Act, business ethics, anti-bribery) delivered via AI tutor with certification tracking | ENT |

---

## J. Platform & Infrastructure

| # | Feature | MVP? | V1.0 Scope | Improvements & Extensions | Viewpoints |
|---|---------|------|-----------|---------------------------|------------|
| J1 | Web App | Yes | Responsive web app (React); full AI tutor functionality; desktop + tablet | Progressive web app (PWA) with install prompt; keyboard shortcuts for power users | STU, BIZ |
| J2 | iOS App | Yes | Native iOS app (Oct 2026); AI tutor (audio-only + avatar); all core features | Apple Watch companion (daily goal, streak); Siri integration; widget; offline drills | STU |
| J3 | Android App | Yes | Native Android app (Oct 2026); feature parity with iOS | Wearable companion; Google Assistant integration; widget | STU |
| J4 | Multi-Device Sync | Yes | Session state, progress, and preferences synced across web/mobile in real-time | Seamless handoff (start on phone, continue on desktop); sync offline progress when reconnected | STU |
| J5 | Offline Mode | No | -- | Download drills and vocabulary for offline practice (audio-only mode); sync progress when back online | STU |
| J6 | Accessibility | Yes | WCAG 2.1 AA compliance; screen reader support; high-contrast mode; keyboard navigation | Dyslexia-friendly font option; adjustable text size; captioning for all audio | STU, BIZ |

---

## K. Evaluation & Quality (Internal)

| # | Feature | MVP? | V1.0 Scope | Improvements & Extensions | Viewpoints |
|---|---------|------|-----------|---------------------------|------------|
| K1 | Simulation Engine | Yes | Synthetic learner profiles at various CEFR levels; automated session runner; regression tests for model/prompt changes | L1 interference modeling (Japanese, Spanish, Arabic patterns); multi-scenario batch testing; automated nightly test runs | BIZ |
| K2 | Ground Truth Benchmark | Yes | Transcribe and annotate real teacher-learner recordings; build Berlitz Teaching Rubric; score AI sessions against rubric | Expand recording corpus by language/level; inter-annotator reliability scoring; rubric versioning as method evolves | BIZ, TCH |
| K3 | Quality Dashboard | No | -- | Per-scenario, per-level, per-skill quality scores tracked over time; alerting on quality regressions; LLM provider comparison | BIZ |
| K4 | Content Pipeline Metrics | No | -- | Auto-approval rate; reviewer workload; time-to-publish; scenario usage vs quality correlation | BIZ |

---

## Summary: MVP Feature Count by Viewpoint

| Viewpoint | MVP Features | Post-MVP Features | Total |
|-----------|-------------|-------------------|-------|
| STU (Student) | 22 | 28 | 50 |
| BIZ (Berlitz) | 16 | 16 | 32 |
| ENT (Enterprise) | 3 | 18 | 21 |
| TCH (Teacher) | 2 | 10 | 12 |

**MVP total: 30 unique features** (some serve multiple viewpoints)
**Post-MVP total: 35 unique features**

### MVP Features by Area

| Area | MVP Count | Features |
|------|-----------|----------|
| A. Onboarding | 4 | Sign-up, placement test, L1/L2, goal setting |
| B. Audio-Only Drills | 4 | Pronunciation, vocabulary, grammar, drill summary |
| C. Avatar Conversation | 5 | Avatar, guided conversation, role-play, grammar correction, Berlitz Method, level-appropriate language |
| D. Content Pipeline | 4 | PDF ingestion, prompt generation, content QA, scenario library |
| E. Progress | 3 | Dashboard, session history, CEFR tracking, basic analytics |
| F. Human Teaching | 0 | All post-MVP (Differentiator tier) |
| G. Billing | 5 | Tiers, credits, payment, free tier, metering |
| H. Engagement | 2 | Streak, daily goal |
| I. Enterprise | 0 | All post-MVP (Differentiator/Enhancement tier) |
| J. Platform | 5 | Web, iOS, Android, sync, accessibility |
| K. Evaluation | 2 | Simulation engine, ground truth benchmark |
