# Pulse

Health benefits your team will actually use.

**Versions:** v3 (Function + Oura + Superpower for employees, Mercury + Ramp for employers) at `/`. v2 (Linear + Duolingo) at `/v2/`. v1 (original build) at `/v1/`. Each keeps its own browser state. See `FEATURES.md` for what was taken from each reference and where it lives.

Pulse is a benefits platform for high-growth teams that unifies three things no one else connects: ICHRA plan administration, a flexible wellness wallet, and real financial rewards for the healthy habits employees already track on their wearables.

## What this is

A fully interactive product demo. Every workflow works end to end:

- Employer signup, five-step program setup (company, budget, rewards, invites, launch)
- Invite codes that gate employee signup and prefill their details
- Employee onboarding (connect device, pick goals, choose a plan)
- Live goal evaluation from biometric data, weekly progress, streaks, tiers
- Wellness wallet with a bookable marketplace, balance tracking, and transaction history
- Preventive care completion with attestation and instant reward credit
- Reasonable alternative standard requests (HIPAA wellness rule compliance)
- Employer dashboard with device adoption, population trends, preventive care, and activity feed
- Aggregate burnout signal detection with recovery-week and wellness-day actions
- Incentive builder with live cost projection and HIPAA 30% safe-harbor check
- Insights with retention cohorts, an adjustable ROI model, goal performance, and benchmarks
- Team management, settings, profile, reward routing preferences, device permissions

## What is synthetic

Health plan data, wearable biometrics, vendor bookings, and claims verification are generated locally. The data layer is a single `db` object backed by `localStorage`; swap it for an API client and the rest of the app does not change.

## Demo accounts

| Role | Email | Password |
| --- | --- | --- |
| Employer | alex@acmelabs.com | demo |
| Employee | sarah@acmelabs.com | demo |

Or click "Open as employer" / "Open as employee" on the landing page.

## Run locally

Open `index.html` in a browser, or serve the folder with any static server.

## Stack

Single HTML file. React 18, Tailwind, Babel standalone. No build step.

## v2 design system

- Semantic tokens on CSS variables (Geist-style 10-step gray, one accent), light and dark, follows system, toggle persisted
- Inter 13px app type, JetBrains Mono for codes, timestamps, chart values and keyboard hints
- `Tabs` primitive: WAI-ARIA tablist/tab/tabpanel, roving tabindex, arrow/Home/End keys, active tab background merges into the panel, overflow scroll with edge fade
- `Segmented` radiogroup with arrow keys
- Command palette (Cmd/Ctrl+K) for navigation, actions and demo role switching; `/` focuses search; Enter advances wizards; Esc closes
- Duolingo loop: daily quests, week strip, streak chip, monthly badge quest, tier ladder, progress-over-perfection copy
- Employer scaling: program score, setup checklist, privacy lock under 5 connected, Team tabs/filters/sort/pagination

## Changelog

### v3
- Employee app rebuilt on Function Health's skeleton (cream canvas, serif display, range ladders with dated draws, systems list), Oura's language (Today / Vitals / My Health, atmospheric hero tinted by local time, arc gauge, baseline sliders, sentence insights) and Superpower's numbers (Pulse Age, letter-grade systems, status pills + sparklines, protocols).
- New engine: 11 synthetic lab markers with history, 7 wearable markers with personal baselines, systems + grades, Pulse Score, Pulse Age, real correlation-based Discoveries, cumulative stress, protocols with daily check-ins.
- Employer app rebuilt on Mercury's layout (quiet home, verb pills, Needs-you inbox, Command-style Ask, Team Spend tables, narrative Insights) and Ramp's automation model (7 rules, auto-approve under a limit, escalation, live "Pulse at work" counters, run log, hours saved).
- Voice and personalization: tone (Coach / Calm / Straight talk), focus areas, spoken daily brief, mic input in Ask with spoken answers, employer priorities that reorder Home, listenable Monday digest.
- Ask Pulse (both sides): grounded intent engine that answers from live data and takes confirmed actions (approve, invite, set wallet, recovery week, nudge, export).
- Light by default, full dark theme, mobile tab bars on both sides.

### v2
- Linear styling + Duolingo UX redesign. See `AUDIT.md`.

### v1
- Original end-to-end build.
