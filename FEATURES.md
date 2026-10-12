# Pulse v3: feature brainstorm and build map

Sources studied from real captures (reference board: `reference/index.html`, kept local, not published):
Mercury public demo (9 screens, light mode), Ramp home + Intelligence, Function Health home + How it works, Oura app (Today / Vitals / My Health from Oura's own redesign posts), Superpower home + product shots.

Legend: **Built** = working in v3. **Partial** = working with a simplified engine. **Next** = not built, worth doing.

---

## 1. Function Health → the employee skeleton

| What they do really well | Pulse feature | Status | Where |
|---|---|---|---|
| Cream canvas, serif display with one italic accent word, mono uppercase step labels | Whole employee visual system: Newsreader serif, terracotta italic accent, `label` mono style | Built | Every `/me` page, landing |
| Category rows: icon, name, tiny in/out-of-range bar, chevron | **Systems** list with count bar + letter grade | Built | My Health |
| Biomarker card: name, "In Range 84 mg/dL", one plain-English line, range ladder (ABOVE / IN / BELOW RANGE) with dated dots | **Metric detail template** for every marker (11 labs + 7 wearable) with Function-style range ladder and dated draws | Built | `/me/metric/:id` |
| "Tracked for life", retest every 3 to 6 months | Lab history with multiple draws; "labs are 10 months old, retest is covered" prompt; marking bloodwork done adds a new draw that improves if a related protocol is active | Built | My Health, Rewards |
| "Bring your results wherever you go" (doctor, Claude, ChatGPT) | **Share with your doctor** export (CSV of every marker, status, date) | Partial | My Health header |
| Summary by category with in-range counts | Optimal / In range / Out of range tiles + segmented bar | Built | My Health summary |

## 2. Oura → design language and the daily loop

| What they do really well | Pulse feature | Status | Where |
|---|---|---|---|
| Three-tab model: Today / Vitals / My Health | Same three, plus Protocols, Rewards, Wallet | Built | Top nav + mobile tab bar |
| Atmospheric hero tinted by context, arc gauge 0-100, one big number, state word, serif headline, one supportive paragraph | **Today hero**: sky tinted by your local time (morning, afternoon, evening, night), Pulse Score arc, state word, tone-aware headline and body | Built | `/me` |
| Score chips row (Readiness, Sleep, Activity...) | Readiness, Sleep, Activity, Stress chips | Built | Today |
| "Morning Focus: one big thing" | **One big thing** card chosen by rules and weighted by your focus areas (rest day, close to a weekly reward, bloodwork due, active protocol, discovery) | Built | Today |
| Vitals with value + state word + baseline slider | Vitals rows with **personal baseline** ranges (HRV range built from your own 90 days) | Built | `/me/vitals` |
| Score contributors | Readiness / Sleep / Activity cards with contributor bars | Built | Vitals |
| My Health sentences: "resilience is **solid**, and down a bit" over a dotted line | **A focus on the journey**: 4 sentence insights, last 30 vs prior 30 days | Built | My Health |
| Discoveries from tags | **Discoveries** computed from real correlations in the person's data (steps→sleep, workouts→next-day HRV, weekend sleep gap, sleep→next-day steps) with sample size | Built | Today, My Health |
| Cumulative stress / burnout awareness | **Cumulative stress** marker (HRV below baseline + RHR above + sleep debt, 2 weeks) | Built | Vitals, Stress system |
| What Oura users hated: font sprawl, low contrast, extra taps, hidden data | Two type families only, no hover menus over data, everything expanded by default | Built | Global |

## 3. Superpower → numbers and visualization

| What they do really well | Pulse feature | Status | Where |
|---|---|---|---|
| One central score + biological age front and center | **Pulse Age** with the top drivers in +/- years and an honest "estimate, not a diagnosis" line | Built | My Health |
| Letter-grade systems (Heart A) | A-D grades per system, computed from marker status | Built | Systems list, system page |
| Status pills (Optimal / Normal / Out of range) + sparkline history per row | Marker rows: status, value, gradient range bar with your marker, sparkline | Built | System pages |
| Gradient range bars that signal without alarm | `RangeBar` with soft red / sage / green zones | Built | Everywhere |
| Protocol card: "High priority · Optimize Heart Health", how you might be feeling, affected biomarkers, Start protocol | **Protocols** generated from your out-of-range markers (heart, vitamin D, sleep, stress, movement, metabolic), with feelings, affected markers, 3 steps, linked reward | Built | `/me/protocols`, metric pages |
| Protocol in progress | Daily checklist, day X of Y, adherence %, confetti when today is done, actions that jump to the wallet | Built | Protocols, Today |
| Kin AI that knows your labs | **Ask Pulse** answers from your own markers, trends, rewards and wallet | Built | ⌘K / Ask button |

## 4. Mercury → employer layout and calm

| What they do really well | Pulse feature | Status | Where |
|---|---|---|---|
| Quiet home: greeting, verb pills, one hero number with area chart, modules with "View >" | Employer Home: Invite / Sync payroll / Review / Ask / Export pills, Program health hero with metric toggle, Needs-you module, Team, This month, Team health | Built | `/employer` |
| Customize home | Show or hide modules, persisted per company | Built | Home → Customize |
| Tasks: one inbox, one sentence per item, bold entities | **Needs you** inbox with inline Approve / Decline and a Completed tab | Built | `/employer/inbox` |
| Command: "Let's cross off some to-dos" + one input + prompt chips | **Ask** page, same layout, takes real actions after confirmation | Built | `/employer/ask` |
| Team Spend: segmented budget bar + Review required + table with % rings | **Program** (budget bar, review card, benefits table) and **Team** (status bar, review card, table with earning rings) | Built | `/employer/program`, `/employer/team` |
| Insights: plain-English trends with inline data chips beside the chart, "may include inaccuracies" | **Insights** with 4 narrative trends, metric toggle chart, disclaimer, team health signal, goal performance | Built | `/employer/insights` |
| Public demo you can click before signing up | Landing → one-click employee or employer demo | Built | Landing |

## 5. Ramp → automation for low-time admins

| What they do really well | Pulse feature | Status | Where |
|---|---|---|---|
| "Your policy, auto-enforced." | **Automations**: 7 rules with toggles and thresholds (auto-invite from payroll, auto-approve under $X with receipt, monthly wallet funding, device nudges, recovery week ask/auto, offboarding, Monday digest) | Built | `/employer/automations` |
| "Approves when it's safe. Escalates when it's not." | Reimbursements under the limit approve instantly (employee sees "Approved automatically"); over-limit or no-receipt items land in Needs you | Built | Benefits → Reimbursement, Needs you |
| "Agents at work today" live counters | **Pulse at work this month** ticker + actions count + hours saved | Built | Employer Home, Automations, Needs you banner |
| "Answers 'is this in policy?' with a text" | **Is this covered?** check (wallet) and Ask eligibility answers (IRS 213(d)-style rules) | Built | Wallet, Ask |
| Run log / audit trail | Run log of every automated action | Built | Automations |
| Payroll as the source of truth | Simulated Gusto / Rippling / Justworks / Deel connect; Sync pulls new hires and invites them | Partial (simulated) | Settings, Onboarding |

## 6. Voice and personalization (cross-cutting)

| Feature | Status | Notes |
|---|---|---|
| Tone of voice: Coach / Calm / Straight talk, changes every headline and body on Today | Built | Chosen in onboarding, editable in Profile |
| Focus areas (Sleep, Stress, Fitness, Long-term health) reorder the one big thing | Built | Onboarding + Profile |
| **Play your brief**: 30-second spoken summary (score, sleep, HRV, rewards, one thing) | Built | Web Speech synthesis, voice picker in Profile |
| Mic input in Ask, spoken answer when you asked by voice | Built | Web Speech recognition (Chrome, Safari, Edge) |
| Sky tinted by local time of day | Built | Today hero |
| Employer priorities (retention, burnout, cost, recruiting) reorder Home modules | Built | Onboarding + Settings |
| Monday digest preview, listenable | Built | Automations → Digest → Preview |
| Briefing schedule (morning / evening) actually delivered as a push | Next | Needs a backend + notifications |
| LLM-backed Ask instead of the rule-based intent engine | Next | Current engine is deterministic and grounded; swap in a model with the same data context |

## 7. Not built yet (ranked)

1. Real wearable + claims integrations (Terra / Vital for devices, a claims feed for preventive verification).
2. LLM Ask with tool-calling over the same functions Ask already uses (approve, invite, set wallet, start protocol).
3. Push notifications for the brief, protocol nudges and Needs-you items.
4. Clinician review layer on protocols (Superpower's "Approved by Dr.").
5. Real Slack digest channel.
