# Loan Default Risk Analytics — Digital Lending Platform (NBFC)

An end-to-end data analytics project simulating the work of a Data Analyst on a lending company's Risk & Credit team: extracting data with SQL, cleaning it, running exploratory analysis, engineering risk features, building an interactive dashboard, and training a baseline predictive model.

## Business Problem

A digital lending NBFC wants to understand **which applicant segments default most often** and needs an early-warning risk score to flag high-risk loan applications before disbursement, so the credit team can prioritize manual underwriting review.

## Dataset

`loan_applications_raw.csv` — 6,000 synthetic loan applications (Jan 2024 – Dec 2025) generated to reflect realistic NBFC lending patterns: applicant demographics, income, credit score, loan details, and a default flag. The raw file intentionally contains duplicate records, invalid negative ages, and missing income values to mirror a real production data export.

| Column | Description |
|---|---|
| applicant_id | Unique applicant reference |
| age, gender, state | Applicant demographics |
| employment_type | Salaried / Self-Employed / Business Owner |
| monthly_income | Applicant's monthly income (₹) |
| credit_score | Bureau credit score (300–900) |
| loan_purpose, loan_amount, tenure_months, interest_rate, emi | Loan details |
| existing_loans, num_dependents | Household financial context |
| application_date | Date the loan application was submitted |
| default_flag | 1 = defaulted, 0 = repaid (target variable) |

## Project Structure

```
├── loan_applications_raw.csv          # Raw dataset (as received)
├── loan_applications_clean.csv        # Cleaned + feature-engineered dataset
├── Loan_Default_Risk_Analytics.ipynb  # Full analysis notebook (SQL → EDA → model)
├── dashboard.html                     # Interactive risk analytics dashboard (open in browser)
├── eda_overview.png                   # Key EDA charts
├── monthly_trend.png                  # Application & disbursement trend
├── model_performance.png              # Confusion matrix + ROC curve
├── feature_importance.png             # Risk driver ranking
└── README.md
```

## Workflow

1. **SQL extraction** — Loaded the raw export into a SQLite database and answered core business questions with `SELECT`, `GROUP BY`, `HAVING`, and `CASE WHEN` queries (default rate by state, employment type, credit band, loan purpose).
2. **Data cleaning (Pandas)** — Removed duplicate applicant records, corrected invalid negative ages, and imputed missing income using employment-type-level medians.
3. **Feature engineering** — Built `emi_to_income_ratio`, `loan_to_income_ratio`, `credit_band`, and `age_group` to strengthen the risk signal.
4. **EDA** — Visualized default rate by credit band, employment type, and EMI burden; reviewed a correlation heatmap of key numeric drivers.
5. **Modeling** — Trained a Logistic Regression baseline (class-weighted for the ~33% default rate) and evaluated it with accuracy, precision, recall, F1, and ROC-AUC.
6. **Dashboard** — Built an interactive HTML dashboard (Chart.js) summarizing portfolio KPIs, monthly disbursement trend, and default-rate breakdowns by state, credit band, employment type, and loan purpose — the kind of view a Power BI/Tableau dashboard would provide for the credit team.

## Key Findings

- **Credit score is the strongest single driver** — applicants below 600 default at ~48%, nearly 3x the rate of 800+ scorers.
- **EMI-to-income ratio above ~0.5** sharply increases default risk — a case for capping approved EMI at 40% of income.
- **Self-employed applicants** default more than salaried applicants despite similar or higher income, pointing to income-verification risk.
- **Medical and Vehicle loan purposes** run above-average default rates.
- Baseline model reaches **ROC-AUC ≈ 0.70** — solid enough to prioritize applications for manual underwriting review, not to fully automate rejection decisions.

## Tools & Skills Demonstrated

SQL (SQLite) · Python · Pandas · NumPy · Matplotlib · Seaborn · Scikit-learn · Exploratory Data Analysis · Feature Engineering · Data Cleaning · Logistic Regression · Model Evaluation (ROC-AUC, Precision/Recall) · Interactive Dashboard Design

## Dashboard Preview
![Dashboard]<img width="1728" height="837" alt="image" src="https://github.com/user-attachments/assets/77ad3f8a-61fa-40ac-a751-bd988f61e687" />


## How to Run

1. Open `Loan_Default_Risk_Analytics.ipynb` in Jupyter Notebook, JupyterLab, or Google Colab (upload `loan_applications_raw.csv` alongside it).
2. Run all cells top to bottom — each cell regenerates the SQL queries, cleaning steps, charts, and model.
3. Open `dashboard.html` directly in any browser to view the interactive risk dashboard (no server needed).

---

## Suggested Resume Bullets (for this project)

> **Loan Default Risk Analytics — Personal Project**
> Tech Stack: SQL, Python (Pandas, NumPy, Scikit-learn), Matplotlib/Seaborn, HTML/Chart.js
> - Analyzed 6,000 loan applications using SQL and Python to identify key default risk drivers (credit score, EMI-to-income ratio, employment type), uncovering a 3x default-rate gap between poor and excellent credit bands.
> - Cleaned and engineered features on raw applicant data (handled duplicates, missing values, and invalid entries) and built a Logistic Regression risk model achieving 0.70 ROC-AUC.
> - Designed an interactive HTML dashboard summarizing portfolio KPIs and default-rate breakdowns by state, credit band, and loan purpose for credit-risk decision-making.
