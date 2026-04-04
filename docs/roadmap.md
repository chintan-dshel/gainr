# GAINR — Project Roadmap

**Version:** 3.0 Released | **Last Updated:** April 2026 | **Methodology:** Value-driven, MVP-first

---

## Roadmap Philosophy

This roadmap is sequenced by value, not by complexity. Each phase delivers a fully working product. If the project stopped at any phase, users would have something genuinely useful.

This is called **MVP thinking** — a core principle of modern product delivery.

> **v1.1 update note:** Following a structured critical review of v1.0, this roadmap has been resequenced. Several issues identified in review — data fragility, misleading AI positioning, missing onboarding, and UX gaps — are now addressed in v1.1 before the nutrition module. A honest product roadmap reflects reality, not just the original plan.

---

## Phase Overview

| Phase | Version | Name | Status | Key Deliverable |
|---|---|---|---|---|
| Phase 0 | — | Foundation | ✅ Complete | All PM documents, discovery, architecture |
| Phase 1–4 | v1.0 | Core App | ✅ Shipped | Working app — Train, Log, Analytics, RPG |
| Phase 5 | v1.1 | Stability & Honesty | ✅ Released | Onboarding, export, set editing, stall fixes, honest copy |
| Phase 5b | v1.2 | Polish & Accuracy | ✅ Released | Radar scoring, mobile UX, QA pass, critical bug fix |
| Phase 6 | v2.0 | Nutrition Module | ✅ Released | TDEE, macros, meal logging, 7th radar axis |
| Phase 7 | v2.1 | Program Customisation | ✅ Released | Custom exercises, swap, Train integration |

| Phase 8 | v3.0 | Real AI Integration | ✅ Released | Claude API coaching, onboarding wizard, physique goals, caloric balance |
| Phase 8b | v3.0 (final) | AI Engine + UX Polish | ✅ Released | CORS fix, test connection, UI simplification, Gemini 2.0 |
| Phase 9 | v4.0 | Multi-Profile + Cloud | 🔭 Next | Multiple user profiles, coach mode, cloud sync |
| Phase 10 | v4.1 | Wearables + Health APIs | 🔭 Future | Apple Health, Google Fit, real calorie burn data |
| Phase 9 | v4.0 | Platform & Sync | 🔭 Future | Cloud storage, wearables, multi-device |

---

## Phase Detail

### Phase 0 — Foundation ✅
**Goal:** Establish everything needed before building.

**Delivered:**
- Project Charter (DOC-001)
- Stakeholder Register (DOC-002)
- Discovery Log (DOC-003) — 3 sessions of structured requirements gathering
- Risk Register (DOC-004)
- Business Requirements Document (DOC-005) — 41 requirements
- Technical Architecture (DOC-006)
- Cost Management Plan (DOC-009) + Cost Log (DOC-010)

---

### Phase 1–4 — Core App ✅ (v1.0)
**Goal:** A functional fitness tracking proof of concept.

**Delivered:** See [CHANGELOG.md](../CHANGELOG.md) for full feature list.

**Honest assessment of v1.0:**
v1.0 is a well-executed proof of concept demonstrating PM-led AI-assisted delivery. It has strong bones — science-backed programming, SDP coaching, stall detection, RPG gamification, and analytics. However a structured critical review identified issues that must be addressed before new features are added. See Phase 5.

---

### Phase 5 — Stability & Honesty ✅ (v1.1) — RELEASED
**Goal:** Address every critical issue identified in post-launch review before adding new features.

**Released:** March 28, 2026

**Why before nutrition?**
Building new features on top of known structural problems is technical debt by choice. This resequencing is itself a demonstration of good PM discipline.

#### 5.1 — ✅ Onboarding & Demo Data (Critical)
**Problem:** Every new user opens the app and sees 3 months of someone else's workout history. Badges are pre-earned. There is no "start fresh" path.

