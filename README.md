# Agri Pulse

### AI-Driven Cash Flow Prediction & Risk Flagging System for Rural Micro Enterprises

---

## The Problem

India has millions of rural micro-enterprises — SHGs, FPOs, and individual entrepreneurs — that lack formal credit histories, limiting their access to structured financial services. Meanwhile, digital payments (UPI), market intelligence, and climate data have created a rich ecosystem of real-time economic signals — but these remain siloed and underutilized.

The result: financial stress goes unnoticed until it's a crisis. Institutions and field officers have no integrated way to see it coming.

## The Idea

**AgriPulse** fuses four otherwise-disconnected data streams — **financial records, UPI transaction proxies, market intelligence, and climate data** — into a single early-warning system for rural micro-enterprises. It forecasts cash flow 3–6 months ahead, flags financial stress before it becomes unmanageable, and delivers plain-language, explainable risk alerts to both entrepreneurs and field officers — even in low-connectivity areas.

No single data source can catch what all four can catch together. That fusion is the core bet.

---

## What Makes This Different

- **Signal fusion, not just forecasting** — most solutions in this space stop at "financial data → ML model." AgriPulse treats UPI trends, commodity prices, and climate shocks as first-class predictive signals, not afterthoughts.
- **Sector-aware risk logic** — dairy, poultry, food processing, handicrafts, and rural retail each have distinct stress signatures (e.g., fodder price spikes for dairy, disease-season flags for poultry). One generic risk score doesn't cut it.
- **Explainable by design** — every risk flag comes with a human-readable reason ("milk price down 12%, repayment delayed 2 months"), not an opaque score. Trust matters when this feeds real credit decisions.
- **Offline-first architecture** — risk classification runs on-device via a lightweight ONNX model, so field officers and entrepreneurs get instant alerts with zero dependency on connectivity. Heavier forecasting syncs to the cloud when available.

---

## Proposed Solution

A dual-interface platform:

| For Micro Enterprises | For Field Officers |
|---|---|
| Simple income/expense & savings/loan entry | Portfolio-wide risk heatmap |
| Real-time risk alerts (on-device) | Detailed enterprise profiles |
| Actionable, plain-language suggestions | Cash flow forecast view (3–6 months) |
| Works fully offline | Risk panel with drill-down explanations |

---

## Architecture

```
┌──────────────────────────────────────────────────────────┐
│                   DATA LAYER (mocked)                    │
│  Financial records │ Synthetic UPI signals │ Market data │
│  Real climate data (Open-Meteo) │ Commodity price trends │
└──────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│               FEATURE ENGINEERING LAYER                 │
│  Rolling cash flow aggregates · UPI volatility ·        │
│  Sector-specific risk features · Climate shock flags    | 
└─────────────────────────────────────────────────────────┘
                          │
                          ▼
┌───────────────────────────────────────────────────────────┐
│                      ML LAYER                             │
│  Cash Flow Forecaster (3–6 mo) · Risk Classifier          │
│  (Green/Amber/Red) · Sector Risk Overlay · SHAP explainer │
└───────────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│                    APPLICATION LAYER                    │
│  Enterprise App (offline-first, on-device inference)    │
│  Field Officer Dashboard (cloud, portfolio-level view)  │
└─────────────────────────────────────────────────────────┘
```

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React (PWA), Tailwind CSS, Recharts, service workers + IndexedDB for offline support |
| Backend | FastAPI (Python) |
| ML | XGBoost / LightGBM for forecasting & classification, SHAP for explainability, exported to ONNX for on-device inference |
| Data | Synthetic financial/UPI datasets (seasonality-aware), Open-Meteo (climate), Agmarknet-style commodity data |
| Cloud | AWS Amplify / S3 + CloudFront (frontend hosting), AWS Elastic Beanstalk on t3.micro (backend), Amazon RDS Postgres (data), AWS Lambda (offline-sync reconciliation) |
| Database | PostgreSQL |

Deployed entirely within AWS Free Tier limits for the hackathon build.

---

## Business Model & Impact

- **B2B2C via NABARD-affiliated institutions**: RRBs, cooperative banks, and NBFC-MFIs license the platform as a credit-appraisal support tool, paying per enterprise monitored.
- **Value to lenders**: earlier visibility into stress signals institutions currently can't see, potentially reducing NPAs and unlocking cheaper credit for enterprises with demonstrated repayment capacity.
- **Value to SHG/FPO federations**: bulk monitoring of member enterprises, supporting the transition from grants to institutional credit.
- **Sustainability path**: free/subsidized core platform as a NABARD-backed digital public good, with premium portfolio-analytics tiers for institutional users as the revenue layer.

---

## Project Status

This repository currently reflects the **ideation phase** of the NABARD Hackathon. Code, models, and datasets are in active development.


---


*Building for India's rural innovation journey — NABARD Hackathon, Global Fintech Fest 2026.*
