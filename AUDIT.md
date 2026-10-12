# Pulse UI/UX Audit and Redesign Spec (v1 to v2)

Lens: Linear styling + Duolingo UX, for a health benefits platform sold to small, fast-moving tech startups. Every finding is graded against three questions: does it feel like a tool engineers and designers already use (Slack, Notion, Linear, Vercel); does it make healthy behavior feel rewarding with near-zero cognitive load; does the layout hold at 10 people and at 300.

Reference specifics applied: Linear generates its whole theme from three variables (base, accent, contrast) and builds hierarchy from black/white opacity, not hue. Geist uses a 10-step gray scale with fixed semantic jobs (100 background, 200 hover, 300 active, 400 border, 500 hover border, 600 active border, 700 high-contrast fill, 900 secondary text, 1000 primary text). Duolingo separates the streak (one action extends it) from the daily goal (tracked on its own), uses daily quests for near-term wins, and celebrates returning instead of punishing a miss. WAI-ARIA tabs use roving tabindex with arrow-key focus movement.

---

## Phase 1: Component audit (v1)

### Global

| Finding | Why it matters | Fix in v2 |
| --- | --- | --- |
| No dark mode | Every reference tool (Linear, Vercel, Raycast) is dark-first or dark-equal. Startup buyers notice. | Semantic token system on CSS variables, `data-theme` toggle, follows system by default, persisted. |
| Color used for decoration (gradient wallet card, six gradient category tiles, gradient streak badge, colored icon tiles on stat cards) | Brief: reserve accent strictly for active states, primary CTAs, streaks and achievements. v1 spends color everywhere so it means nothing. | Neutral surfaces everywhere. Accent only on: active nav, active tab underline, primary button, earning ring, streak, tier progress, completion checks. Category and goal icons become monochrome line icons on a neutral tint. |
| Emoji as iconography (goals, wallet categories, greeting) | Reads consumer-casual, renders differently per OS, breaks the "advanced tool" feel. | Inline SVG line icons with per-goal hue used only on the progress ring stroke. |
| Shadows and lift-on-hover on cards | Linear and Vercel use precise 1px borders and almost no shadow in light mode. | Borders only. Hover = border color step up (400 to 500). Shadow reserved for popovers, dialogs, command palette. |
| 14px base, generous padding | Fine for a consumer app; too airy for a tool. | 13px app base, 14px reading copy, 20 to 24px headings at -0.02em. Padding 16px standard, 20px on hero cards. |
| No monospaced accents | Brief asks for them explicitly; they signal technical clarity (Vercel logs, Linear IDs). | JetBrains Mono for invite codes, timestamps, metric readouts in charts, keyboard hints. |
| No keyboard layer | Linear and Raycast are keyboard-first. v1 has zero shortcuts. | Command palette (Cmd/Ctrl+K) for navigation and actions, `/` focuses search, Esc closes everything, Enter advances wizards, arrow keys in tabs and segmented controls. |
| Tabs do not exist; segmented controls lack ARIA | The brief's core focus. Pages stack cards vertically instead, which is why Insights and Benefits scroll. | A `Tabs` primitive: role tablist/tab/tabpanel, aria-selected, aria-controls, roving tabindex, arrow/Home/End keys, active tab background merges into the panel with no dividing border, inactive tabs muted bg and lower contrast, active gets weight + accent underline + text color (three cues), horizontal scroll with edge fades on overflow. Used on Team, Incentives, Insights, Burnout, Settings, Goals, Wallet, Benefits. |
| Toasts bottom-center on desktop | Fine on mobile; on desktop reference tools place them bottom-right, compact. | Bottom-right desktop, bottom-center mobile, 13px, 1px border, no heavy fill. |

### Shell and navigation

| Finding | Fix |
| --- | --- |
| Sidebar nav items are 14px with 20px icons and a pill highlight; feels like a consumer app. | Linear sidebar: 13px labels, 16px icons, 2px-radius-ish subtle fill on active (`active` step), accent text, workspace header at top (company avatar + name + chevron), footer row with theme toggle, Cmd+K hint, user. |
| Mobile bottom bar shows 5 of 7 employee items; Devices and Profile are unreachable on mobile. | Bottom bar shows 4 primary + "More" sheet; or 5 with Profile folded into a header avatar. v2: header avatar opens Profile; bottom bar = Home, Goals, Health, Wallet, Benefits. Devices reachable from Home card and Health empty state. |
| No way to switch between demo roles without logging out | Pitch friction. | Command palette action: "Switch to employee demo" / "Switch to employer demo". |