**Fix:**
- Detect first-time users vs returning users on load
- Show an onboarding screen: "Explore demo" vs "Start your own journey"
- "Start fresh" clears demo data and initialises a blank profile
- Badges reset — users earn them through their own activity, not from fake data

#### 5.2 — ✅ Data Export & Backup (Critical)
**Problem:** All data lives in localStorage. Clearing browser cache, switching browsers, or getting a new phone causes permanent, unrecoverable data loss. For a fitness tracker where historical data is the entire value proposition, this is a trust-destroying flaw.

**Fix:**
- "Export data" button — downloads `gainr-backup-[date].json`
- "Import data" — restore from a previously exported file
- Visible warning in the UI: "Your data is stored on this device. Export regularly to back up."
- No false promises of cloud sync until v4.0

#### 5.3 — ✅ Honest AI Positioning (Critical)
**Problem:** The app is described as "AI-powered coaching" but the coaching engine is entirely rule-based `if/else` logic with hardcoded recommendation strings. This is accurate for how the app was *built* but not for what it *does* at runtime. A technical audience who reads the source code loses confidence immediately.

**Fix:**
- Update all in-app copy: "smart coaching engine" not "AI coaching"
- Update README to accurately describe the architecture
- Add a note explaining v3.0 will replace the rule-based engine with real Claude API integration
- The AI story is about the development methodology — that remains a genuine and compelling differentiator

#### 5.4 — ✅ Set Editing (High)
**Problem:** Once a set is marked complete it cannot be edited. A user who logs the wrong weight has no correction path — a common occurrence when training with heavy weights and limited attention.

**Fix:**
- Tap a completed checkmark to uncheck and re-edit
- Edited sets update the exercise history correctly on session completion

#### 5.5 — ✅ Stall Detection Accuracy (High)
**Problem:** The 3-session stall rule has three known false positive sources:
1. Deload weeks intentionally produce flat/dropping weights but are flagged as fatigue
2. Weight rounding (2.5 lb increments) makes intentional same-weight sessions look like stalls
3. No differentiation between a rep range ceiling and a genuine plateau

**Fix:**
- Exclude deload week sessions from stall calculations entirely
- Add ±2.5 lb tolerance — one increment variance is not a stall
- Incorporate rep range context — hitting the top of the rep range is SDP working, not a plateau

#### 5.6 — Radar Scoring Accuracy → Carried to v1.2
**Problem:** Several radar axes produce misleading scores:
- **Consistency** penalises appropriate rest (illness, injury, planned recovery)
- **Volume** rewards starting from zero — a beginner always scores higher than an experienced user
- **Recovery** defaults to 50 permanently if sleep isn't logged — meaningless noise
- **Balance** perpetually flags an imbalance because leg exercises generate more volume by weight regardless of programming balance

**Fix:**
- Consistency: rolling 4-week average rather than all-time rate
- Volume: score against optimal range (10–20 sets/muscle/week) not growth rate
- Recovery: show "insufficient data" state — no score is better than a wrong score
- Balance: normalise by set count, not raw volume weight

#### 5.7 — Mobile UX Fixes → Carried to v1.2
**Problem:** Real-device testing surfaces several friction points:
- Set input fields too small for accurate tapping while sweaty
- Long exercise names truncate mid-word, losing differentiating information
- No loading state when CDN is slow on gym WiFi
- Analytics re-renders all charts on every visit — will slow significantly with 12+ months of data

**Fix:**
- Increase set input minimum tap target to 44px height
- Consistent abbreviation system for long exercise names
- Skeleton loading states for all charts
- Cache computed scores — only recalculate when underlying data changes

---

---

### Phase 5b — Polish & Accuracy ✅ (v1.2) — RELEASED
**Goal:** Complete the remaining v1.1 items deferred due to complexity.

#### Radar Scoring Accuracy
- Consistency: rolling 4-week average instead of all-time rate
- Volume: score against optimal range (10–20 sets/muscle/week) not growth rate
- Recovery: show "insufficient data" state when sleep not logged
- Balance: normalise by set count, not raw volume weight

