# GAINR — Project Roadmap

**Version:** 4.0 | **Last Updated:** April 2026 | **Status:** ✅ Active | **Methodology:** Value-driven, MVP-first

---

## Roadmap Philosophy

This roadmap is sequenced by value, not by complexity. Each phase delivers a fully working product. If the project stopped at any phase, users would have something genuinely useful. This is called **MVP thinking** — a core principle of modern product delivery.

> **Project note:** GAINR was built as a portfolio project to demonstrate AI-enabled PM methodology. v1.0–v3.1 was completed in 9 calendar days and approximately 20 hours. v4.0 added a full design refresh and Coach intelligence layer in a follow-up session. Phases 9+ were designed but descoped by deliberate choice, not resource constraint.

---

## Phase Overview

| Phase | Version | Name | Status | Key Deliverable |
|---|---|---|---|---|
| Phase 0 | — | Foundation | ✅ Complete | All PM documents, discovery, architecture |
| Phase 1–4 | v1.0 | Core App | ✅ Shipped | Working app — Train, Log, Analytics, RPG, SDP engine |
| Phase 5 | v1.1 | Stability & Honesty | ✅ Released | Onboarding, export, set editing, stall fixes, honest copy |
| Phase 5b | v1.2–1.3 | Polish & Accuracy | ✅ Released | Radar rebuilt, 44px inputs, mobile UX, exercise abbreviations |
| Phase 6 | v2.0 | Nutrition Module | ✅ Released | TDEE, macros, meal logging, 7th radar axis |
| Phase 7 | v2.1 | Program Customisation | ✅ Released | Exercise swap (24 exercises), custom exercise creator |
| Phase 8 | v3.0 | Real AI Coaching | ✅ Released | Onboarding wizard, physique goals, caloric balance, AI coaching (OpenAI/Gemini) |
| Phase 8b | v3.0.x | AI Engine + UX Polish | ✅ Released | CORS fix, provider-agnostic AI, test connection, post-workout analysis |
| Phase 8c | v3.1 | Profile Page | ✅ Released | Identity card, inline editing, goal management |
| Phase 8d | v4.0 | Design Refresh & Coach Intelligence | ✅ Released | OKLCH design system, Coach tab, interactive charts, versioned AI prompt |
| Phase 9 | v5.0 | Multi-Profile + Cloud | 🚫 Descoped | Designed but not built — intentional scope decision |
| Phase 10 | v5.1 | Wearables + Health APIs | 🚫 Descoped | Designed but not built |
| Phase 11 | v6.0 | Social + Community | 🚫 Descoped | Requires cloud infrastructure — not appropriate scope |

---

## Phase Detail — Completed

### Phase 0 — Foundation ✅
**Delivered:**
- Project Charter, Stakeholder Register, Discovery Log, Risk Register
- Business Requirements Document (41 requirements)
- Technical Architecture document
- Cost Management Plan + Cost Log

---

### Phase 1–4 — Core App ✅ (v1.0) — Released March 26, 2026
**Delivered:** PPLUL workout program, SDP progressive overload engine (4 states), RPG system (XP/levels/badges/streaks), stall detection, analytics with radar chart, GitHub Pages deployment.

**Post-launch review findings:** Data loss risk (localStorage only), misleading "AI-powered" copy, no onboarding, radar scoring inaccuracies. All addressed in v1.1 before new features were added — a deliberate PM decision to protect product integrity over velocity.

---

### Phase 5 — Stability & Honesty ✅ (v1.1) — Released March 28, 2026
**Why before nutrition:** Building new features on known structural problems is technical debt by choice.

- ✅ Onboarding: Explore demo vs Start fresh — user choice on first load
- ✅ Data export/import: JSON backup, restores from file
- ✅ Honest AI copy: "smart coaching engine" not "AI coaching" until v3.0 makes it true
- ✅ Set editing: tap completed checkmark to unlock and re-enter
- ✅ Stall detection: deload exclusion, ±2.5 lb tolerance, rep ceiling context

---