### Employer: Overview

| Finding | Fix |
| --- | --- |
| Four stat cards with colored icon tiles compete with the burnout alert for attention. | Vercel-style stats: label (900), big tabular number (1000), delta chip. No icon tile. Thin border. |
| No single "how are we doing" number. A VP of People wants one score to put in a board deck. | Program health score ring (0 to 100) at top-left: 40% adoption, 30% earning rate, 30% physical completion. Labeled Great / Good / Building. |
| Burnout alert is a gradient amber card. Correct semantics, too loud for Linear. | Amber left-border callout on neutral surface, amber text and icon only. |
| Population trends shown for any team size; with 3 connected people that is a privacy problem and a trust problem. | Lock state under 5 connected: "Needs 5+ connected to show team trends." Brief's scaling lens: the layout now explicitly handles a 10-person startup. |
| New-company empty state is a gradient banner. | Setup checklist card (Duolingo progression): Invite your team, First teammate joins, First device connected, Review rewards. Derived from data, checks fill in as they happen. |
| Activity feed timestamps in proportional font. | Mono timestamps. |

### Employer: Team

| Finding | Fix |
| --- | --- |
| Single flat list; at 300 people it is a wall. | Tabs: Active (n) / Invited (n). Filter chips: device connected, no device. Sort by name or earnings. Load 25 at a time with "Show more". `/` focuses search. |
| Status chips use three colors. | Status as muted text with a 6px dot; only "Invited" uses amber. |
| Invite modal stays open after send. | Closes on success, toast confirms. |

### Employer: Incentives

| Finding | Fix |
| --- | --- |
| Two stacked groups with uppercase section labels (brief forbids all-caps). | Tabs: Habits / Preventive. Mixed case everywhere. |
| Enabled goals get a green border, which competes with the toggle. | Enabled state communicated by the toggle alone; card border stays neutral. |
| Compliance meter is good. Keep it, tighten copy. | Keep. Move into a sticky right rail with mono percentages. |

### Employer: Insights

| Finding | Fix |
| --- | --- |
| Four large cards stacked, requires scrolling to compare. | Tabs: Retention / ROI / Goals / Benchmarks. One panel visible at a time. The merged-active-tab pattern is the showcase here. |

### Employer: Burnout detail

| Finding | Fix |
| --- | --- |
| Three small charts side by side are hard to read on a laptop. | Tabs: Sleep / HRV / Movement over one large chart with hover crosshair and mono values. Actions rail stays. |

### Employer: Settings

| Finding | Fix |
| --- | --- |
| Four cards stacked including a red-bordered demo card. | Tabs: Company / Budget / Integrations / Demo. Demo tab keeps the destructive action behind a confirm. |

### Employee: Home

| Finding | Fix |
| --- | --- |
| Streak badge is a gradient pill; the earning ring, three stat tiles, tier bar, and goal rows all land at once. | Streak as a compact amber chip (the one place amber is allowed). Hero card: ring + three plain stats + tier bar, neutral. |
| No daily loop. Everything is weekly or monthly, so there is nothing to do today. Duolingo's biggest lever is the daily quest. | "Today" card with three micro-quests derived from the latest data row (sleep 7h last night, 30 active minutes, 8k steps) with check states and a "2 of 3" header. Current-week day strip (Mon to Sun dots). |
| Streak break shows nothing; a user who missed a week just sees 0. | Progress-over-perfection copy: "Goals hit 11 of the last 13 weeks." Shown whenever streak < 4. |
| Monthly cap shown only as "of $150 possible". | "Max out October" monthly quest bar with a badge state at 100%. |
| Goal rows use colored progress rings plus colored bars plus colored dollar text. | Ring stroke keeps the goal hue (one color per row), everything else neutral. Week dots: filled, half (in progress), empty, dashed (upcoming). |

### Employee: Goals

| Finding | Fix |
| --- | --- |
| Long single list mixing habits and one-time preventive items. | Tabs: Habits / Preventive. |
| Week cards show "0 Missed" for weeks before the user joined. | Fixed in v1.1; v2 shows "No data" and dashes. |

### Employee: Health

| Finding | Fix |
| --- | --- |
| Range picker is a plain pill group with no ARIA. | Raycast-style segmented control: role radiogroup, arrow keys, animated thumb. |
| Insight card is a dark gradient block. | Neutral `contrast` surface with accent label. |
| Chart dots on every point make 90-day view noisy. | Dots only on hover; crosshair; mono tooltip. |

