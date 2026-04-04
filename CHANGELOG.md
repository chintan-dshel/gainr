# Changelog

All notable changes to GAINR are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) conventions.
Versioning follows [Semantic Versioning](https://semver.org/).

---

## [Unreleased] — v4.0

### Planned
- Multi-profile support — multiple users on one device, switchable without data loss
- Coach / athlete mode — one account manages multiple athletes with shared visibility
- Cloud sync — cross-device data via Supabase (required for multi-profile)
- Pre-workout AI briefing — session plan generated from history before you train
- Apple Health / Google Fit integration

---

## [3.0.0] — 2026-04-04 — Real AI Coaching + New User Journey

### Summary
v3.0 is the release that makes the "AI-powered" label accurate. It ships three major systems: a guided new-user onboarding wizard, a physique goal engine with caloric balance tracking, and a provider-agnostic AI coaching layer connected to real APIs. Every feature traces directly to user feedback from the v1–v2 cycle.

### New User Journey — 4-Step Onboarding Wizard
- Step 1: Welcome — choose Start my journey or Explore demo
- Step 2: Profile — name, age, sex, weight, height, activity level (5 options)
- Step 3: Goal — Bulk / Recomp / Cut with timeline in weeks; plain-English explanation of each
- Step 4: Ready — personalised TDEE, macro targets, and a 4-point next-steps checklist
- Back navigation on every step; all fields validated before proceeding
- Profile and goal committed to S.profile and S.goal on completion
- Baseline weight seeded automatically; dashboard greeting personalised with name

### Physique Goal System
- Bulk: TDEE +250 kcal — maximise muscle, minimal fat overshoot
- Recomp: TDEE +0 kcal — simultaneous fat loss and muscle gain (default)
- Cut: TDEE −400 kcal — fat loss priority, high protein to protect muscle
- Goal progress panel on Dashboard: weeks in / weeks left / weight change since start / on-track indicator
- Expected progress rates: Bulk +0.5 lbs/wk, Recomp ≤±2 lbs, Cut −0.75 lbs/wk

### Caloric Balance
- Daily balance card: consumed (meal logs) vs estimated burned (MET × weight × session type)
- MET values by day type: Legs/Lower 6.0, Push/Pull/Upper/Lower 5.0
- Net calories colour-coded vs daily target
- Remaining calories shown below the card

### AI Coaching Engine (Provider-Agnostic)
- Supports OpenAI (GPT-4o) and Google Gemini (2.0-flash-lite) — both work from browser
- Claude/Anthropic listed but correctly blocked: their API rejects browser requests via CORS policy; this is documented clearly in the UI
- callAI() abstraction routes all calls through one function — provider-swappable
- Key and provider stored in localStorage — user-supplied, never hardcoded
- ⚙️ gear icon on dashboard opens AI settings modal
- Test connection button validates key before saving — shows specific error (invalid key / rate limit / network)
- Error messages translated from HTTP codes to plain English

### Post-Workout Session Analysis
- Completing a session shows a summary modal: XP, PRs, exercise count
- Per-exercise table: weight × reps × sets, colour-coded diff vs last session
- AI analysis button: session assessment + 3 next-week targets with exact weights + focus point
- No key set → informational card explaining what AI provides, with "Set up AI" button

### Radar Coaching (Analytics Tab)
- Tap any axis → rule-based coaching shown immediately
- "Get AI coaching" button fires the AI call for that specific axis
- Context sent: goal, weeks in, weight change, sleep, stalls, all 7 radar scores

### UI & Stability
- AI coaching button and settings icon separated into two distinct controls
- Post-workout modal has clean separate paths for "has key" and "no key" states
- Testing panel in ⚙️ settings: reset to new user, load demo, preview post-workout summary
- All reset actions show confirm dialog with export reminder
- Node.js --check added to QA pipeline — syntax errors now caught before shipping

### Fixes Included from v3.0 Iteration
- Orphaned `});` after mkState — killed entire JS block silently (caught by Node --check)
- Duplicate `let aiCoachLoading` declaration — same cause
- Gemini model updated from deprecated `gemini-1.5-flash` to `gemini-2.0-flash-lite`
- showPage() switched from querySelectorAll('.page') to explicit ID list — was matching 24 elements including page-header, page-title, page-subtitle
- Onboarding step 1 starts display:none — was leaking layout even with parent hidden

---

## [1.3.0] — 2026-03-28 — Polish & Accuracy

### Summary
Completed all items deferred from v1.1. All four radar scoring axes fixed, mobile UX improvements shipped, and exercise name abbreviation added. v1.3 was largely pre-built across previous sessions — this release formally documents and ships it.

### Fixed — Radar Scoring (4 axes)
- **Consistency**: Rolling 4-week session count. Appropriate rest no longer penalised
- **Volume**: Scored against optimal hypertrophy range (10–20 sets/muscle/week), not growth rate from zero
- **Recovery**: Shows "insufficient data" (−1) when fewer than 3 sleep entries — no more misleading 50 default
- **Balance**: Normalised by set count per muscle group, not raw volume weight — legs no longer perpetually imbalanced

### Fixed — Mobile UX
- Set input tap targets: 44px height (accessibility minimum), 16px font (prevents iOS zoom)
- Checkmark button: 44×44px
- Exercise name abbreviation map (24 entries) — no more mid-word truncation in exercise browser
- Skeleton loading opacity on analytics charts — visual feedback on slow connections

---

## [2.0.0] — 2026-03-28 — Nutrition Module

### Summary
The most requested feature. Full nutrition tracking integrated into the Log tab, with TDEE calculation, daily macro targets, meal logging, and a 7th axis on the training composition radar. Nutrition now connects directly to the body recomposition goal.

### Added — TDEE Calculator
- Mifflin-St Jeor BMR formula + activity multiplier
- Activity levels: Sedentary → Very Active (5 options)
- Calculates and saves: TDEE (maintenance calories), protein (0.82g/lb), carbs, fat
- Targets saved to state — persist across sessions
- Recomp-optimised: protein prioritised, calories at maintenance not deficit

### Added — Meal Logging
- Log meal name, calories, protein, carbs, fat per meal
- Daily totals calculated automatically
- Progress bars per macro against target (turns red if over)
- Today's meal list with delete option
- +2 XP per meal logged

### Added — Nutrition Score (7th radar axis)
- Scored from: target setup (prerequisite) + logging consistency (40pts) + protein target hit rate (60pts)
- "Insufficient data" state if no targets set or no meals logged
- Full coaching recommendations in three tiers: high / developing / needs work
- Protein tile added to dashboard showing today's protein vs target

### Architecture
- Nutrition data stored in `S.nt`: `{meals:[], tdee:0, targets:{cal,pro,carb,fat}}`
- Auto-migrated on loadS if not present in existing saves
- Radar expanded from 6 to 7 axes — chart type handles variable axis count natively

---

## [2.1.0] — 2026-03-28 — Program Customisation

### Summary
Users can now meaningfully customise their workout program. Exercise swap (from v1.2) is complemented by custom exercise creation, giving full control over the program without touching code.

### Added — Custom Exercise Creator (Program tab)
- Add any exercise to any training day (Push/Pull/Legs/Upper/Lower)
- Configure: sets, rep range, starting weight, increment
- Appears in Train tab immediately alongside programmed exercises — tagged "custom" in blue
- Exercise history tracked independently in S.eh
- Remove custom exercises without losing history

### Added — Custom Exercise in Train Tab
- Custom exercises appear below programmed exercises per day
- Full SDP coaching applies — same logic as built-in exercises
- "Custom" tag (blue) visually distinct from "swapped" tag (gold)

### Updated — finishWorkout
- Now logs both swapped and custom exercises
- Both write independently to S.eh — full history and analytics for any exercise you add

### Updated — Program tab
- Swap button (↔) on all swappable exercises
- Custom exercise panel at bottom of Program tab
- List of current custom exercises with remove option

### Architecture
- Swaps stored in `S.swaps`: `{"day-idx": exerciseObject}`
- Custom exercises stored in `S.customEx`: `{"day": [exerciseArray]}`
- Both auto-migrated on loadS

---

## [1.2.0] — 2026-03-28 — Polish & Accuracy Release

### The Story
v1.2 completed the work deferred from v1.1, added a full QA stress test across 4 user personas, and caught one critical bug that had been silently present since the v1.1 schema migration. The QA process is now a documented part of the release workflow.

### Fixed — Radar Scoring Accuracy (4 axes)
- **Consistency**: Now uses rolling 4-week session count (not all-time rate) — appropriate rest no longer penalised
- **Volume**: Now scores against optimal hypertrophy range (10–20 sets/muscle/week) not growth rate from zero
- **Recovery**: Now shows "insufficient data" state (score -1) when fewer than 3 sleep entries logged — no more misleading 50 default
- **Balance**: Now normalises by set count per muscle group, not raw volume weight — legs no longer perpetually flagged

### Fixed — Null Score Handling
- Radar chart renders null scores as 0 with grey point colour (visually distinct from a real 0)
- Tooltip shows "No data yet" for null axes
- Detail panel shows contextual "how to unlock this score" message for null axes
- Axis pill buttons show "—" prefix for null scores
- Weakest axis auto-selection ignores null scores — picks the weakest *scored* axis

### Fixed — Critical Bug: Program Tab
- Program tab was reading `S.eh[ex.name].w` directly — broken since v1.1 schema migration to arrays
- Now correctly reads `arr[arr.length-1]` — last session data displays correctly

### Fixed — Mobile UX
- Set input tap targets increased to 44px height (was ~32px) — meets accessibility minimum
- Set input font size increased to 16px (was 14px) — prevents iOS zoom on focus
- Set input border-radius increased to 10px for a more touch-friendly feel
- Checkmark button increased to 44×44px (was 30×30px)

### Added — Exercise Name Abbreviation
- 24-entry abbreviation map for long exercise names (e.g. "Bulgarian Split Squat" → "BSS")
- Applied in exercise browser rows — no more mid-word truncation on small screens
- Full name still shown in chart title and stall alerts

### Added — Skeleton Loading States
- Analytics tab dims chart areas (40% opacity) while computing — visual feedback on slow connections
- Charts restore to full opacity after all renders complete

### Added — Red Toast Type
- `toast('message', 'red')` now styled correctly — used for import errors and validation failures

### QA Process
- 4 user personas tested: non-tech beginner, power user/trainer, returning user restoring backup, user on slow WiFi
- 15 automated checks run against app code
- 2 issues found and fixed (Program tab bug, toast red type)
- 13 checks passed clean

---

## [1.1.0] — 2026-03-28 — Stability & Honesty Release

### The Story
v1.1 was driven entirely by a structured self-critical review of v1.0 — asking the hard question: *what's actually wrong with this?* Seven issues were identified across data architecture, AI positioning, UX, and coaching accuracy. Five are fixed in this release. The remaining two (radar scoring accuracy and mobile UX polish) carry forward to v1.2.

This release also represents a deliberate PM decision: fix known problems before adding new features. Technical debt by choice is still technical debt.

### Fixed — Honest AI Positioning
- Removed "AI-powered" from app title and all in-app copy
- Analytics subtitle updated from "Planned vs actual" to "Smart coaching engine"
- Coaching description updated to accurately reflect rule-based engine
- README updated to distinguish between AI-assisted *development* vs runtime behaviour
- v3.0 Claude API integration noted as the point where "AI coaching" becomes accurate

### Fixed — Onboarding & Demo Data
- First-time users now see a full-screen choice on first load
- "Explore demo" — loads 3-month sample dataset to explore all features
- "Start my journey" — clears demo data, initialises a blank profile
- Badges reset on fresh start — users earn them through their own activity
- Returning users go straight to their dashboard, no disruption
- Data storage warning shown on first load: data lives on this device

### Fixed — Set Editing
- Completed sets can now be unchecked by tapping the checkmark
- Unlocking a set re-enables both weight and rep inputs and focuses weight field
- Toast confirmation shown when a set is unlocked for editing
- Completed set inputs visually dimmed (opacity 45%) so locked state is clear at a glance

### Fixed — Export & Import (Data Backup)
- Export button in Log tab → Data & Backup section
- Downloads `gainr-backup-[date].json` — full data snapshot
- Import accepts .json files, validates GAINR backup structure before restoring
- Confirmation dialog before overwriting current data
- Honest warning: "Your data is stored on this device. Export regularly to back up."

### Fixed — Stall Detection Accuracy
- Deload sessions now excluded from stall calculations (sessions at <75% of recent peak weight)
- ±2.5 lb tolerance band added — one increment variance is not a stall
- Rep ceiling context added — reps at programmed max means SDP is working, not a plateau
- Rep max looked up from program definition per exercise for accurate context

### Carried Forward to v1.2
- Radar scoring accuracy (consistency rolling average, volume vs optimal range, recovery insufficient data state, balance by set count)
- Mobile UX improvements (larger input targets, loading states, cached analytics renders)

---

## [1.0.0] — 2026-03-26 — Initial Release

### The Story
Built across 8 working sessions in March 2026. A zero-budget, PM-led product delivery using Claude AI as the primary development resource. Full project management methodology applied throughout — from discovery to BRD to architecture to delivery.

### Added — Core App
- Single-file PWA (`gainr.html`) — 108KB, works offline, installable on Android
- Dark theme with Bebas Neue display typography and gold/green/red accent system
- localStorage persistence with automatic schema migration across versions
- 3-month demo dataset seeded on first load (57 sessions, 341 exercise entries, 29 exercises)

### Added — Train Tab
- Full PPLUL v2.0 workout program (5 days: Push / Pull / Legs / Upper / Lower)
- Standard Double Progression (SDP) engine with 4 intelligent states:
  - First Session — establishes baseline
  - Push Reps — stay at weight, increase reps
  - Add Weight — SDP triggered, increment loaded
  - Deload — 60% of working weight auto-calculated
- Active Week / Deload Week toggle
- Set-by-set logging with checkmark completion
- XP, streak, and PR tracking on session completion

### Added — Log Tab
- Body weight logging with automatic lbs ↔ kg conversion
- Full body measurements (chest, waist, hips, both arms, thigh)
- Daily check-in: sleep hours and step count

### Added — Analytics Tab
- **Training composition radar** — 6-axis scoring from real data:
  - Strength: % of science-backed progression target achieved
  - Volume: weekly volume growth trend
  - Consistency: sessions per week vs 5-day target
  - Recovery: sleep quality score + deload compliance
  - Balance: push/pull/legs volume distribution ratio
  - Recomp: body composition change rate
- Interactive axis detail with strategic + specific recommendations (3 tiers per axis)
- **Lift progress charts** — planned vs actual for Bench, Squat, Deadlift, OHP
- Science-backed logarithmic beginner progression curves
- **Weekly volume charts** — sets × reps × weight per muscle group
- **Recomp dual-axis chart** — squat strength vs waist measurement
- **Stall detection engine** — 3-session rule with two stall types:
  - Type 1 Plateau (🟡): flat weight + reps → stimulus-change recommendations
  - Type 2 Fatigue (🔴): dropping weights → recovery-focused recommendations
- **Grouped exercise browser** — Push / Pull / Legs accordion with per-exercise trend indicators
- Stall & fatigue alerts panel (consolidated view)
- Planned vs actual analysis panel with auto-generated coaching commentary
- Milestone tracker with progress bars

### Added — RPG System
- Levels: Recruit (0) → Warrior (500 XP) → Beast (1500 XP) → Olympian (3500 XP)
- Stats: Strength, Endurance, Consistency (each levels 1–99)
- XP rules: workout +10, overload +5, PR +20, deload +15, sleep +3, steps +3
- Badges: First Blood, Iron Will (10 overloads), Pull Up Warrior, Warrior Unlocked
- Streak tracking with longest streak record

### Added — Dashboard
- RPG character card with level, XP bar, and stat grid
- Streak and session count
- Quick metric tiles: weight, waist, sleep, steps
- Today's workout label
- Badge collection

### Added — Program Tab
- Full week view with today highlighted
- Per-exercise last session data shown in green
- Exercise targets and baselines

### Technical
- Exercise history schema: full session array per exercise (migrates from single-object format)
- Schema version key: `gainr_v1` (migrates from `fitr_v4`, `fitr_v3`, `fitr_v2`, `olympian_v1`)
- Chart.js 4.4.0 + chartjs-plugin-annotation 3.0.1
- No external dependencies beyond CDN-hosted chart libraries

### Project Management
- Discovery log: 8 constraint decisions, 5 product decisions, 4 learning goals
- BRD: 41 requirements across 7 categories
- Risk register: 7 risks identified and mitigated
- Cost: CAD $28.00 (Claude Pro 1 month subscription)
- Total budget vs estimate: on budget (zero overspend)

---

## [0.1.0] — 2026-03-24 — Internal Prototype

### Added
- Initial app scaffold with 5-tab navigation
- Basic workout logging (flat exercise list, no SDP)
- Weight and measurement logging
- Basic RPG character card
- Progress charts (weight and waist)
- Olympic-themed naming (later renamed to GAINR)

### Notes
This version was never publicly released. Existed as a working prototype to validate the core concept before the full v1.0 build.

---

## Roadmap

### v2.0 — Nutrition Module *(Planned)*
- TDEE calculation based on user profile and activity level
- Daily macro targets: protein, carbs, fat
- Meal logging and daily target tracking
- High-protein meal suggestions
- Nutrition stat integration into RPG system

### v2.1 — Export & Backup *(Planned)*
- Download your data as JSON from within the app
- Import data to restore from backup
- Session summary PDF export

### v3.0 — AI Coaching Layer *(Future)*
- Claude API integration for real conversational coaching
- Pre-workout briefing generated from your actual history
- Post-workout analysis and next-session recommendations
- Research on-demand: ask about any exercise or nutrition topic
- Adaptive program modifications based on progress patterns

### v4.0 — Wearable Integration *(Future)*
- Apple Health / Google Fit passive data sync
- Automatic step and sleep logging
- Heart rate zone tracking during cardio
- Recovery score from HRV data

---

*Each version is a working, shippable product. GAINR is developed iteratively — v1.0 is fully functional today.*
