# GAINR — AI-Powered Personal Fitness Tracker

> A fully functional fitness tracking web app built entirely through human-AI collaboration, applying professional project management methodology from discovery to delivery.

[![Status](https://img.shields.io/badge/status-active-2ed573)](#)
[![Version](https://img.shields.io/badge/version-2.1-f5c842)](#)
[![Built With](https://img.shields.io/badge/built%20with-Claude%20AI-b39ddb)](#)
[![License](https://img.shields.io/badge/license-MIT-4fc3f7)](#)

---

## What Is This?

GAINR is a mobile-first fitness tracking Progressive Web App (PWA) that runs entirely in a browser — no installation, no backend, no cost. It features AI-powered coaching recommendations, science-backed workout programming, RPG-style gamification, and advanced analytics including stall detection and training composition analysis.

**But the app is only half the story.**

This repository is also a live demonstration of what modern AI-assisted project delivery looks like — a PM-led, zero-budget product built from scratch using structured methodology and AI collaboration. Every decision is documented. Every phase is versioned. The full project management artefacts are included.

---

## The App — Feature Overview

### 🏋️ Train
- Full **PPLUL v2.0 workout program** (Push / Pull / Legs / Upper / Lower)
- **Standard Double Progression (SDP)** coaching — tells you exactly when to add weight or push reps
- **Active Week / Deload Week toggle** — deload weights auto-calculated at 60% of working weight
- Set-by-set logging with completion tracking

### 📊 Analytics
- **Training composition radar** — 6-axis score (Strength, Volume, Consistency, Recovery, Balance, Recomp) with interactive coaching recommendations
- **Planned vs actual strength charts** — science-backed logarithmic progression curves
- **Stall detection engine** — distinguishes Type 1 Plateau from Type 2 Fatigue, with different science-backed recommendations for each
- **Grouped exercise browser** — all 29 exercises organised by muscle group with trend indicators
- **7-axis composition radar** — Strength, Volume, Consistency, Recovery, Balance, Recomp, Nutrition
- **Weekly volume tracker** and **recomp dual-axis chart**

### 📝 Log
- Body weight with automatic lbs ↔ kg conversion
- Full body measurements (7 sites)
- Daily check-in: sleep and steps
- **Nutrition tracking** — TDEE calculator, daily macro targets, meal logging with protein/carb/fat

### 🥗 Nutrition
- Mifflin-St Jeor TDEE calculator with 5 activity levels
- Recomp-optimised macro targets (0.82g protein/lb)
- Per-meal logging with daily progress bars
- 7th axis on training composition radar

### 🎮 RPG System
- **Recruit → Warrior → Beast → Olympian** level progression
- XP awarded for sessions, progressive overload, PRs, deloads, and logging
- Badges: First Blood, Iron Will, Pull Up Warrior, Warrior Unlocked
- Streak tracking

### 📱 Progressive Web App
- Works in any mobile browser
- Installable on Android home screen (no App Store needed)
- All data stored locally — no server, no account, no cost

---

## The Project — PM Methodology

This project was built using full PMI-aligned project management methodology. Every phase is documented.

### Project Documents

| Document | Description |
|---|---|
| [Project Charter](docs/project-charter.docx) | Formal project authorisation, scope, stakeholders, risks |
| [Business Requirements (BRD)](docs/brd.md) | 41 functional and non-functional requirements with priorities |
| [Technical Architecture](docs/technical-architecture.md) | System design, data architecture, session flow, tech stack decisions |
| [Project Roadmap](docs/roadmap.md) | 6-phase delivery plan with rationale for sequencing |
| [Risk Register](docs/risk-register.md) | 7 identified risks with likelihood, impact, and mitigations |
| [Cost Management](docs/cost-log.md) | Full cost tracking — total spend: CAD $28.00 |

### The Process

**Discovery** — Before writing a single line of code, 3 sessions of structured requirements gathering: user profile, constraints, goals, technical environment, priorities.

**Definition** — BRD with prioritised requirements (Must Have / Should Have / Nice to Have), formal scope boundaries, acceptance criteria, and open questions log.

**Architecture** — Technical decisions documented with rationale. Data architecture designed for forward compatibility with future phases.

**Execution** — Agile delivery with sprint logs, change control, and version management. Scope changes formally processed and documented.

**Review** — Real workout history analysed (86 sessions, 1,702 sets) to calibrate the app to actual user data before building features.

---

## The AI Collaboration — How It Actually Worked

This is not a project where AI wrote everything and a human pressed send. The collaboration was structured and intentional.

### What the Human (PM) Did
- Defined the problem and success criteria
- Made all product decisions and approved scope
- Challenged assumptions and pushed back on over-engineering
- Provided real personal data for calibration
- Applied PM methodology to structure the work

### What AI (Claude) Did
- Wrote all code (HTML, CSS, JavaScript, Python data scripts)
- Researched fitness science and validated recommendations
- Generated all project management documents
- Analysed workout history data (341 entries across 29 exercises)
- Proposed technical architecture options with tradeoffs

### What Made It Work
- The PM treated AI as a **team member with expertise**, not a tool to prompt
- Every assumption was questioned — no assumptions made without asking
- Work was broken into phases with formal approvals at each gate
- The PM's domain knowledge (fitness, project management) shaped every output
- When AI over-engineered (e.g. suggesting complex cloud infrastructure), the PM redirected to simpler solutions

### Key Prompting Principles Applied
1. **Context before requests** — always establishing goals and constraints first
2. **Approval gates** — nothing built without explicit sign-off
3. **No assumptions** — every unknown was surfaced as a question
4. **Iterative refinement** — features were reviewed and improved across sessions
5. **Domain expertise injection** — real workout data and PM knowledge shaped outputs

---

## Technical Architecture

```
┌─────────────────────────────────────┐
│     You (Browser / Phone)           │
│     Samsung Galaxy / Any Browser    │
└──────────────┬──────────────────────┘
               │ paste save file
┌──────────────▼──────────────────────┐
│     GAINR Web App (Frontend)        │
│     Single HTML file — no server    │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│     JavaScript Engine (Backend)     │
│  ┌──────────┐ ┌──────────────────┐  │
│  │  SDP     │ │  Stall Detection │  │
│  │  Engine  │ │  Engine          │  │
│  └──────────┘ └──────────────────┘  │
│  ┌──────────┐ ┌──────────────────┐  │
│  │  RPG     │ │  Analytics &     │  │
│  │  System  │ │  Radar Engine    │  │
│  └──────────┘ └──────────────────┘  │
│  ┌────────────────────────────────┐ │
│  │  Science & Knowledge Base      │ │
│  │  (SDP rules, stall thresholds, │ │
│  │   progression curves, recs)    │ │
│  └────────────────────────────────┘ │
└──────────────┬──────────────────────┘
               │
┌──────────────▼──────────────────────┐
│     localStorage (Database)         │
│     JSON — runs on your device      │
└─────────────────────────────────────┘
```

**Why this architecture?**
Zero budget + no coding background + personal use = the simplest architecture that works. Client-side persistence via localStorage means no server costs, no privacy concerns, no account management. The entire app ships as a single 108KB HTML file.

---

## Quick Start

1. Download `app/gainr.html`
2. Open in any browser (Chrome recommended for Android install)
3. On Android: tap the browser menu → "Add to Home Screen"
4. The app comes pre-loaded with 3 months of demo data to explore all features

**To use with your own data:**
- Open the app and go to **Log** to start entering your actual metrics
- Go to **Train** to log your first workout session
- Your data saves automatically to your browser

---

## Roadmap

| Version | Focus | Status |
|---|---|---|
| v1.0 | Core app — Train, Log, Analytics, RPG | ✅ Released |
| v1.1 | Stability & Honesty — onboarding, export, set editing, stall detection, honest copy | ✅ Released |
| v1.2 | Radar scoring accuracy, mobile UX polish, QA pass | ✅ Released |
| v1.3 | Remaining radar fixes, abbreviations, skeleton states | ✅ Released |
| v2.0 | Nutrition module — TDEE, macros, meal logging, 7th radar axis | ✅ Released |
| v2.1 | Program customisation — custom exercises, swap, Train integration | ✅ Released |
| v3.0 | Claude API — real conversational coaching | 🔭 Future |
| v2.1 | Export & backup — download data from within app | 📋 Planned |
| v3.0 | Claude API integration — live AI coaching | 🔭 Future |

---

## What I Learned

This project was intentionally designed as a learning exercise in AI collaboration and software delivery. Key lessons:

**On AI Collaboration**
- AI is most powerful when given a PM-style brief, not just a task
- The quality of output scales directly with the quality of context provided
- Knowing when to push back on AI suggestions is as important as knowing what to ask for
- Effective prompting is a structured discipline, not trial and error

**On Building with AI**
- A non-technical PM can ship real, functional software using AI — but methodology matters
- The PM's job shifts from writing requirements for developers to writing requirements *as* the AI's operating context
- Architecture decisions still require human judgment — AI will over-engineer without constraints
- Documentation and version control remain essential even in AI-assisted delivery

**On the SDLC**
- Discovery is even more important with AI — garbage in, garbage out at speed
- Approval gates prevent scope creep in AI-assisted projects just as in traditional ones
- The PM role doesn't disappear with AI — it becomes the most critical role in the process

---

## About This Project

Built by a project manager exploring the intersection of AI and product delivery.

- **Timeline:** March 2026
- **Budget:** CAD $28.00 (Claude Pro, 1 month)
- **Team:** 1 PM + Claude AI
- **Sessions:** ~8 working sessions
- **Methodology:** PMI-aligned, Agile delivery

**Connect:** [LinkedIn](#) | [GitHub](#)

---

## Science References

The fitness recommendations in GAINR are grounded in peer-reviewed research:

- Progressive overload and hypertrophy: Schoenfeld, B.J. (2010). *The mechanisms of muscle hypertrophy and their application to resistance training.*
- Optimal training frequency: Ralston et al. (2017). *The Effect of Weekly Set Volume on Strength Gain.*
- Beginner progression rates: Aaberg, E. (2007). *Resistance Training Instruction.*
- Body recomposition: Barakat et al. (2020). *Body Recomposition: Can Trained Individuals Build Muscle and Lose Fat at the Same Time?*
- Deload protocols: Pritchard et al. (2015). *The Effects of Training Cessation on Muscular Performance.*

---

*GAINR is a personal portfolio project. It is not a medical device and does not provide medical advice. Always consult a qualified professional before beginning any exercise programme.*
