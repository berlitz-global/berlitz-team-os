# Privacy & Data Requirements

> **Status:** Living reference
> **Last Updated:** 2026-06-21
> **Source:** AI Conversation Experience PRD Section 7
> **Used by:** AI Conversation Experience PRD, Practice Drills PRD, AI Avatar PRD
> **Owner:** Legal + Product

All AI features (conversation, drills, avatar) record, transcribe, and score learner speech. Berlitz operates in the EU (EUR pricing, Germany launch market). These requirements apply to every product that processes learner voice data.

---

## Requirements

| Constraint | Requirement | Owner |
|-----------|------------|-------|
| **Consent for voice recording** | Learner must explicitly consent before their first AI session (conversation or drill). Consent revocable at any time. The consent gate must fire on the first voice-based interaction regardless of entry point - a free-tier learner may reach drills before ever starting a conversation. | Legal + Product |
| **Data retention** | Audio recordings retained max 90 days [~], then auto-deleted. Transcripts retained for learner profile lifetime. Learner can request deletion (GDPR Art. 17). | Legal + Engineering |
| **Human audit access controls** | 10% human audit sample anonymized/pseudonymized. Auditors access transcripts, not raw audio unless needed for pronunciation eval (logged, time-limited). | Legal + Data |
| **GDPR DPIA** | Required before Phase 2 beta - voice biometric data is special category (GDPR Art. 9). | Legal |
| **Data residency** | EU user data processed and stored within the EU. | Engineering + Legal |
| **Launch gate** | Privacy review and DPIA approval are Phase 2 beta entry gates. | Legal |

---

## Product-Specific Notes

- **Curriculum Factory:** Lesson transcripts used for teaching pattern extraction have a 90-day retention limit. Structured extractions persist after source deletion. See Curriculum Factory PRD Section 10.
- **Practice Drills:** Free-tier learners reach drills without a conversation session, so the consent gate must trigger on first drill, not first conversation.
- **AI Avatar:** Avatar sessions record the same voice data as audio-only. No additional privacy requirements beyond what's listed above.
