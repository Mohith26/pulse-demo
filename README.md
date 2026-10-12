# Pulse

Health benefits your team will actually use.

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
