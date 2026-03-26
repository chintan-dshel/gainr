# Changelog

All notable changes to GAINR are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) conventions.
Versioning follows [Semantic Versioning](https://semver.org/).

---

## [Unreleased] — v1.1

### Planned
- GitHub Pages deployment — live URL accessible from any device
- Docs folder with full PM artefact suite
- Export / backup feature — download your data as JSON from within the app
- Pull-up progression tracker on dashboard

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
