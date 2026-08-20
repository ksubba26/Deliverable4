# MSCS-634 Final Project: Predicting and Understanding Customer Churn

**Course:** MSCS-634-B01 — Advanced Big Data and Data Mining
**Dataset:** IBM Telco Customer Churn (7,043 records, 21 attributes)

## Project Overview

This repository consolidates the full four-deliverable data mining project into a
single pipeline: data cleaning and exploration, regression modeling, classification,
clustering, association rule mining, and a final cross-technique synthesis with
practical recommendations and ethical considerations.

**Why this dataset:** it exceeds the project's minimum size requirement (500+
records, 8-10+ attributes), mixes numerical and categorical feature types, and
naturally supports every phase of the project — churn as a classification target,
monthly billing as a regression target, service attributes for clustering, and
categorical service columns for association rule mining.

## Project Steps

1. **Data Cleaning** — converted `TotalCharges` from text to numeric (11 blank
   entries from zero-tenure customers imputed as 0), consolidated redundant "no
   service" categories into "No", recoded `SeniorCitizen` to Yes/No.
2. **Exploratory Data Analysis** — found ~26.5% churn rate (class imbalance),
   `TotalCharges` near-collinear with `tenure`/`MonthlyCharges`, and churn
   concentrated among month-to-month, fiber-optic, short-tenure customers.
3. **Feature Engineering** — `NumAddOnServices`, `HasInternet`, `HasPhone`,
   `TenureGroup`.
4. **Regression** — predicted `MonthlyCharges` from services/contract/demographics
   (Linear, Ridge, Lasso); Ridge preferred, R² ≈0.999.
5. **Classification** — predicted `Churn` with a Decision Tree (baseline + tuned via
   GridSearchCV) and k-NN; evaluated with confusion matrix, ROC curve,
   accuracy/F1.
6. **Clustering** — K-Means (k=4) customer segmentation by tenure/billing/services.
7. **Association Rule Mining** — Apriori on a service/contract/churn basket.
8. **Synthesis** — cross-technique insights, practical recommendations, ethical
   considerations, and limitations/future work.

## Major Findings

- **Churn drivers are consistent across every technique used:** short tenure and
  weak commitment (month-to-month contracts, thin service bundles) predict churn far
  more than the bill amount itself.
- **Classification:** baseline Decision Tree achieved the best test ROC AUC (≈0.83);
  the CV-tuned tree scored slightly lower on this specific split (≈0.79) despite
  being selected on stronger evidence (5-fold cross-validated F1) — a useful
  illustration that tuning optimizes for generalization, not for beating one split.
- **Clustering:** customer segments range from 7% churn (low-cost, no-internet,
  reasonable tenure) to 47% churn (short-tenure, mid-bill, thin bundle) — entirely
  unsupervised, with no access to the churn label, yet matching the classification
  and EDA findings.
- **Association rules:** `{Month-to-month contract, Fiber optic internet} →
  Churn=Yes` is the strongest churn-associated rule (lift ≈2.06).
- **Regression:** `MonthlyCharges` is almost fully explained by which services a
  customer subscribes to (R² ≈0.999), confirming price itself is not an independent
  churn driver — it's a proxy for the underlying service/contract choices that
  actually matter.

See the full written report (`Final_Report.docx`) for the complete analysis,
including ethical considerations and detailed recommendations, and the notebook
(`Deliverable4_FinalProject.ipynb`) for all code, comments, and visualizations.

## Repository Contents

- `Deliverable4_FinalProject.ipynb` — consolidated notebook: all code, comments, and
  visualizations for data cleaning, EDA, regression, classification, clustering, and
  association rule mining in one non-redundant pipeline.
- `Final_Report.docx` — comprehensive written report (title page, introduction, data
  preparation, modeling details, evaluation, insights, ethical considerations,
  recommendations, references).
- `Final_Presentation.pptx` — slide deck for the 5–7 minute video presentation.
- `telco.csv` — source dataset.
- `README.md` — this file.

## How to Run

1. Clone this repository
2. Install dependencies: `pip install pandas numpy matplotlib seaborn scikit-learn mlxtend`
3. Open `Deliverable4_FinalProject.ipynb` in Jupyter Notebook/Lab and run all cells
