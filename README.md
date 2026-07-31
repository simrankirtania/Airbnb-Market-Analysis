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
├── data/
│   ├── Listings.csv                                     # 279,712 listings, 30+ fields
│   └── Reviews.csv                                      # 5.37M reviews (proxy for bookings)
├── 01_excel_audit/
│   └── Airbnb_Data_Audit_Report_2.xlsx                  # Data quality audit workbook
├── 02_sql_analysis/
│   ├── Airbnb_Marketplace_Intelligence_-_SQL_Analytics.ipynb   # SQLite-based business analysis
│   └── Airbnb_SQL_Business_Insights_Summary.docx
├── 03_python_eda/
│   ├── Airbnb_Python_EDA_Statistical_Insights.ipynb     # EDA, hypothesis tests, ML
│   └── Airbnb_Multi-City_Dataset_Python_EDA_Statistical_Insights.docx
├── 04_power_bi/
│   ├── Airbnb_Global_Marketplace_Intelligence.pbix      # Interactive dashboard (4 pages)
│   ├── Airbnb_Power_BI_Dashboard_.pdf                   # Static export
│   └── POWER_BI_DAX.docx                                # All DAX measures & calculated columns
├── docs/
│   ├── Data_Set_Dictionary.docx                         # Field-level data dictionary
│   ├── Airbnb_Marketplace_Intelligence_Project_Business_Questions.docx
│   └── Airbnb_Executive_Business_Insights_Summary.docx  # Final rollup report
└── README.md
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

📄 Full write-up: [`Airbnb_SQL_Business_Insights_Summary.docx`](./02_sql_analysis/Airbnb_SQL_Business_Insights_Summary.docx)

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

📄 Full write-up: [`Airbnb_Multi-City_Dataset_Python_EDA_Statistical_Insights.docx`](./03_python_eda/Airbnb_Multi-City_Dataset_Python_EDA_Statistical_Insights.docx)

---

## 📊 Stage 4 — Power BI: Executive Dashboard

**Goal:** Turn all of the above into an interactive, filterable tool executives can actually use.

**4 report pages:**

| Page | Purpose |
|---|---|
| **Market Health & Growth** | Composite Marketplace Health Score (gauge), KPI cards (listings, hosts, rating, superhost rate, response rate, YoY growth), listings vs. demand-growth combo chart by city |
| **Regional Market Analysis** | Bubble chart of price (city-standardized z-score) vs. rating by room type, monthly demand-trend lines by city, neighbourhood demand concentration (Pareto) |
| **Listing Quality Monitoring** | Table of 174 flagged listings (invalid price/capacity/night-range data or persistently low ratings) for operational follow-up |
| **Executive KPI Cadence** | A one-page playbook defining *what* to track and *how often* (daily/weekly/monthly), tying every visual back to a decision cadence |

**Notable DAX work** (see [`POWER_BI_DAX.docx`](./04_power_bi/POWER_BI_DAX.docx)):
- A custom **Marketplace Health Score** (0–100) blending rating, Superhost rate, response rate, YoY growth, and review engagement, each weighted by business importance
- A `flag_reason` calculated column that programmatically classifies data-quality issues (invalid price/capacity, broken night ranges, persistently low ratings with sufficient review volume)
- City-relative pricing via `price_z_within_city` (removes local-currency/market-level effects for fair cross-city comparison)
- Pareto-style `Cumulative %` and `Neighbourhood Rank` measures for demand-concentration analysis
- A full Date dimension table and YoY growth measures built from the Reviews table (used as a demand/booking-activity proxy)

**Headline dashboard metrics:**
- Marketplace Health Score: **54.55 / 100** (Target: 75) — signals real, actionable room for improvement, not a vanity metric
- 279,712 listings · 182,024 hosts · 93.41 average rating · 17.98% Superhost rate · 86.59% response rate · 42.98% YoY growth
- **174 listings flagged** for invalid data or persistently low ratings, ready for the ops team

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

Public multi-city Airbnb listings and reviews data (Listings ~152 MB, Reviews ~244 MB — hosted externally / via Git LFS due to GitHub file-size limits; see `data/README.md` for download instructions if not included in this repo).

---

## 🙋 About This Project

Built as a portfolio project to demonstrate a complete, production-style analytics workflow — from raw, messy data to an executive decision-making tool — with an emphasis on **honest, defensible insights** (e.g., explicitly reporting the Random Forest's limited explanatory power rather than overstating model performance).

**Author:** Simran Kirtania — MSc Economics, aspiring Data Analyst
📧 [Add your email] · 🔗 [Add your LinkedIn] · 🌐 [Portfolio](https://simrankirtaniaportfolio.netlify.app)
