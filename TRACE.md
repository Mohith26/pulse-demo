# Pulse: original spec → what's built (as of v3.1)

Status: **Done** works in the demo · **Partial** some of it · **Simulated** real-looking, fake data or integration · **Missing** not built · **Needs accounts** blocked on real third-party access.

## 7 core features
| Feature | Status | Notes |
|---|---|---|
| Wearable data platform | **Partial** | Real Apple Health export (zip/xml) and CSV import, parsed in the browser: per-source step dedup, sleep stitched across midnight, gap fill, per-metric availability. Live device APIs (Oura/WHOOP/Garmin/Fitbit/Terra) **Needs accounts**. Fraud detection **Missing**. |
| Incentive engine | **Done** | Goal library (8 + classes, commute, meals), employer config, HIPAA 30% guardrail, weekly verification, automatic alternatives, recovery-week thresholds. Tax classification and payroll export **Missing**. |
| ICHRA administration | **Simulated** | Plan choice, contribution, reimbursements with auto-approve. Real ICHRA partner (Thatch / Take Command / Gravie) **Needs accounts**. |
| Privacy & consent | **Done (client-side)** | Consent step with per-type sharing, toggles that actually hide data and remove you from averages, min group 5, audit log, employee access log, download my data, delete my data, retention setting, deletion certificates. Encryption/SOC 2 need a real backend. |
| Employer analytics | **Done** | Engagement, trends, burnout signal + detail page, retention (before/after, connected vs not), satisfaction/NPS, benchmarks, ROI from retention, board report (PDF). |
| Employee experience | **Done** | Today, Vitals, My Health, metric pages, protocols, Care, rewards, wallet, benefits, Ask, voice. |
| Onboarding | **Done** | Employer 5 steps (with turnover baseline), employee 7 steps (with consent and real-data import). Payroll **Simulated**. |

## 9 workflows
| # | Workflow | Status |
|---|---|---|
| 1 | Employer setup | Done (payroll simulated) |
| 2 | Employee enroll + connect | Done, with consent screen and real-data import |
| 3 | Earning loop | Done (tax/payroll export missing) |
| 4 | Alternative standard | **Done to spec**: employee picks, same reward, employer never involved or told |
| 5 | Employer reviews population health | Done, plus board report |
| 6 | Preventive verification | Done: claims match (simulated feed), document upload, self-report with spot-check note |
| 7 | Offboarding | Done: final rewards, wallet return, reimbursements end, plan stays theirs, removed from aggregates, deletion after retention window, certificate. Auto-offboard from payroll termination. |
| 8 | ICHRA → self-insured | **Partial**: stage page, readiness checks, person-months, carrier report. Actual level-funded/TPA mode **Missing**. |
| 9 | Burnout detection | Done: computed signal, detail page with history, actions, private employee alert, opt-in manager check-in |

## 12 lifestyle features
| # | Feature | Status |
|---|---|---|
| 1 | Wellness wallet | Done |
| 2 | Marketplace with group rates | Done (list vs Pulse rate, tier discount) |
| 3 | Bloodwork as benefit | Done |
| 4 | Therapy direct access | Done: Care directory, filters, booking, 988 line |
| 5 | Sleep score rewards | Done (4-week bonus missing) |
| 6 | Private burnout alert | Done |
| 7 | Class credits + class reward | Done |
| 8 | Nutrition score on meals | Partial: wallet meals carry a score and count toward a meals reward. Company meal-order integration (DoorDash) **Needs accounts** |
| 9 | Active commute rewards | Done (from step data on Tue to Thu) |
| 10 | Supplement guidance | Done for vitamin D |
| 11 | Team challenges | Done: opt-in, team averages, min 5 per team, employer creates |
| 12 | Annual value visualization | Done, with used vs ahead |

## Strategy items now in the product
- Locked one-liner on the landing page.
- Participation guarantee (50% floor at month 6) on landing, employer Settings and Ask.
- Closed loop: "Pulse suggests" recommendations that change policy in one click.
- "Grows with you" page.

## Still needs your decision or accounts
1. Hosted backend + real auth (data currently lives in each browser).
2. Live wearable APIs (Terra or Vital is one integration for all devices; paid).
3. ICHRA partner and real payroll (Gusto/Rippling developer access).
4. Clinician review layer for protocols.
5. Legal/privacy counsel review of consent copy and incentive design.