### Employee: Wallet

| Finding | Fix |
| --- | --- |
| Gradient balance card and six gradient tiles. | Neutral balance card with the number as the only large element; progress bar in accent; categories as bordered rows with line icons. Tabs: Browse / Activity. |
| Marketplace items have no visible "covered" explanation. | Covered items show "Covered by plan" as a muted chip; price column aligned mono. |

### Employee: Benefits, Devices, Profile

| Finding | Fix |
| --- | --- |
| Benefits: two columns plus a stacked bar; reimbursements list grows unbounded. | Tabs: Plan / Reimbursements. Value bar stays as the hero. |
| Devices: dark 56px tiles with text glyphs. | 40px neutral tiles, glyph in mono, connected state as a dot + text. |
| Profile: fine. | Tier ladder visual (Bronze to Platinum) so the progression is visible. |

### Onboarding wizards (both)

| Finding | Fix |
| --- | --- |
| Step indicator is five short bars; fine but no label. | Duolingo-style progress bar with step label and "x of 5". |
| Continue only by mouse. | Enter advances when the step is valid. |
| Plan cards show strikethrough premium; good. Keep. | Keep. Add "most popular" as muted chip not green. |

---

## Phase 2: Redesign specification

### Tokens (CSS variables, Tailwind colors mapped to them)

Light
- `--bg` #fafafa, `--bg2` #f4f4f5 (page, secondary page)
- `--g1` #ffffff surface, `--g2` #f4f4f5 hover, `--g3` #e4e4e7 active
- `--g4` #e4e4e7 border, `--g5` #d4d4d8 hover border, `--g6` #a1a1aa active border
- `--g7` #18181b contrast fill, `--g8` #27272a contrast hover
- `--g9` #71717a secondary text, `--g10` #09090b primary text
- `--accent` #059669, `--accent-hover` #047857, `--accent-soft` rgba(5,150,105,.10), `--accent-text` #047857

Dark
- `--bg` #0a0a0b, `--bg2` #0f0f10
- `--g1` #131315, `--g2` #1a1a1d, `--g3` #232327
- `--g4` #27272a, `--g5` #3f3f46, `--g6` #52525b
- `--g7` #fafafa, `--g8` #e4e4e7
- `--g9` #a1a1aa, `--g10` #fafafa
- `--accent` #10b981, `--accent-hover` #34d399, `--accent-soft` rgba(16,185,129,.14), `--accent-text` #34d399

Semantic (both): `--warn` amber 500/400, `--danger` red 500/400, goal hues sleep violet, hrv rose, steps sky, movement emerald, physical amber, dental teal.

### Type
- Inter: 13px app, 14px copy, 12px labels, 11px meta. Headings 20/24/28 weight 600 letter-spacing -0.02em. All numbers `tabular-nums`.
- JetBrains Mono: codes, timestamps, chart values, kbd.
- No all-caps anywhere. Section labels are 12px 500 in `--g9`.

### Spacing and shape
- 4px grid. Card padding 16. Hero 20. Gaps 12/16.
- Radius: cards 10, controls 8, chips 6, ring/pill 999.
- Borders 1px `--g4`. Hover `--g5`. Focus ring 2px accent at 40%.

### Active vs inactive
- Nav: active `--g3` fill (light) / `--g2` (dark), text `--accent-text`, weight 600, icon accent. Inactive text `--g9`, hover `--g2` fill.
- Tabs: tablist sits on `--bg2`; active tab background = `--g1` (same as panel), no bottom border (panel border is interrupted under it), 2px accent underline at the top edge inside the tab, text `--g10` 600. Inactive: `--bg2`, text `--g9` 500, hover text `--g10`.
- Segmented: track `--g2`, thumb `--g1` with 1px `--g4` border, active text `--g10`.
- Buttons: primary `--accent` fill white text; secondary `--g1` with `--g4` border; ghost text only; destructive red text with red soft fill on hover.

### Duolingo layer (what stays bright)
- Earning ring stroke (accent), streak chip (amber), tier progress (amber), completion checks (accent), confetti, "Today" quest checks. Nothing else.

### Keyboard
- Cmd/Ctrl+K palette. Esc closes. `/` focuses search on list pages. Arrow keys in tabs and segmented controls. Enter advances wizard steps when valid.

---

## Phase 3

Implemented in `index.html` (v2). v1 preserved at `/v1/`.
