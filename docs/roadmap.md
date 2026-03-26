# GAINR — Project Roadmap

**Version:** 1.0 | **Last Updated:** March 2026 | **Methodology:** Value-driven, MVP-first

---

## Roadmap Philosophy

This roadmap is sequenced by value, not by complexity. Each phase delivers a fully working product. If the project stopped at any phase, users would have something genuinely useful.

This is called **MVP thinking** — a core principle of modern product delivery.

---

## Phase Overview

| Phase | Name | Status | Key Deliverable |
|---|---|---|---|
| Phase 0 | Foundation | ✅ Complete | All PM documents, discovery, architecture |
| Phase 1 | Core Engine | ✅ Complete | Working app — Train, Log, RPG, Analytics |
| Phase 2 | Tracking & Logging | ✅ Complete (in v1.0) | All metric logging with history |
| Phase 3 | RPG System | ✅ Complete (in v1.0) | Levelling, XP, badges, streaks |
| Phase 4 | Progress Visualisation | ✅ Complete (in v1.0) | Charts, analytics, stall detection |
| Phase 5 | Nutrition Module | 📋 Planned — v2.0 | TDEE, macros, meal logging |
| Phase 6 | Future / North Star | 🔭 Future | API integration, wearables, body scan |

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

**Why first?** You cannot build the right thing without knowing what the right thing is. Discovery is the highest-leverage investment in any project.

---

### Phase 1–4 — Core App ✅ (shipped as v1.0)
**Goal:** A fully functional AI fitness tracker.

**Delivered:** See [CHANGELOG.md](../CHANGELOG.md) for full feature list.

**Key decisions made:**
- Single HTML file architecture (no server, no cost, no login)
- localStorage for persistence (simple, portable, private)
- Science-backed SDP coaching engine
- 3-session stall detection rule
- PPLUL workout split with science-backed periodisation

---

### Phase 5 — Nutrition Module (v2.0) 📋
**Goal:** Complete the body recomposition picture with dietary tracking.

**Why last?**
Nutrition is complex and deserves full focus. By the time we build this, users will have months of training data — making the nutrition recommendations far more accurate and personalised.

**Planned features:**
- TDEE calculation (Mifflin St-Jeor formula + activity multiplier)
- Daily calorie and macro targets
- Meal logging against targets
- High-protein meal suggestions
- Nutrition score integrated into RPG system and radar chart

---

### Phase 6 — North Star 🔭
**Goal:** The vision that shaped every architecture decision.

**Items:**
- **Claude API integration** — real-time AI coaching, not rule-based recommendations
- **Wearable integration** — passive data from Apple Health / Google Fit
- **Body scan progress** — visual body composition tracking over time
- **Adaptive programming** — program automatically evolves based on individual progress patterns

**Architecture note:** Every Phase 1–5 decision was made with Phase 6 in mind. The data schema, the exercise history arrays, the analytics engine — all designed to be forward-compatible with API automation.

---

## Decision Log — Why Things Are Sequenced This Way

| Decision | Rationale |
|---|---|
| Nutrition module last | User needs training data history before nutrition advice is personalised |
| SDP before gamification | Gamification needs real data to be meaningful — empty levels feel hollow |
| Stall detection before nutrition | Training quality must be verified before dietary advice is calibrated |
| Charts after tracking | Can't visualise data that doesn't exist yet |
| API integration in v3.0 | Zero budget in v1.0; API requires cost management strategy first |

---

*This roadmap is a living document. It is updated at each version release.*
