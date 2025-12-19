# CredResolve Intelligence Challenge (Kaggle)

## Competition Overview

This project is my solution for the **CredResolve Intelligence Challenge** on Kaggle.
The goal is to predict the **probability of successful payment recovery** for each borrower–action pair so that the system can choose the **most cost-effective collection channel** and maximize **Return on Action Spend (ROAS)**.

---

## Problem Statement

Debt recovery actions vary widely in cost:

* Digital (WhatsApp): very low cost
* Bot Call: low cost
* Human Call: medium cost
* Field Visit: very high cost

Using expensive actions unnecessarily reduces ROI.
The task is to estimate **P(payment | action)** for each lead so the evaluator can select the optimal action.

---

## Input Data

Multiple data sources joined using `lead_code`:

* **Train / Test**: lead–action pairs and target probability
* **Metadata**: total due amount, DPD bucket, state
* **WhatsApp Activity**: sent/read history
* **Human Calls & Bot Calls**: call outcomes and durations
* **Field Visits**: visit results from mobile app data

---

## Methodology

### Feature Engineering

* Aggregated interaction features (counts, rates, durations)
* Action-aware features (cost and intensity encoding)
* Missing interactions treated as *no activity*, not missing data

### Modeling

* Framed as a **regression problem** (target is a continuous probability)
* **LightGBM Regressor** with native categorical handling
* **Isotonic Regression** used for probability calibration

### Evaluation Insight

* Leaderboard metric optimizes **ROAS**
* Action selection depends on **relative ranking across actions**, not absolute accuracy
* Smooth predictions can score poorly without strong action separation

---

## Results

* Built a stable, well-calibrated probability model
* Identified that **decision-aware post-processing** is required to improve ROAS
* Demonstrated how action ranking impacts final evaluation score

---