#### Mobile UX Improvements
- Increase set input minimum tap target to 44px height
- Skeleton loading states for all charts
- Cache computed analytics scores — only recalculate when data changes
- Abbreviation system for long exercise names in exercise browser

---

### Phase 6 — Nutrition Module 📋 (v2.0)
**Goal:** Complete the body recomposition picture with dietary tracking.

**Moved from original v2.0 slot** — now follows Phase 5 stability work.

**Planned features:**
- TDEE calculation (Mifflin St-Jeor + activity multiplier)
- Daily calorie and macro targets
- Meal logging against targets
- High-protein meal suggestions aligned to goal
- Nutrition score integrated into RPG system and radar chart

---

### Phase 7 — Program Customisation 📋 (v2.1)
**Goal:** Let users modify their workout program without editing source code.

**Problem being solved:** The entire workout program is hardcoded in a JavaScript constant. Users cannot swap exercises, adjust sets/reps, or follow any training style other than PPLUL. This limits the app to a single user archetype.

**Planned features:**
- Exercise swap — replace any movement with an alternative
- Set/rep target editing per exercise
- Rest day reassignment
- Custom exercise creation
- Program templates — Powerlifting, Bodyweight, 3-day, 4-day variants

---

### Phase 8 — Real AI Integration 🔭 (v3.0)
**Goal:** Replace the rule-based coaching engine with genuine Claude API integration. This is what makes the "AI coaching" claim legitimate.

**Planned features:**
- Pre-workout briefing generated from your actual session history
- Post-workout analysis — what went well, what to adjust next session
- Conversational coaching — ask any question about training or nutrition
- Adaptive program modifications based on detected patterns
- Research on-demand — science-backed answers with cited sources

**Architecture note:** The v1.0 engine functions (`getSDP()`, `detectStall()`, `computeHexScores()`) are designed as drop-in replacements for API calls. The UI and data layer remain unchanged in v3.0 — only the intelligence layer is upgraded. This was a deliberate forward-compatibility decision made at v1.0 architecture stage.

**Cost consideration:** API integration introduces per-request costs. A cost management strategy must be designed before v3.0 development begins.

---

### Phase 9 — Platform & Sync 🔭 (v4.0)
**Goal:** Solve the data architecture's fundamental limitations identified in v1.0 review.

**Problems being solved:** localStorage data loss, no cross-device sync, no automatic backup.

**Planned features:**
- Cloud storage backend (Supabase free tier)
- Account creation and authentication
- Cross-device sync — same data on phone and laptop
- Automatic cloud backup
- Apple Health / Google Fit passive data integration
- Wearable device support

---

## Decision Log — Full History

| Decision | Version | Rationale |
|---|---|---|
| Nutrition module last in original plan | v1.0 | User needs training history before nutrition is personalised |
| SDP before gamification | v1.0 | Gamification needs real data to be meaningful |
| API integration deferred to v3.0 | v1.0 | Zero budget; API requires cost strategy first |
| **Stability phase inserted before nutrition** | **v1.1** | **Critical review identified data loss risk and misleading positioning — these must be fixed before new features are added** |
| Program customisation added as v2.1 | v1.1 | Hardcoded program identified as blocker for real users beyond original single-user scope |
| Radar scoring moved from feature to fix | v1.1 | Misleading scores damage trust more than missing scores |
| Radar + UX fixes deferred to v1.2 | v1.1 | Complexity warranted a separate focused release rather than delaying v1.1 ship date |

---

## Known Limitations (Honest)

Documented limitations of the current version and when each will be addressed:

| Limitation | Severity | Addressed In |
|---|---|---|
| Data stored in localStorage — lost on cache clear | High | ✅ v1.1 (export/import) / v4.0 (cloud sync) |
| No cross-device data sync | High | v4.0 |
| Coaching engine is rule-based, not genuine AI | Medium | v3.0 |
| Workout program hardcoded — not user-editable | Medium | v2.1 |
| Demo data shown to all new users on first load | Medium | ✅ v1.1 |
| No set editing after completion | Medium | ✅ v1.1 |
| Stall detection has known false positives | Medium | ✅ v1.1 |
| Radar scores have measurement accuracy issues | Medium | v1.2 |

