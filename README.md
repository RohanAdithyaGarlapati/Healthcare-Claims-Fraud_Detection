# Healthcare Claims Fraud Detection

An end-to-end data analytics and machine learning project that detects fraudulent Medicare providers using real CMS claims data. The project covers data cleaning, SQL analysis, feature engineering, ML modeling with XGBoost, and a four-page Power BI dashboard.

## Project Overview

Healthcare fraud costs the US billions of dollars each year. This project builds a fraud detection pipeline on a dataset of 558,000+ Medicare claims across 5,400+ providers, identifying patterns that separate fraudulent billing behavior from legitimate claims.

The final XGBoost model achieves an AUC-ROC of 0.958, meaning it correctly distinguishes fraud from legitimate providers 95.8% of the time.

## Key Findings

- Fraudulent providers bill nearly twice as much on average ($1,400 vs $750 per claim)
- Fraud claims tend to run longer in duration than legitimate ones
- Total billing amount is the strongest predictor of fraud, followed by claims per patient and average hospital stay
- State 46, State 5, and State 49 show the highest fraud concentrations (above 57% fraud rate)

## Tech Stack

- **Python** — data cleaning, feature engineering, ML modeling (pandas, scikit-learn, XGBoost, SHAP)
- **SQL / SQLite** — relational schema with 3 tables, analytical queries for fraud pattern analysis
- **Power BI** — four-page interactive dashboard with KPI cards, provider analysis, state heatmap, and model insights
- **Jupyter Notebooks** — end-to-end reproducible analysis pipeline

## Dataset

Source: [Healthcare Provider Fraud Detection Analysis on Kaggle](https://www.kaggle.com/datasets/rohitrox/healthcare-provider-fraud-detection-analysis)

The dataset contains four files covering Medicare beneficiary details, inpatient claims, outpatient claims, and fraud labels at the provider level. Raw data files are not included in this repo due to size limits but can be downloaded directly from Kaggle.

## Project Structure
Healthcare_Fraud_Detection/
├── notebooks/
│   ├── 01_EDA.ipynb          # Data loading, cleaning, exploratory analysis
│   ├── 02_SQL.ipynb          # SQLite schema, data loading, analytical queries
│   └── 03_ML.ipynb           # Feature engineering, ML models, SHAP, exports
├── outputs/
│   ├── fraud_distribution.png
│   ├── fraud_insights.png
│   ├── roc_curve.png
│   ├── confusion_matrix.png
│   ├── shap_importance.png
│   ├── dashboard_providers.csv
│   ├── dashboard_claims.csv
│   ├── dashboard_states.csv
│   └── dashboard_shap.csv
├── .gitignore
└── README.md
## Machine Learning Results

Two models were trained on provider-level aggregated features:

| Model | AUC-ROC |
|---|---|
| Random Forest | 0.955 |
| XGBoost | 0.958 |

XGBoost was selected as the final model. SHAP analysis identified total billing amount, claims per patient, and average hospital stay as the top three fraud indicators.

## SQL Analysis

Four analytical queries were written against the SQLite database covering fraud rate by claim type, top billing providers, average claim metrics by fraud status, and state-level fraud concentration. These queries fed directly into the Power BI dashboard.

## Power BI Dashboard

The dashboard has four pages:

1. **Overview** — KPI cards showing total providers, fraud count, fraud rate, and total billed amount alongside a fraud vs legit breakdown
2. **Provider Analysis** — scatter plot of billing vs fraud probability, top provider table sortable by risk score
3. **State Analysis** — bar chart of fraud rate by state, detailed state breakdown table
4. **Model Insights** — SHAP feature importance chart, high-risk provider table filtered to fraud probability above 80%

## How to Run

1. Download the dataset from Kaggle and place the four CSV files in a `data/` folder
2. Create a virtual environment and install dependencies:
3. Run the notebooks in order: `01_EDA.ipynb` then `02_SQL.ipynb` then `03_ML.ipynb`
4. Open the Power BI dashboard using the exported CSV files in the `outputs/` folder