### Phase 5b — Polish & Accuracy ✅ (v1.2–1.3) — Released March 28, 2026
- ✅ Radar rebuilt: rolling 4-week consistency, optimal volume range (10–20 sets/week), null scores for insufficient data, balance by set count
- ✅ 44px tap targets, 16px font (prevents iOS zoom)
- ✅ Exercise name abbreviation map (24 entries)
- ✅ Skeleton loading states for analytics

---

### Phase 6 — Nutrition Module ✅ (v2.0) — Released March 28, 2026
- ✅ TDEE calculator: Mifflin-St Jeor formula + 5 activity levels
- ✅ Recomp macro targets: 0.82g protein/lb, 25% fat, remainder carbs
- ✅ Meal logging: name, calories, protein, carbs, fat; daily progress bars; delete option
- ✅ 7th radar axis: Nutrition (scored from target setup + logging consistency + protein hit rate)
- ✅ Protein tile on dashboard

---

### Phase 7 — Program Customisation ✅ (v2.1) — Released March 28, 2026
- ✅ Exercise swap: 3 curated alternatives per exercise (24 exercises covered), stored in S.swaps
- ✅ Custom exercise creator: add any exercise to any day, full SDP coaching, stored in S.customEx
- ✅ Both swapped and custom exercises tracked independently in S.eh
- ✅ "swapped" (gold) and "custom" (blue) tags in Train and Program tabs

---

### Phase 8 — Real AI Coaching ✅ (v3.0) — Released April 4, 2026
- ✅ 4-step onboarding wizard: Welcome → Profile → Goal → Ready
- ✅ Physique goal system: Bulk +250 kcal / Recomp +0 / Cut −400 from TDEE
- ✅ Goal progress panel on dashboard: weeks in/left, weight change, on-track indicator
- ✅ Caloric balance: consumed vs MET-estimated burned vs daily target
- ✅ AI coaching: provider-agnostic (OpenAI GPT-4o, Gemini 2.0 Flash Lite)
- ✅ Post-workout summary: session recap, next-week targets, AI analysis
- ✅ API settings modal: provider selector, key input, test connection button
- ✅ CORS correctly handled: Anthropic blocked by design, OpenAI/Gemini work natively from browser
- ✅ Testing panel: reset to new user, load demo, preview post-workout summary

---

### Phase 8c — Profile Page ✅ (v3.1) — Released April 6, 2026
- ✅ Profile tab replaces Program in nav (Program accessible from Profile → Workout program)
- ✅ Identity card: gold avatar, name, level, session count, XP, streak
- ✅ Goal banner: active goal in goal colour, caloric target, weeks in / remaining
- ✅ Inline editing for all fields: name, age, sex, weight, height, activity, goal type, timeline
- ✅ Field-specific validation before save
- ✅ Recalculate targets button: reruns TDEE from current profile, applies goal offset
- ✅ Quick links: Workout program, Progress charts, AI settings

---

### Phase 8d — Design Refresh & Coach Intelligence ✅ (v4.0) — Released April 25, 2026
- ✅ OKLCH perceptual color system — full token migration, legacy aliases preserved
- ✅ Three-font typographic stack: Archivo Narrow (display), Inter (body), JetBrains Mono (numbers)
- ✅ First-run experience: SDP baseline targets on day 1, contextual empty state on dashboard
- ✅ Coach tab: Weekly Readiness card, Today's SDP Focus, Stall Flags, Weekly Brief AI
- ✅ Stats sub-tab: existing analytics behind lazy-loaded tab toggle
- ✅ Date range filter (7d/30d/90d/All) on strength and recomp charts
- ✅ Touch tooltips on all Chart.js charts (`touchstart`/`touchmove` events)
- ✅ `COACH_PROMPT_V1` versioned prompt object with `buildWeeklyPrompt()` and `buildAxisPrompt()`
- ✅ `getCoachAI()` function: structured STATUS / PRIORITY / 3-action output in Coach tab
- ✅ Visual polish: character card quieter, page titles reduced, number/label hierarchy tightened

---

## Phase Detail — Descoped

The following phases were designed during the project and are documented here for portfolio completeness. They were not built due to a deliberate wind-down decision, not resource or time constraints.

### Phase 9 — v5.0: Multi-Profile + Cloud Sync 🚫 Descoped

**Problem it would have solved:** GAINR is single-user. All data in one localStorage key. No cross-device sync, no shared-device support, no coach/athlete mode.

