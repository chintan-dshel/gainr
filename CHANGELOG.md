# Changelog

All notable changes to GAINR are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) conventions.
Versioning follows [Semantic Versioning](https://semver.org/).

---

## [Unreleased] — v1.2

### Planned
- Radar scoring accuracy (rolling averages, optimal range, insufficient data states)
- Mobile UX improvements (larger inputs, loading states, cached renders)
- Export history view in Log tab

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
