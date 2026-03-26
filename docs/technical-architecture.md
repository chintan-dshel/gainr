# GAINR — Technical Architecture

**Version:** 1.0 | **Author:** PM + Claude AI | **Status:** Approved

---

## System Overview

GAINR uses what software engineers call a **stateless client-side architecture**. In plain English: there is no server. The entire app runs in your browser, and your data lives on your device.

```
┌─────────────────────────────────────┐
│     User (Browser / Phone)          │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│     GAINR Web App                   │
│     gainr.html — 108KB single file  │
│                                     │
│  ┌──────────┐  ┌──────────────────┐ │
│  │  SDP     │  │  Stall Detection │ │
│  │  Engine  │  │  Engine          │ │
│  └──────────┘  └──────────────────┘ │
│  ┌──────────┐  ┌──────────────────┐ │
│  │  RPG     │  │  Analytics /     │ │
│  │  System  │  │  Radar Engine    │ │
│  └──────────┘  └──────────────────┘ │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│     localStorage                    │
│     Key: gainr_v1                   │
│     JSON — stored on device         │
└─────────────────────────────────────┘
```

---

## Why This Architecture?

### Constraints that shaped decisions

| Constraint | Impact on Architecture |
|---|---|
| Zero budget | No cloud hosting, no database service, no API costs |
| No coding background | No build tools, no package managers, no deployment pipeline |
| Personal use only | No multi-user auth, no data sync, no server needed |
| Mobile-first | PWA approach — no App Store submission required |

### What "stateless" means in practice

Traditional apps remember you between sessions via a server database. GAINR has no server. Instead, all state (your workout history, RPG level, body measurements) is stored in `localStorage` — a key-value store built into every browser.

This is the same pattern used by production AI applications: data is retrieved and injected into the system at runtime. You're essentially performing this manually by opening the app, which loads your stored state automatically.

---

## Data Architecture

### Storage key
```
localStorage key: gainr_v1
```

### State schema (simplified)
```json
{
  "rpg": {
    "xp": 955,
    "stats": { "str": 28, "end": 22, "con": 35 },
    "sc": 57,
    "streak": 5,
    "badges": ["First Blood", "Iron Will"]
  },
  "tr": {
    "wl": [{ "date": "2026-01-05", "lbs": 182, "kg": 82.5 }],
    "ml": [{ "date": "2026-01-05", "chest": 40, "waist": 35.5 }],
    "sl": [{ "date": "2026-01-05", "hours": 7.5 }],
    "stl": [{ "date": "2026-01-05", "steps": 8000 }]
  },
  "eh": {
    "Squat (Barbell)": [
      { "w": 145, "r": 8, "s": 4, "d": "2026-01-06", "vol": 4640 },
      { "w": 180, "r": 9, "s": 4, "d": "2026-01-13", "vol": 6480 }
    ]
  },
  "wt": "active"
}
```

### Schema migration
The app automatically migrates data from older schema versions on load. This means updates never break existing data.

| Key | Version |
|---|---|
| `gainr_v1` | Current |
| `fitr_v4` | Migrated automatically |
| `fitr_v3`, `fitr_v2` | Migrated automatically |
| `olympian_v1` | Migrated automatically |

---

## Engine Overview

### SDP Engine (Standard Double Progression)

The core coaching intelligence. For every exercise, every session:

```
If first session ever → First Session (use baseline weight)
If deload week active → Deload (60% of last working weight)
If last session hit top of rep range → Add Weight (+ increment)
Otherwise → Push Reps (same weight, more reps)
```

Increment sizes are exercise-specific (2.5 lbs for isolation, 5 lbs for compounds, 10 lbs for leg press and hip thrust).

### Stall Detection Engine (3-session rule)

Runs on every exercise with 3+ logged sessions:

```
Last 3 sessions: weights dropping → Type 2 Fatigue (🔴)
Last 3 sessions: weights + reps flat → Type 1 Plateau (🟡)
Otherwise → Progressing normally (✅)
```

Different stall types receive different recommendations because they have different causes:
- Fatigue → recovery intervention (sleep, deload, volume reduction)
- Plateau → stimulus change (tempo, rest periods, near-failure training)

### Radar Engine (6-axis scoring)

Each axis scores 0–100 from real user data:

| Axis | Data Source | Scoring Logic |
|---|---|---|
| Strength | Lift history vs projection curves | % of 12-week target achieved |
| Volume | Weekly sets×reps×weight per group | Growth trend vs starting point |
| Consistency | Session count / weeks elapsed | % of 5 sessions/week target |
| Recovery | Sleep log average | 8hrs = 100, 4hrs = 0, linear |
| Balance | Push/pull/legs volume ratio | Deviation from equal distribution |
| Recomp | Weight + measurement logs | Weight loss + waist reduction + muscle gain signals |

---

## Technology Stack

| Layer | Technology | Cost | Rationale |
|---|---|---|---|
| App | HTML/CSS/JavaScript | Free | Single file, no build step |
| Charts | Chart.js 4.4.0 (CDN) | Free | Industry standard, radar support |
| Annotations | chartjs-plugin-annotation (CDN) | Free | Milestone lines on charts |
| Fonts | Google Fonts (CDN) | Free | Bebas Neue + DM Sans |
| Storage | localStorage | Free | Browser built-in |
| Hosting | GitHub Pages (v1.1) | Free | Static file hosting |

**Total infrastructure cost: $0**

---

## Forward Compatibility — Phase 6 Design Decisions

Every architecture decision in v1.0 was made with the future API integration in mind:

- **Exercise history arrays** — structured for easy API transmission
- **Modular engine functions** — `getSDP()`, `detectStall()`, `computeHexScores()` can be replaced with API calls
- **Clean state schema** — JSON-serialisable, ready for cloud sync
- **No vendor lock-in** — pure HTML/JS, portable to any hosting

When v3.0 Claude API integration is built, the transition will be: replace rule-based engine functions with API calls. The UI, data layer, and UX remain unchanged.

---

## Security & Privacy

- No data ever leaves the user's device
- No analytics, no tracking, no external data collection
- No account creation or authentication required
- Data can be cleared by clearing browser localStorage
- No third-party data sharing

---

*Architecture designed by PM + Claude AI. All decisions documented with rationale.*