---

*This roadmap is a living document. It is reviewed and updated after every version release and every structured feedback session.*

---

## Next Phases — v4.0 and Beyond

### Phase 9 — v4.0: Multi-Profile + Cloud Sync

#### The Problem
GAINR is currently a single-user app. If you share a device with a partner, family member, or if you're a coach managing athletes, there's no way to separate data. Everything lives in one localStorage key. This is the most significant architectural limitation remaining.

#### Design Approach

**Option A — Local Multi-Profile (no server required)**
- Multiple profiles stored in localStorage: `gainr_profiles: { id1: {...}, id2: {...} }`
- Profile switcher on the landing screen — tap your name to load your data
- Each profile has its own full state: exercise history, nutrition, goal, settings
- PIN-lock optional per profile for privacy on shared devices
- Export/import works per-profile

**Option B — Coach / Athlete Mode (requires cloud)**
- Coach account has visibility across all athlete profiles
- Athletes log their own sessions; coach sees aggregated analytics
- Requires Supabase or similar for real-time sync
- More complex but the right long-term architecture

**Recommended sequencing:** Ship Option A first (local multi-profile, no new infrastructure). This solves the shared-device problem immediately. Then layer cloud sync on top for cross-device + coach mode in v4.1.

#### Key Design Decisions Deferred
- How many profiles per device? (Suggested cap: 6)
- Does switching profiles require a re-onboarding or just name selection?
- Should AI settings (API key) be per-profile or shared across profiles?
- How does demo mode work with multiple profiles?

#### Technical Notes
- Schema change: `gainr_profiles` replaces `gainr_v1` as the root key
- Migration: existing `gainr_v1` becomes Profile 1 automatically
- Active profile ID stored separately: `gainr_active_profile`
- All existing functions read from `S` — minimal changes needed if profile switching just swaps the `S` object

---

### Phase 10 — v4.1: Wearables + Health APIs

#### The Problem
MET-based calorie burn estimates (current approach) are approximations. A 60-minute Push day estimated at 5.0 MET × weight = ~330 kcal. A fitness tracker reading heart rate and movement gives a far more accurate number. The caloric balance feature is only as good as the burn estimate.

#### Design Approach
- Apple Health (iOS): read active calories via HealthKit Web API
- Google Fit (Android): read active calories via Fitness REST API
- Fallback: keep MET estimates if no wearable connected
- Show data source on caloric balance card (Estimated vs From Apple Health)

#### Pre-requisites
- Cloud sync (v4.0) makes the wearable data persistent across sessions
- User must grant health permissions explicitly — needs clear consent UI

---

### Phase 11 — v5.0: Social + Community

#### The Problem
GAINR is entirely private. There's no accountability mechanism, no way to share achievements, and no way to see how your progress compares to anything external. For many users, social accountability is the strongest driver of consistency.

#### Possible Features
- Share a workout summary as an image (generated client-side)
- Public profile with cumulative stats (opt-in)
- Challenges: set a goal, invite someone to match it
- Leaderboard for custom groups (gym friends, office challenge)

#### Constraint
This requires cloud infrastructure. Not appropriate before v4.0 cloud sync is stable.

---

### Decision Log (open)

| Decision | Options | Status |
|---|---|---|
| Multi-profile local vs cloud-first | Local first → cloud later | ✅ Decided |
| Coach mode architecture | Supabase + role-based access | 📋 Deferred to v4.1 |
| AI API key per-profile vs shared | Likely shared (convenience) | ❓ Open |
| Profile cap per device | 6 suggested | ❓ Open |
| Wearable priority: Apple or Google | Both, Apple first (iOS traffic) | ❓ Open |

