# 🏠 Airbnb Global Marketplace Intelligence

**An end-to-end data analytics project** — Excel → SQL → Python → Power BI — analyzing **279,712 listings**, **182,024 hosts**, and **5.37M+ reviews** across **10 global cities** to uncover pricing, host performance, and customer demand insights for a simulated Airbnb marketplace operations team.

![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Tools](https://img.shields.io/badge/tools-Excel%20%7C%20SQL%20%7C%20Python%20%7C%20Power%20BI-blue)

---

## 📌 Project Overview

Airbnb marketplace teams need to answer a recurring set of questions: *Where is the marketplace growing? Which listings need attention? Are Superhosts actually worth promoting? Is pricing fair relative to the local market?*

This project simulates a real analytics engagement — starting with messy raw data and ending in an executive-ready Power BI dashboard — using a **four-stage pipeline**, each stage answering a defined set of business questions and feeding the next:

```
Excel Audit  →  SQL Analysis  →  Python EDA & Statistics  →  Power BI Dashboard
(data quality)   (business qs)    (why it happens)            (executive decisions)
```

**Cities covered:** Paris, New York, Sydney, Rome, Rio de Janeiro, Istanbul, Mexico City, Bangkok, Cape Town, Hong Kong

---

## 🗂️ Repository Structure

```
Airbnb-Global-Marketplace-Intelligence
│
├── 📁 1. Airbnb_Data_Audit_Report
│   ├── Airbnb_Data_Audit_Report.pdf
│   └── Airbnb_Data_Audit_Report.xlsx
│
├──  0. Airbnb_Marketplace_Intelligence_Project_Business_Questions.pdf
├──  2. Airbnb Marketplace Intelligence - SQL Analytics.ipynb
├──  3. Airbnb Marketplace Intelligence - Python EDA & Statistical Insights.ipynb
├──  4. Airbnb Marketplace Intelligence - Power BI Dashboard.pdf
├──  LICENSE
└──  README.md
```

---

## 🧩 Stage 1 — Excel: Data Audit & Initial Exploration

**Goal:** Is the raw data complete, accurate, and analysis-ready?

A structured audit workbook (`Read Me → Executive Summary → 6 analysis tabs → raw data tabs`) was built to check:
- Duplicate and integrity checks (listing IDs, host IDs, referential integrity between Listings and Reviews)
- Missing value and inconsistency scans across 30+ fields
- Distribution checks across cities, neighbourhoods, property types, and room types
- Initial pricing patterns and outlier/anomaly flags (invalid prices, zero capacity, broken min/max night ranges)
- High-level pre-analysis trends

**Output:** A clean, audited dataset and a documented list of data quality issues that were carried forward and explicitly handled (not hidden) in every later stage.

---

## 🗄️ Stage 2 — SQL: Business Analysis (SQLite via Python)

**Goal:** Answer core business questions with structured queries against a locally-built SQLite database.

10 business questions were answered with SQL, including:
1. Which cities/neighbourhoods have the largest marketplaces?
2. Which markets generate the highest demand (review volume)?
3. How do property type, room type, and capacity influence pricing?
4. Which hosts consistently outperform others?
5. Do Superhosts deliver a measurably better guest experience?
6. How does host experience affect performance?
7. Which listings are over/underpriced vs. local market averages?
8. What seasonal trends exist in reviews/bookings?
9. Which neighbourhoods drive the bulk of demand (Pareto/80-20 analysis)?
10. What KPIs should executives track, and at what cadence?

**Key findings:**
- **Paris** is the largest single market (64,690 listings), followed by New York and Sydney — but supply is concentrated in a handful of neighbourhoods per city.
- **Rome** has the highest average reviews per listing despite Paris having the highest total volume — demand intensity ≠ marketplace size.
- **Superhosts** outperform regular hosts on ratings, cleanliness, communication, and response/acceptance rates.
- Many listings sit **>50% away** from their local city price average — underpriced listings substantially outnumber overpriced ones.
- In Paris, roughly **70% of neighbourhoods generate ~80% of reviews** — a classic Pareto concentration.


---

## 🐍 Stage 3 — Python: Exploratory Data Analysis & Statistical Modeling

**Goal:** Go beyond SQL aggregates — test relationships statistically and surface patterns invisible to simple queries.

**Techniques used:**
- Feature engineering: `Price per Guest`, `Host Experience (years)`, `Review Density`, `Price Z-score within City`, `Has Reviews`
- Correlation analysis and scatter plots (pricing vs. ratings vs. host characteristics)
- **Random Forest regression** for price drivers (feature importance ranking)
- **Isolation Forest** for multivariate outlier/anomaly detection
- Hypothesis testing (Superhost vs. Regular Host; Instant Book vs. Request-to-Book) with distribution comparisons

**Key findings:**
- **Cleanliness and communication** — not price — are the strongest drivers of overall guest rating.
- The Random Forest model explains only **~7.1%** of price variation from available fields, honestly indicating that real pricing drivers (exact location, interior quality, amenities, seasonality) aren't fully captured in this dataset — a deliberately reported *limitation*, not an inflated claim.
- **Superhosts outperform regular hosts** across nearly every service metric **without charging meaningfully higher prices** — quality, not price premium, is the differentiator.
- **Instant Book** listings get more reviews (more bookings) but *not* meaningfully higher ratings — it drives activity, not satisfaction.
- **Isolation Forest** flagged ~2% of listings as multivariate outliers worth manual review.
- Paris prices are strongly right-skewed by a small number of luxury listings — median, not mean, is the more honest "typical price" metric.

---

## 📊 Stage 4 — Power BI: Executive Dashboard

**Goal:** Turn all of the above into an interactive, filterable tool executives can actually use.

---

## 🏠 Page 1 — Market Health & Growth

**Business Question**
- What is the overall health of the Airbnb marketplace?
- Which cities present the greatest growth opportunities?

**Highlights**
- Executive KPI Cards
- Marketplace Health Score
- Market Size vs YoY Growth
- Interactive slicers

### Dashboard Preview

<p align="center">
<img width="1342" height="751" alt="image" src="https://github.com/user-attachments/assets/9a2b5036-d45f-4772-8b0a-f173a484d9d3" />
</p>


---

## 🌍 Page 2 — Marketplace & Demand Analysis

**Business Question**
- How do pricing, quality, and customer demand vary across regions?

**Highlights**
- Pricing vs Guest Rating Analysis
- Monthly Demand Trends
- Neighbourhood Demand Concentration (Pareto Analysis)
- Cross-filtering between visuals

### Dashboard Preview

<p align="center">
  <img width="668" height="376" alt="Screenshot 2026-07-31 003621" src="https://github.com/user-attachments/assets/a1574d49-d1a7-4991-a92e-e9c15d962bc9" />
</p>

---

## 🚩 Page 3 — Needs Operational Attention

**Business Question**
- Which listings require operational attention?

**Highlights**
- Flagged Listings Table
- Data Quality Issues
- Low-Rated Listings
- Invalid Pricing & Night Rules

### Dashboard Preview

<p align="center">
  <img width="667" height="365" alt="Screenshot 2026-07-31 003635" src="https://github.com/user-attachments/assets/2a73e2c7-8090-4cd2-9b8b-c842d6207934" />
</p>

---

## 📅 Page 4 — Executive KPI Cadence

**Business Question**
- What should executives monitor daily, weekly, and monthly?

**Highlights**
- KPI Monitoring Framework
- Operational Priorities
- Executive Reporting Schedule
- Decision Support Guide

### Dashboard Preview

<p align="center">
  <img width="668" height="369" alt="image" src="https://github.com/user-attachments/assets/1bb7def3-9715-4d9e-aa40-b41694e813aa" />
</p>

---

## 🎯 Key Business Recommendations

1. **Pricing guidance:** Systematically flag and message underpriced listings (which outnumber overpriced ones) — a direct host-revenue lever.
2. **Superhost expansion:** Since Superhosts improve quality metrics without raising prices, growing the Superhost program is a low-cost lever for marketplace-wide quality.
3. **Demand diversification:** With demand concentrated in a small number of neighbourhoods (Pareto effect), target marketing/inventory investment in high-potential secondary neighbourhoods.
4. **Operational triage:** Use the 174 flagged listings + the Health Score's engagement component to catch broken or under-serving listings before they hurt guest experience.
5. **KPI governance:** Adopt the daily/weekly/monthly cadence defined in the dashboard rather than reviewing all metrics at once.

---

## 🛠️ Tools & Skills Demonstrated

| Category | Tools / Techniques |
|---|---|
| Data Auditing | Excel (formulas, conditional logic, pivot-based distribution checks) |
| Database & Querying | SQL (SQLite), Python (`sqlite3`, `pandas`) |
| Statistical Analysis | Correlation, hypothesis testing (t-tests), distribution analysis |
| Machine Learning | Random Forest Regression (feature importance), Isolation Forest (anomaly detection) |
| Business Intelligence | Power BI, DAX (calculated columns, measures, time intelligence, ranking/Pareto logic) |
| Data Storytelling | Executive KPI design, health-score composite metrics, business-question-driven structure |

---

## 📁 Data Source

Public multi-city Airbnb listings and reviews data (Listings ~152 MB, Reviews ~244 MB — hosted externally due to GitHub file-size limits.

---

## 🙋 About This Project

Built as a portfolio project to demonstrate a complete, production-style analytics workflow — from raw, messy data to an executive decision-making tool — with an emphasis on **honest, defensible insights** (e.g., explicitly reporting the Random Forest's limited explanatory power rather than overstating model performance).

**Author:** Simran Kirtania — MSc Economics, aspiring Data Analyst
📧 simrankirtania02@gmail.com · 🔗 [LinkedIn](https://www.linkedin.com/in/simrankirtania/) · 🌐 [Portfolio](https://simrankirtaniaportfolio.netlify.app)
