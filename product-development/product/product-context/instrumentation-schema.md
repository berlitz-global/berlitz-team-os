# Instrumentation Schema

> **Status:** Living reference
> **Last Updated:** 2026-06-21
> **Source:** AI Conversation Experience PRD Section 5, Practice Drills PRD Section 5, AI Avatar PRD Section 5
> **Used by:** All PRDs, Analytics

Single source of truth for event namespaces, payload specs, and derived metrics across all AI products. Each PRD owns its namespace but the schema is documented here to prevent conflicts and enable cross-product analytics.

---

## Event Conventions

- Event names use `snake_case`
- All events carry common fields: `session_id`, `user_id`, `tier`, `cefr_level`, `timestamp`
- Conversation events also carry `mode` (audio_only / avatar)
- Events are streamed to the analytics pipeline. Dependency: Analytics engineering must confirm the event pipeline before Phase 2 beta entry.

---

## Namespace: `ai.*` (AI Conversation Experience)

| Event | Payload (key fields) | Metrics it feeds |
|-------|---------------------|-----------------|
| `ai.session.started` | `scenario_id`, `scenario_type` (guided / role_play), `mode` | Session completion rate, weekly sessions |
| `ai.session.ended` | `end_reason` (goal_reached / time_up / learner_exit / error), `duration_ms` | Session completion rate, return rate |
| `ai.utterance.learner` | `duration_ms`, `transcript`, `asr_confidence` | Speaking time per session |
| `ai.utterance.tutor` | `duration_ms`, `latency_ms` (voice-to-first-audio) | Latency guardrail |
| `ai.correction.delivered` | `correction_type` (grammar / pronunciation / vocabulary), `strategy` (prompt / recast / hint), `learner_response` (self_repair / ignored / n/a) | Berlitz Method compliance |
| `ai.feedback.surfaced` | `feedback_type` (pronunciation_flag / vocab_suggestion / fluency_cue), `severity` | Diagnostic only |
| `ai.scenario.goal_reached` | `scenario_id`, `turns_taken`, `time_to_goal_ms` | Session completion rate |
| `ai.eval.compliance` | `session_id`, `compliance_score`, `violations[]` | Berlitz Method compliance guardrail |

### Derived metrics (conversation)

- **Speaking time per session** = SUM(`ai.utterance.learner.duration_ms`) per `session_id`
- **Session return rate** = COUNT(users with >=2 `ai.session.started` within 7 days) / COUNT(users with >=1)
- **Session completion rate** = COUNT(`ai.session.ended` WHERE `end_reason` IN (goal_reached, time_up)) / COUNT(`ai.session.started`)
- **Latency p95** = PERCENTILE(95, `ai.utterance.tutor.latency_ms`)

---

## Namespace: `drill.*` (Practice Drills)

| Event | Payload | Metrics it feeds |
|-------|---------|-----------------|
| `drill.started` | `drill_type` (pronunciation / vocabulary / grammar), `cefr_level`, `tier` | Drill completion rate, weekly sessions |
| `drill.completed` | `items_total`, `items_completed`, `accuracy_rate`, `duration_ms` | Drill completion rate |
| `drill.pronunciation.scored` | `phoneme_scores[]`, `word`, `confidence`, `overall_score` | Pronunciation accuracy guardrail |
| `drill.vocabulary.reviewed` | `word_id`, `srs_interval`, `outcome` (correct / incorrect) | SRS effectiveness |
| `drill.abandoned` | `items_completed`, `items_total`, `abandon_reason` (if detectable) | Drill completion rate |

### Derived metrics (drills)

- **Drill completion rate** = COUNT(`drill.completed`) / COUNT(`drill.started`)
- **Weekly drill sessions per WAU** = COUNT(`drill.started`) per user per week

---

## Namespace: `avatar.*` (AI Avatar)

| Event | Payload | Metrics it feeds |
|-------|---------|-----------------|
| `avatar.render.started` | `avatar_vendor`, `avatar_config` (appearance, dialect) | Avatar adoption rate, cost |
| `avatar.session.cost` | `avatar_render_cost` | Cost per minute by tier |
| `avatar.session.feedback` | `appearance_natural` (boolean), `appearance_rating` (1-5), `free_text` | Uncanny valley guardrail |

### Derived metrics (avatar)

- **Avatar adoption rate** = COUNT(`ai.session.started` WHERE mode=avatar) / COUNT(`ai.session.started` WHERE tier IN paid_tiers)
- **Uncanny valley rate** = COUNT(WHERE `appearance_natural` = false) / COUNT(WHERE `appearance_natural` IS NOT NULL)
