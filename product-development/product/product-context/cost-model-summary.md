# Cost Model Summary

> **Status:** Living reference
> **Last Updated:** 2026-06-21
> **Source:** `strategy/business-context/berlitz_cost_model_v0.2.8.xlsx`
> **Used by:** AI Conversation Experience PRD, AI Avatar PRD, Practice Drills PRD

This summarizes how AI session costs compose across tiers. PRDs reference this doc for cost numbers rather than restating them inline. For the full model with assumptions and sensitivity analysis, see the source spreadsheet.

---

## Per-Session Cost Components

| Component | Vendor | Cost | Applies to |
|-----------|--------|------|-----------|
| LLM (conversation) | Claude Sonnet | 0.055 EUR/session (10k tokens) | Conversation sessions only |
| ASR | Deepgram Nova | 0.017 EUR/session (4.5 min user speech) | Conversation + drills |
| TTS | Azure Neural | 0.028 EUR/session (4.5 min AI speech) | Conversation sessions only |
| Pronunciation scoring | Azure | 0.021 EUR/session (4.5 min user speech) | Conversation + drills |
| Avatar render (Simli) | Simli Trinity-1 | 0.01 EUR/min (0.276 EUR/30-min session) | Avatar mode, Plus-Career tiers |
| Avatar render (HeyGen) | HeyGen LiveAvatar Lite | 0.10 EUR/min (2.76 EUR/30-min session) | Avatar mode, Premium-Enterprise tiers |
| Human teacher session | Berlitz instructors | 8.60 EUR/session | Human sessions (not AI) |

---

## Composite Cost per Session by Tier and Mode

| Mode | Components | Cost per session | Tiers |
|------|-----------|-----------------|-------|
| **Drill** (1-5 min) | ASR + pronunciation scoring | ~0.038-0.078 EUR [~] | All tiers (Free included) |
| **Conversation, audio-only** (15 min) | LLM + ASR + TTS + pronunciation | ~0.121 EUR | Plus and above |
| **Conversation, avatar (Simli)** (15 min) | Conversation + Simli render | ~0.397 EUR [~] | Plus, Pro, Career |
| **Conversation, avatar (Simli)** (30 min) | Conversation + Simli render | ~0.507 EUR [~] | Plus, Pro, Career |
| **Conversation, avatar (HeyGen)** (15 min) | Conversation + HeyGen render | ~1.621 EUR [~] | Premium, Enterprise |
| **Conversation, avatar (HeyGen)** (30 min) | Conversation + HeyGen render | ~2.991 EUR [~] | Premium, Enterprise |
| **Human session** (45 min) | Teacher time | ~8.60 EUR | Pro and above |

---

## Key Ratios

- Avatar render is **55-92%** of total AI session cost for paid tiers
- Audio-only conversation is **6.5x cheaper** than avatar (Simli) for the same session
- Drills are the cheapest AI practice: ~0.078 EUR/session for free tier
- Human sessions are ~70x the cost of an AI conversation session

---

## Cost Guardrails (from PRDs)

| Guardrail | Threshold | Owner PRD |
|-----------|-----------|-----------|
| Cost per drill session (free tier) | <=0.08 EUR | Practice Drills |
| Cost per drill session (paid tiers) | <=0.15 EUR | Practice Drills |
| Avatar render cost/min (Plus-Career) | <=0.01 EUR/min | AI Avatar |
| Avatar render cost/min (Premium-Enterprise) | <=0.10 EUR/min | AI Avatar |
| Avatar render cost must not exceed 1.5x tier target for >24h | Alert + investigate | AI Avatar |

---

## Notes

- All costs are marginal (per-session). Fixed costs (engineering, infrastructure) are not included
- Currency: EUR unless marked otherwise. USD conversions are approximate
- Session durations are assumptions: drills 1-5 min, conversations 15 min (default) or 30 min, human sessions 45 min
- [~] marks estimated values that depend on actual session duration and usage patterns
