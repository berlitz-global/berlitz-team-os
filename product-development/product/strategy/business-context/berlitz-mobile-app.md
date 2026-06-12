# Berlitz Mobile App

**Source:** Teams message (launch planning)
**Last Updated:** 2026-06-10

## Objective

Launch a mobile app based on credits, so we can learn from the market on what does good look like.

## Assumptions

- Stripe and Netsuite are payments gateway
- Packages are managed in Metronome; metering also is in Metronome
- Only implementing "use it or lose it" credit management — every month (aside from free) credits get refilled based on date of purchase (e.g., 18th July purchase → new credits on 18th August)
- iOS and Android launch together

## Conversion Scenario Matrix — India & Chile (1k signups/downloads)

| Conv Rate | Paid Users | Revenue | AI Cost | Teacher Cost | Total Cost | Net P&L | Plus LTV | Pro LTV | Verdict |
|-----------|-----------|---------|---------|--------------|------------|---------|----------|---------|---------|
| 5% | 50 | $636 | $2.1k | $62 | $2.3k | -$1.7k | $135 | $375 | At risk |
| 10% | 100 | $1.3k | $2.2k | $125 | $2.6k | -$1.3k | $135 | $375 | At risk |
| 12% | 120 | $1.5k | $2.3k | $150 | $2.7k | -$1.2k | $135 | $375 | At risk |
| **15%** | **150** | **$1.9k** | **$2.3k** | **$187** | **$2.8k** | **-$928** | **$135** | **$375** | **At risk** |
| 18% | 180 | $2.3k | $2.4k | $225 | $3.0k | -$704 | $135 | $375 | At risk |
| 20% | 200 | $2.5k | $2.4k | $250 | $3.1k | -$554 | $135 | $375 | At risk |
| 25% | 250 | $3.2k | $2.5k | $312 | $3.4k | -$181 | $135 | $375 | Near break-even |
| 30% | 300 | $3.8k | $2.6k | $374 | $3.6k | $193 | $135 | $375 | Viable |

## Authentication & Onboarding (both markets, all tiers)

- Single sign-on, email signup, and Google auth
- 5-minute AI placement test (writing, speaking, reading) → places learner at A1–C2
- Goal selection: career, travel, exam, business
- Language selection:
  - **India:** English, German, Spanish (okay if just English)
  - **Chile:** English, German, Spanish (okay if just English)
- Personalised learning path generated from placement + goal — must take under 3 minutes from install to first lesson or you lose half your installs before they start

## Free Tier — the non-negotiables

AI Practice (voice-first) is the entire value proposition of the Free tier. If this doesn't work flawlessly on a mid-range Android handset in India with a patchy 4G connection, nothing else matters. (We need to look at local voice models for this reason.)

**Included:**

- Voice recognition, real-time pronunciation feedback, and natural conversation flow
- Offline mode for AI practice (not optional for India — essential)
- Streak tracking with daily notification
- Home screen showing one clear action: "practice today"
- Progress level display (A1–C2)
- Vocabulary review module; lesson plan similar to MyBerlitz
- Basic settings with upgrade flow (subscriptions), downgrade, and cancel

**Not needed at launch:** social features, leaderboards, group classes, referrals, content library browsing, settings complexity.

## Plus Tier — $19/month or Rs 999/month

Everything in Free, plus:

- AI Tutor structured session experience — goal-oriented 30-minute lesson with a clear objective (key differentiator from Free; can use structure of existing MyBerlitz product)
- Credit wallet showing balance (2 credits/month)
- Credit top-up purchase (buy extra credits in-app)
- Progress metrics / analytics — very high level (need to define what good looks like)
- Certifications (nice to have)

## Pro Tier — $49/month or Rs 1999/month

Everything in Plus, plus human teacher booking. This is where build complexity jumps significantly.

- Student availability calendar
- Booking confirmation flow (a slot is given, user can accept or reject it)
- Video session integration (Zoom embed)
- Post-session rating (eCFF 3-question flow)
- Session history
- For past video: transcript of the class and notes connected to it
- Teacher profile page — name, languages, 30-second video intro, rating (enough for launch)
- Progress metrics / analytics — very high level (need to define what good looks like)
- Certifications (nice to have)
- Credit balance showing 6 credits, which sessions cost how many credits, and a clear top-up path

## Infrastructure — must work before launch (all tiers)

- Stripe subscription management (signup, billing, cancellation)
- Metronome credit balance API feeding into the app wallet
- Push notifications (daily practice reminder is the single highest-impact retention mechanic)
- App Store and Google Play compliance for both markets — India has specific data localisation considerations
- Hindi localisation for India, Spanish for Chile (nice to have)
- GDPR-equivalent compliance — India's DPDPA is now in force
