# 🛵 GigShield — AI-Powered Parametric Income Insurance for Food Delivery Partners

> **Guidewire DEVTrails 2026 | Phase 1 Submission**
> Protecting the livelihoods of India's food delivery workforce against uncontrollable external disruptions.

---

## 📌 Table of Contents

1. [Problem Context & Persona](#1-problem-context--persona)
2. [Core Solution Overview](#2-core-solution-overview)
3. [Persona-Based Scenarios & Application Workflow](#3-persona-based-scenarios--application-workflow)
4. [Weekly Premium Model & Parametric Triggers](#4-weekly-premium-model--parametric-triggers)
5. [AI/ML Integration Strategy](#5-aiml-integration-strategy)
6. [Adversarial Defense & Anti-Spoofing Strategy](#6-adversarial-defense--anti-spoofing-strategy)
7. [Tech Stack & Development Plan](#7-tech-stack--development-plan)
8. [Platform Choice Justification](#8-platform-choice-justification)
9. [Compliance & Coverage Boundaries](#9-compliance--coverage-boundaries)

---

## 1. Problem Context & Persona

### Target Persona: Food Delivery Partners (Zomato / Swiggy)

India has over **12 million active gig delivery workers**, with food delivery being the single largest segment. These workers operate in hyperlocal urban zones, typically completing 30–50 deliveries per day across a 8–10 hour shift. Their income is entirely tied to time-on-road.

**Key characteristics of our persona:**

| Attribute | Detail |
|-----------|--------|
| Income model | Per-delivery commission + surge bonuses |
| Earnings cycle | Weekly payout via platform wallet/UPI |
| Working hours | 10:00 AM–2:30 PM & 6:00 PM–11:00 PM (peak windows) |
| Primary disruption risk | Heavy rain, extreme heat, waterlogging, local curfews, platform outages |
| Geography | Tier 1 & Tier 2 Indian cities (Mumbai, Bengaluru, Delhi, Hyderabad, Pune) |
| Digital literacy | Moderate; comfortable with UPI apps & platform apps |

**The Income Gap Problem:**

When a city experiences heavy rainfall (AQI > 300 due to secondary dust storms, or ground flooding), food orders don't stop — but deliveries become physically impossible. A typical worker loses ₹800–₹1,400 per disrupted day with zero compensation from the platform. Over a bad monsoon week, that's ₹4,000–₹7,000 in lost wages — nearly 25–35% of their monthly income — with no recourse.

**GigShield is not health insurance, not accident coverage, not vehicle repair.** It is a weekly income safety net that automatically pays out when verifiable external conditions prevent a worker from earning.

---

## 2. Core Solution Overview

GigShield is a **web-based parametric insurance platform** built specifically for food delivery partners on Zomato and Swiggy. It uses real-time environmental data and AI-driven risk profiling to:

- **Automatically enroll** workers via a 3-minute onboarding flow
- **Dynamically price** weekly premiums based on hyper-local risk factors
- **Parametrically trigger** claims when pre-defined disruption thresholds are crossed — no manual claim filing required
- **Instantly disburse** payouts via UPI / platform wallet integration within minutes of trigger confirmation
- **Detect and block fraud** using multi-signal anomaly detection and GPS anti-spoofing logic

> 💡 Zero paperwork. Zero claim forms. If the rain hits, the payout follows.

---

## 3. Persona-Based Scenarios & Application Workflow

### Scenario A — Monsoon Flooding (Most Common)

**Situation:** Mumbai experiences 80mm rainfall in 4 hours. Roads in Andheri West and Kurla are waterlogged. Delivery partner Ramesh (Swiggy, Zone: Andheri) cannot complete any deliveries from 6 PM to 10 PM.

**GigShield Response:**
1. IMD rainfall API + OpenWeatherMap detects threshold breach (>50mm/4hr)
2. System cross-references Ramesh's registered active zone (Andheri West)
3. GPS last-seen confirms Ramesh was in the zone at disruption onset
4. Claim auto-initiated — no action needed by Ramesh
5. Payout of ₹350 (4 disrupted hours × hourly rate) credited to UPI within 30 minutes

### Scenario B — Extreme Heat Advisory

**Situation:** Hyderabad issues a heat advisory (>44°C). Outdoor deliveries deemed hazardous. Workers in Zone: Hitech City log significantly fewer orders between 1 PM–4 PM.

**GigShield Response:**
1. IMD heat alert API triggers zone-level disruption flag
2. Historical platform activity data (simulated) shows >40% drop in deliveries in the zone
3. Workers with active weekly policies in that zone receive automatic partial payout
4. ML model weighs delivery attempt rate to validate genuine disruption vs. worker absence

### Scenario C — Local Curfew / Unplanned Strike

**Situation:** A local political event results in sudden curfew in parts of Pune. Zomato/Swiggy pause deliveries for 3 hours.

**GigShield Response:**
1. Local news API / government alert feed detects zone-level curfew
2. Platform delivery pause (simulated via mock API) confirms disruption
3. Workers in active coverage zones auto-compensated for lost window
4. Fraud detection checks for workers who weren't logged in to platform during the window

### Application Workflow

```
[ Worker Onboarding ]
       ↓
[ Risk Profile Creation (AI) ]
       ↓
[ Weekly Policy Selection & Premium Payment ]
       ↓
[ Real-Time Disruption Monitoring ]
       ↓
[ Parametric Trigger Activated? ]
      / \
    YES   NO → Continue monitoring
     ↓
[ Fraud Validation Layer ]
      / \
  PASS   FAIL → Flag for review
     ↓
[ Auto Payout via UPI ]
       ↓
[ Worker Dashboard Updated ]
```

---

## 4. Weekly Premium Model & Parametric Triggers

### Why Weekly Pricing?

Food delivery workers are paid weekly by Zomato/Swiggy. A monthly insurance premium creates a cash-flow mismatch. Weekly pricing (₹29–₹89/week depending on risk tier) aligns perfectly with their earnings cycle, making micro-insurance affordable and psychologically easier to commit to.

### Premium Tiers (Base Structure)

| Tier | Weekly Premium | Coverage | Target Worker |
|------|---------------|----------|---------------|
| Basic | ₹29/week | Up to ₹600/disruption event | Low-risk zone, new worker |
| Standard | ₹49/week | Up to ₹1,000/disruption event | Mid-risk zone, established worker |
| Pro | ₹89/week | Up to ₹1,800/disruption event | High-risk zone, high-income worker |

**Dynamic Adjustment Factors (applied by ML model):**

- **Zone waterlogging history** (last 3 monsoon seasons) — up to ±20%
- **Historical avg deliveries/week** — higher activity = higher coverage need
- **Disruption frequency in worker's zone** (last 90 days) — risk multiplier
- **Claim history** — clean history = 5% loyalty discount
- **Platform tenure** — longer tenure = lower fraud risk = small discount

### Parametric Triggers (Loss of Income Only)

| Trigger | Data Source | Threshold | Payout Condition |
|---------|-------------|-----------|-----------------|
| Heavy Rainfall | OpenWeatherMap API / IMD | >50mm in 4 hrs in active zone | Worker GPS in zone at onset |
| Extreme Heat | IMD Heat Advisory API | >43°C + official advisory issued | Active policy + zone match |
| Severe Air Quality | CPCB AQI API | AQI >300 (Hazardous) for >2 hrs | Active shift window |
| Flood/Waterlogging | IMD + Google Maps flood layer | Zone-level flood alert | GPS + delivery attempt drop |
| Curfew / Civil Disruption | Gov alert API + platform pause signal | Platform deliveries paused >1hr | Active login on platform |

> ⚠️ **Coverage Exclusions (Hard Rules):** No payouts for vehicle breakdown, health issues, personal accidents, or self-reported claims without verified parametric trigger.

---

## 5. AI/ML Integration Strategy

### 5.1 Dynamic Premium Calculation Model

**Implementation:** Gradient Boosted Decision Tree using `ml-cart` / `ml-random-forest` (Node.js ml-js library ecosystem)

**Input Features:**
- Worker zone's historical rainfall/heat disruption frequency
- Zone-level delivery density (proxy for income potential)
- Worker's average weekly earnings (from simulated platform data)
- Time of year (monsoon season weight)
- City tier (risk index by city)

**Output:** Weekly premium in ₹, coverage limit, risk tier classification

**Training Approach:** Initially trained on synthetic data modeled after IMD historical weather records and approximated gig worker income data. Model weights serialized to JSON and loaded at server startup. Retrained monthly as real claim data accumulates.

### 5.2 Risk Profiling at Onboarding

During onboarding, the worker provides:
- City and primary delivery zone
- Approximate weekly earnings
- Active platform (Zomato / Swiggy)

The AI model immediately generates a **risk profile score (0–100)** that determines starting premium, coverage limits, and fraud sensitivity thresholds.

### 5.3 Claim Anomaly Detection

**Implementation:** Isolation Forest logic implemented in Node.js using `isolation-forest` npm package

**Signals monitored:**
- GPS location at time of trigger (must be in claimed zone)
- Platform activity log (was the worker logged into the app?)
- Historical claim frequency (>2 claims/month flagged for review)
- Trigger co-occurrence (is the worker claiming in a zone where no other workers triggered?)
- Device fingerprint consistency

**Output:** Anomaly score → Auto-approve / Hold for review / Auto-reject

### 5.4 Predictive Disruption Forecasting (Admin Dashboard)

**Implementation:** Time-series LSTM using `brain.js` (Node.js neural network library)

- 7-day forward forecast of disruption probability by zone
- Enables insurer to pre-allocate liquidity for likely payout weeks
- Alerts insurer when predicted claim surge may stress the liquidity pool

---

## 6. Adversarial Defense & Anti-Spoofing Strategy

> 🚨 **Market Crash Scenario Response**
> 500 delivery partners. Coordinated GPS spoofing. Fake zone presence. ₹X lakh drained in fraudulent payouts. Here is GigShield's multi-layer defense architecture to prevent and detect this.

### The Attack Pattern We're Defending Against

A fraud ring operates as follows:
1. Multiple workers (real or synthetic accounts) register in a high-risk zone
2. During a genuine disruption event (e.g., heavy rain), they spoof GPS to place themselves in the trigger zone
3. They claim payouts while never actually being present or attempting deliveries
4. Coordinated timing maximizes the number of fraudulent claims in a single event

### Layer 1 — GPS Signal Integrity Validation

Simple GPS coordinate matching is dead. We go deeper:

- **Movement entropy check:** A genuine worker's GPS trace shows micro-movement (turns, stops, starts). A spoofed static coordinate shows zero entropy. We flag accounts with <5m movement variance during a 30-min window as suspicious.
- **Speed-vector plausibility:** GPS coordinates must follow physically plausible routes. Teleportation between two points (e.g., 3km in 45 seconds) is an automatic fraud flag.
- **Device sensor fusion:** Cross-reference GPS with accelerometer/gyroscope data (mobile SDK). A stationary phone claiming delivery-zone presence is flagged.
- **Cell tower triangulation cross-check:** Where available, cross-check GPS claim against network-reported cell tower location. Major discrepancy = spoofing signal.

### Layer 2 — Platform Activity Correlation

A worker claiming disruption-based loss must have been actively trying to work:

- **Platform login verification:** Worker must be logged into Zomato/Swiggy app during the disruption window (verified via simulated platform API integration)
- **Order acceptance attempt:** Was the worker receiving or attempting orders before the trigger? Zero activity = no loss of income = no payout
- **Delivery attempt logs:** Even if deliveries weren't completed, the attempt trail (order received, route started) must exist

### Layer 3 — Cohort Behavioral Analysis (Ring Detection)

This is the key layer for catching coordinated fraud rings:

- **Zone claim density scoring:** If >15% of all workers claiming in a zone during a single event are new accounts (<4 weeks old), the batch is flagged for manual review
- **Claim timing clustering:** Legitimate claims arrive in a Poisson distribution across the disruption window. A fraud ring produces a suspicious spike — many claims filed within minutes of each other. Burst detection algorithm flags clusters with >3 standard deviations above baseline claim rate
- **Social graph analysis:** If multiple flagged accounts share device IDs, IP addresses, or UPI beneficiary accounts, the entire cohort is suspended pending investigation
- **New account velocity check:** Accounts created <7 days before a major disruption event are automatically held — payouts pending 48-hour manual review

### Layer 4 — Historical Disruption Consistency Check

Fake claims often appear in zones during events that don't geographically match historical patterns:

- A worker claiming flood disruption in a zone with zero historical waterlogging incidents scores a high anomaly flag
- AQI-based claims in zones geographically distant from industrial pollution sources are cross-validated against the nearest CPCB monitoring station, not just the claimed zone

### Layer 5 — Progressive Trust Model

Not all fraud is a ring. Some is opportunistic. We prevent punishing honest workers:

- Workers with 8+ weeks of clean history get a **Trusted Worker** badge — lower scrutiny thresholds, faster payouts
- First-time claimants (even for legitimate events) receive a small 4-hour payout hold while a lightweight automated check runs
- Fraud-flagged workers receive a **review notice**, not an instant ban — appeals process built in to prevent false positive punishment
- Workers who attempt fraud (confirmed) are blacklisted from the platform and reported to the aggregated industry fraud database (in future phases)

### Quantified Risk Thresholds

| Signal | Flag Type | Action |
|--------|-----------|--------|
| GPS entropy < 5m in 30min | Soft flag | Payout held 2 hours, re-check |
| Platform not logged in during event | Hard block | Auto-reject claim |
| Claim filed <72hrs after account creation | Soft flag | Manual review queue |
| >2 claims in 7 days | Soft flag | Anomaly score review |
| Cohort burst: >20 claims in 5 minutes from same zone | Hard block | Entire cohort held, alert raised |
| Device ID shared with another account | Hard block | Both accounts suspended |
| GPS vs. cell tower discrepancy >2km | Hard block | Auto-reject + flag for investigation |

---

## 7. Tech Stack & Development Plan

### Tech Stack

**Frontend (Worker-facing):**
- React Native (iOS + Android mobile app)
- Expo (for faster build/test cycles)
- React Query for API state management

**Frontend (Admin/Insurer-facing):**
- React.js (Web dashboard)
- Tailwind CSS for UI
- Recharts for analytics visualizations

**Backend:**
- Node.js + Express.js (unified REST API for both mobile and web)
- ML logic implemented in JavaScript using **ml-js / brain.js** libraries (XGBoost-equivalent gradient boosting and anomaly detection — no separate Python service needed)
- PostgreSQL (primary database — policies, claims, workers, fraud flags)
- Redis (real-time trigger state, session management, rate limiting)

**External Integrations (Free Tier / Mock):**
- OpenWeatherMap API (weather triggers)
- CPCB AQI API (air quality triggers)
- IMD alert RSS feed (flood/heat advisories)
- Razorpay Test Mode (payout simulation)
- Simulated platform API (mock Zomato/Swiggy activity logs via local JSON fixtures)

**Infrastructure:**
- Docker (containerized Node + PostgreSQL + Redis)
- GitHub Actions (CI/CD)
- Render / Railway 
### 6-Week Development Plan

| Phase | Weeks | Focus | Key Deliverables |
|-------|-------|-------|-----------------|
| Phase 1 | 1–2 | Ideation & Foundation | README, architecture design, DB schema, mock data setup |
| Phase 2 | 3–4 | Core Platform Build | Onboarding flow, policy creation, premium calculator, trigger monitoring, claims UI |
| Phase 3 | 5–6 | Fraud, Payouts & Dashboard | Fraud detection engine, Razorpay mock payouts, analytics dashboard, final polish |

---

## 8. Platform Choice Justification

**We are building for both Web and Mobile**, using a dual-surface strategy:

| Surface | Use Case | Audience |
|---------|----------|----------|
| **Mobile App (React Native)** | Daily worker interactions — policy status, payout alerts, active coverage view | Delivery partners (primary users) |
| **Web App (React.js)** | Insurer admin dashboard, analytics, fraud review queue, policy management | Insurance ops team (admin users) |

**Why Mobile for workers:**
1. Delivery partners spend 90% of their digital time on their phones — a mobile app puts GigShield one tap away
2. Push notifications are critical: workers need instant alerts when a disruption triggers and when a payout lands
3. GPS and accelerometer access (required for our anti-spoofing layer) is far more reliable via a native mobile app than a browser

**Why Web for admin/insurer:**
1. Analytics dashboards, fraud review queues, and policy management require a larger screen experience
2. The insurer-side users are office-based and expect a full browser interface
3. Web deployment allows faster iteration on the admin panel without app store cycles

**Shared backend:** Both surfaces connect to the same Node.js REST API, ensuring a single source of truth for all policy, claims, and fraud data.

---

## 9. Compliance & Coverage Boundaries

GigShield strictly adheres to the following constraints:

| ✅ Covered | ❌ Explicitly Excluded |
|-----------|----------------------|
| Income loss during verified weather disruption | Health insurance of any kind |
| Income loss during verified civic disruption (curfew/strike) | Accident or hospitalization coverage |
| Income loss during platform-wide outage (simulated) | Vehicle repair or maintenance |
| Partial income loss (hourly proration) | Any self-reported claims without parametric trigger |

All parametric triggers are based on **third-party verifiable data sources** — no worker-initiated claims, no subjective assessments.

---