**Design (not built):**
- Option A — Local multi-profile: `gainr_profiles: {id1:{...}, id2:{...}}`, profile switcher on landing screen, PIN-lock per profile, export/import per profile. No server required.
- Option B — Cloud: Supabase backend, account auth, real-time sync across devices, coach visibility across athlete profiles.
- Recommended sequence: A first, then B on top.

**Why descoped:** Cloud infrastructure is a different complexity tier and appropriate scope for a separate project. Portfolio objectives were met at v3.1.

---

### Phase 10 — v4.1: Wearables + Health APIs 🚫 Descoped

**Problem it would have solved:** MET-based burn estimates (~330 kcal for a Push session) are approximations. Apple Health / Google Fit data would make the caloric balance card genuinely accurate.

**Design (not built):** HealthKit Web API (iOS) + Google Fitness REST API (Android). Show data source on balance card. Fall back to MET if no wearable connected. Requires cloud sync as prerequisite.

---

### Phase 11 — v5.0: Social + Community 🚫 Descoped

**Design (not built):** Shareable workout summary images, opt-in public profile, group challenges, leaderboard. Requires cloud infrastructure — not appropriate without v4.0.

---

## Decision Log — Full History

| Decision | Version | Rationale |
|---|---|---|
| Nutrition module deferred from v1.0 | v1.0 | User needs training history before nutrition is personalised |
| SDP before gamification | v1.0 | Gamification needs real data to be meaningful |
| API integration deferred to v3.0 | v1.0 | Zero budget; API requires cost strategy first |
| Stability phase inserted before nutrition | v1.1 | Critical review found data loss risk and misleading AI copy — integrity before features |
| Program customisation added as v2.1 | v1.1 | Hardcoded program is a blocker for real users beyond original single-user scope |
| Radar scoring moved from feature to fix | v1.1 | Misleading scores damage trust more than missing scores |
| Radar + UX fixes deferred to v1.2 | v1.1 | Complexity warranted a separate release |
| Anthropic API not used for browser calls | v3.0 | CORS policy blocks browser-to-API calls by design; OpenAI + Gemini support it natively |
| Provider-agnostic AI (not Claude-only) | v3.0 | No reason to lock users to one provider; abstraction costs nothing |
| Profile page replaces Program in nav | v3.1 | Program is reference material visited occasionally; Profile is account information visited regularly |
| Cloud sync and wearables descoped | v3.1 | Portfolio objectives met; infrastructure work is a separate project |
| Wind down at v3.1 | v3.1 | Clean exit on a high note with complete narrative — intentional, not forced |
| Design refresh reopened at v4.0 | v4.0 | OKLCH design system + Coach intelligence layer added — design critique driving follow-on release |

---

## Known Limitations (Honest, Final)

| Limitation | Severity | Status |
|---|---|---|
| Data stored on device only — lost on cache clear | High | Mitigated: export/import in v1.1. Full cloud sync descoped. |
| No cross-device sync | High | Descoped — v4.0 designed but not built |
| No automated tests or CI/CD | High | Not built — manual QA with Node.js syntax validation |
| Codebase requires AI to maintain or extend | High | Intentional constraint of the development approach |
| Technical debt invisible without code literacy | Medium | Documented risk, accepted for portfolio scope |
| Caloric burn is MET estimate, not measured | Medium | Wearable integration descoped |
| Single user only — no profile switching | Medium | Multi-profile descoped |

---

## Project Outcomes

| Metric | Result |
|---|---|
| Calendar days (v1.0 → v3.1) | 9 days |
| Calendar days (v4.0 design refresh) | 1 session |
| Active work hours (total) | ~22 hours |
| Versions shipped | 10 |
| Features in final build | 28 confirmed |
| Total infrastructure cost | CAD $28 (one month Claude Pro) |
| Traditional dev estimate (same scope) | CAD $18,000–$24,000 |
| Scope delivered | 97%+ of original vision |
| Final QA result | 0 blocking issues |

---

*This roadmap is a complete record of the project from inception to wind-down. It reflects reality at every stage — including the resequencing decisions, the honest limitations, and the deliberate scope choices. That's what a PM roadmap should do.*
