<div align="center">

# 👁️ PROJECT DRISHTI
### AI-Powered Proactive Intelligence Radar for Cybercrime & Mule Account Interception

[![SIH 2026](https://img.shields.io/badge/SIH-2026-orange.svg?style=for-the-badge)](https://www.sih.gov.in/)
[![Problem Statement](https://img.shields.io/badge/Problem_Statement-SIH26184-blue.svg?style=for-the-badge)](https://www.sih.gov.in/)
[![Partner Agency](https://img.shields.io/badge/Agency-I4C_%7C_MHA-red.svg?style=for-the-badge)](https://i4c.mha.gov.in/)
[![Status](https://img.shields.io/badge/Status-Active_Development-success.svg?style=for-the-badge)]()

<p align="center">
  <b>Smart India Hackathon 2026 — Indian Cybercrime Coordination Centre (I4C), Ministry of Home Affairs</b><br />
  <i>Transforming Cybercrime Policing from Reactive Tracing to Real-time Physical Interception.</i>
</p>

</div>

---

## 🎯 Executive Summary & The Core Problem

When an innocent citizen falls victim to cyber fraud (OTP scam, KYC phishing, fake investment schemes), stolen money is rapidly routed through a multi-tiered hierarchy of **"mule" bank accounts**. Within minutes, runners physically withdraw hard currency from distant ATMs or Banking Correspondents (BCs).

Today, law enforcement relies purely on **reactive tracing**. Police begin investigation hours or days after the incident report. By the time accounts are frozen via 1930 / CFCFRMS, the accounts have zero balance and the criminal has vanished.

### ⚡ The Drishti Solution (Proactive Forecasting)
**Project Drishti** is an active intelligence radar for cyber enforcement agencies. The instant stolen funds hit a designated mule network, Drishti answers two exact operational questions *before* scammers reach the cashpoint:

```
                  ┌────────────────────────────────────────┐
                  │          ACTIVE FRAUD EVENT            │
                  └───────────────────┬────────────────────┘
                                      │
               ┌──────────────────────┴──────────────────────┐
               ▼                                             ▼
  ┌─────────────────────────┐                   ┌─────────────────────────┐
  │         WHERE?          │                   │          WHEN?          │
  │  Ranked Top-5 Physical  │                   │  Exact cashout window   │
  │  ATMs the mule is heading│                   │  (e.g., "in 25–40 min") │
  │  to right now.          │                   │  derived from survival. │
  └─────────────────────────┘                   └─────────────────────────┘
               │                                             │
               └──────────────────────┬──────────────────────┘
                                      ▼
                  ┌────────────────────────────────────────┐
                  │ 🚨 ACTIONABLE POLICE DISPATCH (20 MIN) │
                  │  Patrol units alerted with exact route │
                  │  and high-probability ATM coordinates. │
                  └────────────────────────────────────────┘
```

> ⏱️ **Operational Outcome:** Gives local PCR vans and field patrol officers a **20+ minute actionable window** to intercept criminals red-handed at the ATM.

---

## 📦 Core Repositories

| Repository | Purpose | Primary Stack |
|---|---|---|
| 🏛️ [**project-drishti**](https://github.com/project-drishti-sih26/project-drishti) | **Master Monorepo & Implementation:** Contains FastAPI Backend, ML Predictive Engine, Mapbox GL JS Command Radar, UI/UX Dashboard, and Synthetic Data Pipeline. | Python 3.11+, React (Vite), Tailwind, Mapbox GL JS, PostgreSQL/PostGIS, Docker |
| ⚙️ [**.github**](https://github.com/project-drishti-sih26/.github) | **Organization Profile & Workflows:** Global organization landing page, community health, and templates. | Markdown, GitHub Actions |

---

## 🧠 Dual-Engine Machine Learning Pipeline

1. **WHERE Engine (Retrieval + Learning-to-Rank):**
   * **Stage 1 (Uber H3 Spatial Hex Pruning):** Filters 100,000+ national ATMs down to ~200 reachable candidates within the travel time horizon using pre-computed road travel distance matrices.
   * **Stage 2 (LightGBM LambdaMART LTR):** Scores and ranks the candidates based on travel duration, ATM historical fraud density, and historical mule network affinity.
   * **Cold-Start Fallback:** For brand new mules with zero history:
     $$\text{Score} = (\text{Fraud\_History} \times 0.7) + \left(\frac{1}{\text{Distance}} \times 0.3\right)$$
2. **WHEN Engine (Survival Analysis):**
   * Employs **Survival Analysis** (`lifelines` — Kaplan-Meier / Cox Proportional Hazards) to forecast the probability density function of cashout timing, generating an active time window (e.g., *"14:32 to 14:48"*).
3. **AI Explainability (SHAP):**
   * Translates tree weights into plain language: *"Rank #1 ATM: 6-min road travel time + historically used by this mule network in 3 prior frauds."*

---

## 👥 Granular Team Breakdown (Squad of 6)

| Role | Title | Core Ownership | Deliverables |
|:---:|:---|:---|:---|
| **Role 1** | **Backend Engineer** | [`backend/`](https://github.com/project-drishti-sih26/project-drishti/tree/main/backend) | SQLAlchemy models, FastAPI REST APIs, ML trigger logic (`> ₹50,000`), WebSocket alert stream. |
| **Role 2** | **ML/AI Engineer** | [`ml_engine/`](https://github.com/project-drishti-sih26/project-drishti/tree/main/ml_engine) | LightGBM LambdaMART ranker, `lifelines` survival time model, SHAP explainability strings, fallback formula. |
| **Role 3** | **Frontend Engineer (GIS)** | [`frontend/src/components/Map/`](https://github.com/project-drishti-sih26/project-drishti/tree/main/frontend/src/components/Map) | Mapbox GL JS dark radar, smooth `map.flyTo()` zoom animations, H3 spatial hex danger overlays. |
| **Role 4** | **Frontend Engineer (UI/UX)** | [`frontend/src/components/UI/`](https://github.com/project-drishti-sih26/project-drishti/tree/main/frontend/src/components/UI) | 3-column layout, Live Case Flow visualizer, Top-5 cards, 1-Click Police Dispatch PDF. |
| **Role 5** | **Data Engineer** | [`simulation/`](https://github.com/project-drishti-sih26/project-drishti/tree/main/simulation) | `atms_master.csv`, pre-computed distance matrix, `run_live_demo.py` presentation trigger. |
| **Role 6** | **Integrator & DevOps** | Root, [`docker/`](https://github.com/project-drishti-sih26/project-drishti/tree/main/docker), [`docs/`](https://github.com/project-drishti-sih26/project-drishti/tree/main/docs) | `docker-compose.yml`, E2E latency optimization (< 2s), presentation deck and pitch choreography. |

---

## 🚀 Quickstart & Setup

```bash
# 1. Clone the master repository
git clone git@github.com:project-drishti-sih26/project-drishti.git
cd project-drishti

# 2. Configure environment
cp .env.example .env

# 3. Spin up the full system in one command
docker-compose up --build

# 4. Trigger a live cyber fraud simulation event
python simulation/run_live_demo.py
```

---

<div align="center">
  <b>Built with ❤️ by Team Project Drishti for Smart India Hackathon (SIH 2026)</b><br />
  <sub>Partnered with Indian Cybercrime Coordination Centre (I4C), Ministry of Home Affairs</sub>
</div>
