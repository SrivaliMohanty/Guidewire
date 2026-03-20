# 🛡️ GigShield — AI-Powered Parametric Income Insurance for India's Gig Economy

> **Guidewire DEVTrails 2026 Hackathon Submission**
> _Seed · Scale · Soar_

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Node](https://img.shields.io/badge/Node.js-20.x-green)
![React](https://img.shields.io/badge/React-18-blue)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-brightgreen)

---

## 📌 Problem Statement

India's 15M+ platform delivery partners (Zomato, Swiggy, Zepto, Amazon, Blinkit) lose **20–30% of monthly income** due to uncontrollable external disruptions — extreme rain, heat waves, severe pollution, and local curfews. They have **no safety net**.

GigShield is an **AI-enabled parametric insurance platform** that:
- Pays out automatically when a parametric trigger fires (no paperwork)
- Uses ML to calculate **dynamic weekly premiums** based on zone risk, segment, platform, and season
- Detects fraud with a multi-factor AI engine
- Covers **income loss only** (not health, life, accidents, or vehicle repair)
- Operates on a **weekly pricing model** aligned with gig worker earnings cycles

---

## 🎯 Persona Focus

**All three delivery segments supported:**

| Segment | Platforms | Key Disruptions |
|---------|-----------|-----------------|
| 🍕 Food Delivery | Zomato, Swiggy | Rain, Heat, Curfew, Strike |
| 🛒 Grocery/Q-Commerce | Zepto, Blinkit, Dunzo | Rain, Flood, Pollution |
| 📦 E-Commerce | Amazon, Flipkart | Storm, Curfew, Extreme Heat |

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                        GigShield Platform                        │
│                                                                   │
│  ┌──────────────┐     ┌──────────────┐     ┌──────────────────┐ │
│  │  React SPA   │────▶│  Express API │────▶│  MongoDB Atlas   │ │
│  │  (Vite)      │     │  (Node.js)   │     │  (Mongoose)      │ │
│  └──────────────┘     └──────┬───────┘     └──────────────────┘ │
│                              │                                    │
│              ┌───────────────┼───────────────┐                   │
│              ▼               ▼               ▼                   │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │ AI Risk      │  │ Disruption   │  │ Fraud        │          │
│  │ Engine       │  │ Monitor      │  │ Detection    │          │
│  │ (ML Premium) │  │ (CRON/API)   │  │ (AI Scoring) │          │
│  └──────────────┘  └──────┬───────┘  └──────────────┘          │
│                            │                                      │
│                            ▼                                      │
│               ┌────────────────────────┐                         │
│               │   OpenWeatherMap API   │                         │
│               │   (+ Mock fallback)    │                         │
│               └────────────────────────┘                         │
└─────────────────────────────────────────────────────────────────┘
```

---

## ⚙️ Tech Stack

### Frontend
| Tech | Purpose |
|------|---------|
| React 18 + Vite | SPA framework |
| React Router v6 | Client-side routing |
| Recharts | Analytics charts |
| Lucide React | Icon system |
| Axios | API calls |
| CSS Variables | Design system (no Tailwind needed) |

### Backend
| Tech | Purpose |
|------|---------|
| Node.js + Express | REST API server |
| MongoDB + Mongoose | Database + ODM |
| JSON Web Tokens | Auth |
| bcryptjs | Password hashing |
| node-cron | Scheduled disruption monitor |
| Axios | Weather API calls |

### AI/ML Services (Custom, no external ML lib needed)
| Service | Description |
|---------|-------------|
| `riskEngine.js` | Weighted multi-factor risk score (0-100) + dynamic premium |
| `fraudDetection.js` | Multi-rule fraud scoring: frequency, location, behavior, timing |
| `disruptionMonitor.js` | Real-time parametric trigger evaluation with API + mock fallback |

---

## 📁 Folder Structure

```
gigshield/
├── backend/
│   ├── models/
│   │   ├── Worker.js          # Worker/user schema with risk profile
│   │   ├── Policy.js          # Weekly insurance policy schema
│   │   ├── Claim.js           # Parametric claim with fraud fields
│   │   └── Disruption.js      # Disruption event log
│   ├── routes/
│   │   ├── auth.js            # Register, login, quote
│   │   ├── workers.js         # Worker CRUD
│   │   ├── policies.js        # Policy management
│   │   ├── claims.js          # Claims + auto-processing
│   │   ├── dashboard.js       # Analytics endpoints
│   │   └── disruptions.js     # Disruption check + simulate
│   ├── services/
│   │   ├── riskEngine.js      # 🤖 AI risk scoring + premium calculation
│   │   ├── fraudDetection.js  # 🛡️ Multi-factor fraud analysis
│   │   └── disruptionMonitor.js # 🌩️ Parametric trigger monitoring
│   ├── middleware/
│   │   └── auth.js            # JWT middleware
│   ├── server.js              # Entry point + cron setup
│   ├── seed.js                # Demo data seeder
│   ├── .env.example
│   └── package.json
│
├── frontend/
│   ├── src/
│   │   ├── pages/
│   │   │   ├── Landing.jsx      # Marketing landing page
│   │   │   ├── Login.jsx        # Auth with demo accounts
│   │   │   ├── Register.jsx     # 3-step onboarding + AI quote
│   │   │   ├── Dashboard.jsx    # Worker dashboard + charts
│   │   │   ├── Policy.jsx       # Policy management
│   │   │   ├── Claims.jsx       # Claims list + detail panel
│   │   │   ├── Simulator.jsx    # 🎮 Live disruption simulator
│   │   │   └── AdminDashboard.jsx # Insurer analytics
│   │   ├── components/
│   │   │   └── Layout.jsx       # Sidebar navigation
│   │   ├── context/
│   │   │   └── AuthContext.jsx  # Global auth state
│   │   ├── utils/
│   │   │   └── api.js           # Axios instance + interceptors
│   │   ├── App.jsx              # Routes
│   │   ├── main.jsx             # Entry point
│   │   └── index.css            # Full design system
│   ├── index.html
│   ├── vite.config.js
│   ├── vercel.json
│   └── package.json
│
├── render.yaml                  # One-click Render deployment
└── README.md
```

---

## 🤖 AI/ML Features

### 1. Risk Assessment Engine (`riskEngine.js`)

**Risk Score Formula (0–100):**
```
Risk Score = (
  Environmental Risk × 0.60   [flood/rain/heat/pollution zone data]
  + Social Risk × 0.40         [platform strike/crash history]
) × Exposure Factor             [daily hours / 10]
  × Experience Factor           [newer workers = higher risk]
  × Segment Multiplier          [food 1.2x, grocery 1.15x, ecommerce 1.0x]
```

**Tiers:**
- 🟢 Low (0–35): Stable zones, experienced workers
- 🟡 Medium (35–65): Moderate weather/social risk
- 🔴 High (65–100): Flood-prone/heat-heavy zones, new workers

**Dynamic Weekly Premium:**
```
Base Rate = 3% + (riskScore / 100) × 3%  [3–6% of weekly earnings]
Premium = (Base × avgWeeklyEarning) + Risk Loading - Platform Discount - Loyalty Discount
Minimum: ₹49/week
```

### 2. Parametric Triggers

| Trigger | Threshold | Unit |
|---------|-----------|------|
| 🌧️ Heavy Rain | > 50 | mm/3hr |
| 🌡️ Extreme Heat | > 42 | °C |
| 😷 Severe Pollution | > 300 | AQI |
| 🌊 Flood Alert | ≥ 1 | alert_level |
| 🌪️ Storm | > 60 | km/h wind |
| 🚫 Curfew/Strike | ≥ 1 | govt_order |

### 3. Fraud Detection Engine (`fraudDetection.js`)

Multi-rule scoring system:

| Rule | Score Impact | Description |
|------|-------------|-------------|
| High claim frequency | +30 | ≥5 claims/week |
| Repeated disruption type | +20 | Same type ≥3×/month |
| Duplicate claim window | +40 | New claim within 4 hours |
| Excessive payout | +25 | > 120% of daily coverage |
| New account claim | +20 | Account age < 24 hours |
| Location mismatch | +15 | Claim zone ≠ registered zone |
| No parametric data | +10 | Missing weather snapshot |

**Decision:**
- 0–29: ✅ Auto-approved → instant payout
- 30–59: ⚠️ Under review (manual check)
- 60+: 🚨 Flagged → payout blocked

---

## 🚀 Setup Instructions

### Prerequisites
- Node.js 18+
- MongoDB (local) or MongoDB Atlas (free tier)
- Git

### 1. Clone the Repository
```bash
git clone https://github.com/YOUR_USERNAME/gigshield.git
cd gigshield
```

### 2. Backend Setup
```bash
cd backend
npm install

# Configure environment
cp .env.example .env
# Edit .env with your MongoDB URI and optional OpenWeatherMap API key

# Seed the database with demo data
node seed.js

# Start the API server
npm run dev
# API runs on http://localhost:5000
```

### 3. Frontend Setup
```bash
cd frontend
npm install

# Configure environment
cp .env.example .env
# VITE_API_URL=http://localhost:5000/api  (default, no change needed for local)

# Start the dev server
npm run dev
# App runs on http://localhost:3000
```

---

## 🧪 Demo Credentials

| Role | Email | Password | Profile |
|------|-------|----------|---------|
| 🔧 Admin | `admin@gigshield.com` | `admin1234` | Full analytics access |
| 🍕 Food Worker | `rahul@demo.com` | `demo1234` | Zomato, Mumbai, High risk |
| 📦 E-com Worker | `priya@demo.com` | `demo1234` | Amazon, Delhi, Medium risk |
| ⚡ Grocery Worker | `arjun@demo.com` | `demo1234` | Zepto, Bangalore, Low risk |

---

## 🎮 Testing the Disruption Simulator

1. Log in as any worker (e.g., `rahul@demo.com`)
2. Navigate to **Disruption Lab** ⚡ in the sidebar
3. Select a disruption type (e.g., Heavy Rain 🌧️)
4. Adjust severity above the threshold
5. Click **Trigger Disruption Simulation**
6. Watch the AI process: weather fetch → trigger check → fraud analysis → payout
7. Navigate to **Claims** to see the generated claim with fraud score

---

## 📊 API Reference

### Auth
```
POST /api/auth/register    - Register + get AI risk profile
POST /api/auth/login       - Login
POST /api/auth/quote       - Get premium quote (no account needed)
```

### Policies
```
GET  /api/policies/my      - Get my policies
POST /api/policies/create  - Activate new weekly policy
GET  /api/policies/all     - All policies (admin)
GET  /api/policies/:id     - Policy detail
```

### Claims
```
GET  /api/claims/my        - My claims
POST /api/claims/trigger   - Manually trigger a claim (simulator)
GET  /api/claims/all       - All claims (admin)
PATCH /api/claims/:id/review - Approve/reject (admin)
```

### Dashboard
```
GET /api/dashboard/worker  - Worker stats + weekly chart
GET /api/dashboard/admin   - Platform-wide analytics
```

### Disruptions
```
GET  /api/disruptions/check/:city  - Current disruptions for city
POST /api/disruptions/simulate     - Trigger cron monitor manually
```

---

## 🌐 Deployment Guide

### Option A: Render (Recommended — free tier)

1. Push code to GitHub
2. Go to [render.com](https://render.com) → New → Blueprint
3. Connect your repo — `render.yaml` handles everything
4. Set environment variables:
   - `MONGODB_URI` → your Atlas connection string
   - `OPENWEATHER_API_KEY` → optional (mock works without it)
5. Deploy both services

### Option B: Vercel (Frontend) + Render (Backend)

**Backend on Render:**
```bash
# Root dir: backend
# Build: npm install
# Start: node server.js
# Env: MONGODB_URI, JWT_SECRET, NODE_ENV=production
```

**Frontend on Vercel:**
```bash
# Root dir: frontend
# Build: npm run build
# Output: dist
# Env: VITE_API_URL=https://your-backend.onrender.com/api
```

### Option C: Railway
```bash
# Install Railway CLI
npm i -g @railway/cli
railway login
railway init
# Deploy backend and frontend as separate services
```

---

## 🏆 Unique Features That Stand Out

### 1. 🤖 Zero-External-ML AI Engine
Custom-built risk scoring and fraud detection — no TensorFlow, no paid APIs. Pure actuarial + rule-based ML that runs anywhere.

### 2. ⚡ Live Disruption Simulator
Interactive demo tool where judges can trigger any disruption type, watch the full AI pipeline run in real time, and see the claim auto-generated.

### 3. 🗺️ Hyper-Local Zone Risk Database
City-level weather risk profiles (Mumbai flood risk vs Delhi heat risk vs Bangalore moderate risk) embedded directly in the engine.

### 4. 🔄 30-Minute CRON Monitor
Production-grade scheduled job that auto-monitors all active policy cities and creates claims without any worker action — true zero-touch insurance.

### 5. 📱 Dual Dashboard (Worker + Insurer)
Both perspectives built: workers see their coverage/claims, insurers (admin) see loss ratios, fraud rates, city/platform breakdowns, and monthly P&L trends.

### 6. 🛡️ GPS Spoofing Detection
Haversine-based impossibility check — if a claimed location requires physically impossible travel from the last known point, it's flagged automatically.

### 7. 💸 Weekly Pricing Model Compliance
Every financial calculation is structured weekly, not monthly or annually — matching exactly how gig workers earn and think about money.

---

## 📐 Financial Model

### Premium Calculation Example

For a **Zomato food delivery partner in Mumbai** earning ₹4,200/week:
```
Risk Score: 72/100 (HIGH — flood + rain risk)

Base Premium Rate: 3% + (72/100 × 3%) = 5.16%
Base Premium: ₹4,200 × 5.16% = ₹217/week
Risk Loading (high): ₹217 × 25% = +₹54
Loyalty Discount (18 months): ₹217 × 5% = -₹11
Platform Discount (none for Zomato): ₹0

Weekly Premium: ₹260/week
Weekly Coverage: ₹4,200 × 70% = ₹2,940/week
Daily Maximum: ₹490/day
```

### Payout Calculation Example

Trigger: Heavy rain 75mm (threshold: 50mm), 4-hour disruption
```
Coverage Ratio: 0.8 (75mm < 100mm → partial)
Hourly Rate: ₹490 / 8 = ₹61.25/hr
Payout: ₹61.25 × 4h × 0.8 = ₹196

→ ₹196 credited to UPI in ~60 seconds
```

---

## 🗓️ 6-Week Roadmap Alignment

| Phase | Weeks | Status | Deliverables |
|-------|-------|--------|-------------|
| Ideation & Foundation | 1–2 | ✅ | This README, architecture, tech stack |
| Automation & Protection | 3–4 | ✅ | Registration, policy, dynamic premium, claims |
| Scale & Optimise | 5–6 | ✅ | Fraud detection, instant payout, admin dashboard |

---

## ⚠️ Coverage Exclusions (Golden Rules Compliance)

GigShield strictly covers **INCOME LOSS ONLY** during parametric disruptions.

❌ NOT covered:
- Health insurance or medical bills
- Life insurance
- Accident coverage
- Vehicle repair or damage
- Personal liability

✅ Covered:
- Lost working hours due to rain/heat/flood/pollution exceeding thresholds
- Income loss during verified government curfews
- Income loss during platform-verified local strikes

---

## 🤝 Contributing

Built for DEVTrails 2026. PRs welcome after the hackathon.

---

## 📄 License

MIT © 2026 GigShield Team

---

_Built with ❤️ for India's 15 million delivery partners who power our daily lives._
